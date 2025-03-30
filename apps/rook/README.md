## Argo CD で Rook をデプロイ

```sh
$ argocd app create --file ./rook-ceph.yaml
```

## 外部のCeph Clusterに接続するためのリソースを追加

Rook経由ではなく、Proxmoxの機能でCephを作成しているため以下が必要になる
Rookで全てまとめた方がおそらく楽

```sh
$ argocd app create --file ./rook-ceph-external-cluster.yaml
```

## Cephのデフォルトストレージクラスを変更

```sh
$ kubectl patch storageclass ceph-rbd \
  -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
```

## Argo CD で見るブランチの切り替え

```sh
$ argocd app set rook-ceph --revision {branch_name}
```
