```sh
$ argocd app create --file ./cloudflare-tunnel-ingress-controller.yaml
```

### Permissions: 

- Zone:Zone:Read
- Zone:DNS:Edit
- Account:Cloudflare Tunnel:Edit

## 参考

- [自宅 kubernetes で cloudflare-tunnel-ingress-controller を使ってお手軽外部公開](https://zenn.dev/yh/articles/11823e77bd4379)
- [Cloudflare Tunnel Ingress Controller](https://github.com/STRRL/cloudflare-tunnel-ingress-controller)
