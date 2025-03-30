## Argo CD でRookをデプロイ

```sh
$ argocd app create --file ./rook-ceph.yaml
```

```sh
$ argocd app create --file ./rook-ceph-external-cluster.yaml
```

## Argo CD で見るブランチの切り替え

```sh
$ argocd app set rook-ceph --revision {branch_name}
```
