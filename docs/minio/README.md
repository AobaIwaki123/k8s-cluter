# Install Minio

```sh
$ kubectl create ns minio-operator
```

## 1. Minio Operatorをインストール

### 1-1. Helmを使う場合

```sh
$ helm repo add minio https://operator.min.io/
$ helm repo update
```

```sh
$ helm install \
  --namespace minio-operator \
  operator minio-operator/operator
```

### 1-2. ArgoCDを使う場合

```sh
$ argocd app create --file apps/minio-operator.yaml
```
