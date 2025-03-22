# Harbor Setup with Helm/ArgoCD

# 1. Install Harbor with Helm

## ADD Helm Repo

```sh
$ helm repo add harbor https://helm.goharbor.io
$ helm repo update
```

## Add Secret for GCS

```sh
$ kubectl create ns harbor
$ kubectl create secret generic harbor-gcs-secret \
  --from-file=key.json=/path/to/gcs-service-account.json \
  -n harbor
```

## Add Values Yaml

- [values.yaml](values.yaml)

## Install Harbor

```sh
$ helm install harbor harbor/harbor -n harbor --create-namespace -f values.yaml
```
