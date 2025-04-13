## 1. Argo CD で Rook をデプロイ

```sh
$ argocd app create --file ./argocd/rook-ceph.yaml
```

## 2. ProxmoxでPoolを作成する

### 2-1. Proxmox GUIで作成する

- PVE Node > Ceph > Pool > Create: `k8s-pv-pool`

### 2-2. Proxmox CLIで作成する

```sh
$ pveceph pool create k8s-pv-pool --pg_autoscale_mode-on
```

## 3. 環境変数の取得

以下のコマンドを**Proxmoxのホスト上**で実行する

```sh
$ wget https://raw.githubusercontent.com/rook/rook/release-1.16/deploy/examples/create-external-cluster-resources.py
$ python3 create-external-cluster-resources.py --namespace rook-ceph-external --rbd-data-pool-name k8s-pv-pool --format bash --skip-monitoring-endpoint --v2-port-enable
# 出力値は後で使うのでコピーしておく
```

次に以下のコマンドを実行する **`kubectl` が使えるホスト上** で以下のコマンドを実行する

```sh
# env.shに前に取得した環境変数をコピーする
$ source ./env.sh
$ wget https://raw.githubusercontent.com/rook/rook/release-1.16/deploy/examples/import-external-cluster.sh
. import-external-cluster.sh
```

## 4. Cephのデフォルトストレージクラスを変更

```sh
$ kubectl patch storageclass ceph-rbd \
  -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
```

## 5. 外部のCeph Clusterに接続するためのリソースを追加

Rook経由ではなく、Proxmoxの機能でCephを作成しているため以下が必要になる
Rookで全てまとめた方がおそらく楽

```sh
$ argocd app create --file ./argocd/rook-ceph-external-cluster.yaml
```

### 参考

- [Proxmox × k0s × CephFS で構築するKubernetesストレージ基盤](https://zenn.dev/aobaiwaki/articles/28ad58a3acaf24)
- [kubernetesからProxmoxのCephを使う](https://www.tunamaguro.dev/articles/20240318-kubernetes%E3%81%8B%E3%82%89Proxmox%E3%81%AECeph%E3%82%92%E4%BD%BF%E3%81%86/)
