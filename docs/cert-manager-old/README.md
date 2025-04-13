# Setup Cert Manger

## 1. Install Cert Manager

```sh
$ kubectl create ns cert-manager
```

### 1-0. Install CRDs

```sh
$ kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.17.1/cert-manager.crds.yaml -n cert-manager
```

### 1-1. Helm

```sh
$ helm repo add jetstack https://charts.jetstack.io
$ helm repo update
```

```sh
$ helm install cert-manager --namespace cert-manager --version v1.17.1 jetstack/cert-manager
```

### 1-2. ArgoCD

```sh
$ argocd app create --file argocd/cert-manager.yaml
```

## 2. Cloudflare API TokenをSecretに登録

### Permissions:

- Zone:DNS:Edit

### Zone Resources:

Include → Specific Zone →（対象のドメイン名を選択）

```sh
$ kubectl create secret generic cloudflare-api-token-secret \
  --from-literal=api-token=<your-cloudflare-api-token> \
  --namespace=cert-manager
```

## 3. Issuerの作成

```sh
$ kubectl apply -f manifests/clusterissuer-letsencrypt.yaml -n cert-manager
```

## 4. Certificateの作成

```sh
$ kubectl apply -f manifests/certificate.yaml
```
