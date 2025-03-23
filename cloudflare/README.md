```sh
$ kubectl create ns cloudflared
```

```sh
$ kubectl apply -f manifests/secret.yaml -n cloudflared
```

```sh
$ kubectl apply -f manifests/configmap.yaml -n cloudflared
```

```sh
$ kubectl apply -f manifests/deployment.yaml -n cloudflared
```
