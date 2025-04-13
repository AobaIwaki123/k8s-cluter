# Deploy Cloudflare on k8s Cluster

## 1. Create Namespace

```sh
$ kubectl create ns cloudflare
```

## 2. Create Secret

```sh
$ kubectl create secret generic cloudflare-credentials \
  --from-file=credentials.json=/path/to/your/credentials.json \
  -n cloudflared
```

## 3. Set ConfigMap

```sh
$ kubectl apply -f manifests/cloudflared-config.yaml
```

## 4. Deploy Cloudflared

```sh
$ kubectl apply -f manifests/cloudflared-deploy.yaml
```
