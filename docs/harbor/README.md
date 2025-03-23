# Install Harbor

## 1. Harborのインストール

```sh
$ kubectl create ns harbor
```

### 1-1. Helmを使う場合

```sh
$ helm repo add harbor https://helm.goharbor.io
$ helm repo update
```

```sh
$ helm install \
  --namespace harbor \
  harbor harbor/harbor
```

### 1-2. ArgoCDを使う場合

```sh
$ argocd app create --file apps/harbor.yaml
```
