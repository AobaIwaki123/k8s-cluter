# Deploy Cloudflare on k8s Cluster

```sh
$ kubectl create ns cloudflare
```

```sh
$ kubectl create secret generic cloudflare-credentials \
  --from-file=credentials.json=/path/to/your/credentials.json \
  -n cloudflared
```
