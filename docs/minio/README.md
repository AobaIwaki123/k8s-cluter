# Install Minio


## 1. Minio Operatorをインストール

```sh
$ kubectl create ns minio-operator
```

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

## 2. Minio Tenantを作成

```sh
$ kubectl create ns minio-tenant
```

使用したいStorageClassをデフォルトに設定しておく (TODO: StorageClass作成時点でやる方法を今度調べる)  
以下はCephのStorageClassをデフォルトに設定する例

```sh
$ kubectl patch storageclass ceph-rbd \
  -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
```

```sh
$ kubectl get sc
# DefaultになっていればOK
```

### 2-1. Helmを使う場合

```sh
$ helm install \
  --namespace minio-tenant \
  --values values.yaml \
  TENANT-NAME minio-operator/tenant
``` 

### 2-2. ArgoCDを使う場合

```sh
$ argocd app create --file apps/minio-tenant.yaml
```
