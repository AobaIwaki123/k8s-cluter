# Install Minio with ArgoCD

https://blog.min.io/deploy-minio-with-argocd-in-kubernetes/

## Create namespace

```sh
$ kubectl create namespace minio-operator
$ kubectl config set-context --current --namespace=minio-operator
```

## Install Minio

```sh
$ argocd app create minio-operator --repo https://github.com/cniackz/minio-argocd.git --path minio-operator --dest-namespace minio-operator --dest-server https://kubernetes.default.svc --insecure --upsert
```

## Create namespace

```sh
$ kubectl create namespace minio-tenant
$ kubectl config set-context --current --namespace=minio-tenant
$ argocd app create minio-tenant \
  --repo https://github.com/cniackz/minio-argocd.git \
  --path minio-tenant \
  --dest-namespace minio-tenant \
  --dest-server https://kubernetes.default.svc \
  --insecure \
  --upsert
```
