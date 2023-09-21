This is a potential bug.

```bash
$ kustomize version
{Version:kustomize/v4.5.5 GitCommit:daa3e5e2c2d3a4b8c94021a7384bfb06734bcd26 BuildDate:2022-05-20T20:21:22Z GoOs:darwin GoArch:arm64}

$ kustomize build --enable-helm '--load-restrictor=LoadRestrictionsNone' .
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app.kubernetes.io/version: FOOBAR
  name: app
spec:
  template:
    spec:
      containers:
      - image: foobar:20230921.12345678
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  labels:
    app.kubernetes.io/version: 2.023092112345678e+07
  name: ingress
```

The `replacements` version is changed from `20230921.12345678` to the scientific notation of `2.023092112345678e+07`.