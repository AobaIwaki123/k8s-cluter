```sh
$ argocd app create --file ./argocd/cloudflare-tunnel-ingress-controller.yml
```

### Permissions: 

CloudflareのPermissionは`:`区切りの3つのパートから構成されます。

- Zone:Zone:Read
- Zone:DNS:Edit
- Account:Cloudflare Tunnel:Edit

## 参考

- [自宅 kubernetes で cloudflare-tunnel-ingress-controller を使ってお手軽外部公開](https://zenn.dev/yh/articles/11823e77bd4379)
- [Cloudflare Tunnel Ingress Controller](https://github.com/STRRL/cloudflare-tunnel-ingress-controller)
