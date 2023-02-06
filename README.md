# 🖥 provider-citbbs

`provider-citbbs` is a [Crossplane](https://crossplane.io/) Provider
that is meant to show that Crossplane can be extended to any modern
Cloud provider and even those not so modern.

## Requirements
* Crossplane v1.11+

## Usage
First, we need to apply the custom resources:
```
kubectl apply -f package/crds
```
Next, we need to apply our provider configuration:
```
kubectl apply -f examples/provider/config.yaml
```
To create a user:
```
kubectl apply -f examples/sample/user.yaml
```
Which will show you crossplane creating a durable resource from any API, even a BBS:
```
NAME      READY   SYNCED   EXTERNAL-NAME   AGE
example   True    True     example         85s
```

See how crossplane interacts with the API to ensure a durable resource:
```
2023-02-06T17:40:18-05:00	DEBUG	provider-citbbs	Successfully requested creation of external resource	{"controller": "managed/user.user.citbbs.crossplane.io", "request": "/example", "uid": "3e2d5c43-1299-42e8-a6a9-f36c03d28b9c", "version": "222464", "external-name": "", "external-name": "example"}
2023-02-06T17:40:18-05:00	DEBUG	events	Successfully requested creation of external resource	{"type": "Normal", "object": {"kind":"User","name":"example","uid":"3e2d5c43-1299-42e8-a6a9-f36c03d28b9c","apiVersion":"user.citbbs.crossplane.io/v1alpha1","resourceVersion":"222557"}, "reason": "CreatedExternalResource"}
2023-02-06T17:40:18-05:00	DEBUG	provider-citbbs	Reconciling	{"controller": "managed/user.user.citbbs.crossplane.io", "request": "/example"}
2023-02-06T17:40:32-05:00	DEBUG	provider-citbbs	External resource is up to date	{"controller": "managed/user.user.citbbs.crossplane.io", "request": "/example", "uid": "3e2d5c43-1299-42e8-a6a9-f36c03d28b9c", "version": "222558", "external-name": "example", "requeue-after": "2023-02-06T17:41:32-05:00"}
2023-02-06T17:40:32-05:00	DEBUG	provider-citbbs	Reconciling	{"controller": "managed/user.user.citbbs.crossplane.io", "request": "/example"}
2023-02-06T17:40:46-05:00	DEBUG	provider-citbbs	External resource is up to date	{"controller": "managed/user.user.citbbs.crossplane.io", "request": "/example", "uid": "3e2d5c43-1299-42e8-a6a9-f36c03d28b9c", "version": "222586", "external-name": "example", "requeue-after": "2023-02-06T17:41:46-05:00"}
```

Refer to Crossplane's [CONTRIBUTING.md] file for more information on how the
Crossplane community prefers to work. The [Provider Development][provider-dev]
guide may also be of use.

[CONTRIBUTING.md]: https://github.com/crossplane/crossplane/blob/master/CONTRIBUTING.md
[provider-dev]: https://github.com/crossplane/crossplane/blob/master/docs/contributing/provider_development_guide.md
