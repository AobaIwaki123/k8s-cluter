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

### 参考

- [Proxmox × k0s × CephFS で構築するKubernetesストレージ基盤](https://zenn.dev/aobaiwaki/articles/28ad58a3acaf24)
- [kubernetesからProxmoxのCephを使う](https://www.tunamaguro.dev/articles/20240318-kubernetes%E3%81%8B%E3%82%89Proxmox%E3%81%AECeph%E3%82%92%E4%BD%BF%E3%81%86/)
