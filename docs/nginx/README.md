# Install Nginx

## 1. Nginx Ingress Controllerをインストール

```sh
$ kubectl create ns nginx-ingress
```

### 1-1. Helmを使う場合

```sh
$ helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
$ helm repo update
```

```sh
$ helm install \
  --namespace nginx-ingress \
  nginx-ingress ingress-nginx/ingress-nginx
```

### 1-2. ArgoCDを使う場合

```sh
$ argocd app create --file apps/nginx-ingress.yaml
```
