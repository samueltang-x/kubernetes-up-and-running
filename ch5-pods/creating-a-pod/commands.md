```shell
docker login
```

secret-myregistrykey.yaml:
```json
apiVersion: v1
kind: Secret
metadata:
  name: myregistrykey
  namespace: default
data:
  .dockerconfigjson: ewoJImF1dGhzIjogewoJCSJodHRwczovL2luZGV4LmRvY2tlci5pby92MS8iOiB7CgkJCSJhdXRoIjogImMyRnRkV1ZzZEdGdVp6cFRZVzExWld4QVpHOWphMlZ5IgoJCX0KCX0KfQ==
type: kubernetes.io/dockerconfigjson
```
```shell
kubctl get secret
kubectl apply -f secret-myregistrykey.yaml
kubctl get secret
```


```shell
kubectl run kuard --image=samueltang/kuard-demo:blue --overrides='{"spec":{"imagePullSecrets":[{"name":"myregistrykey"}]}}'
k get po kuard -o wide
k delete po kuard
```