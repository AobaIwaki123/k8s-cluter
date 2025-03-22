# ProxmoxのCeph ClusterにPersistentVolumeClaimを作成する

## 1. Rook Ceph Clusterの作成

```sh
$ kubectl create ns rook-ceph
```

### 1-1. Helmを使う場合
```sh
$ helm repo add rook-release https://charts.rook.io/release
$ helm repo update
```

```sh
$ helm install --namespace rook-ceph rook-ceph-cluster rook-release/rook-ceph-cluster
$ helm install rook-ceph rook-release/rook-ceph \
  --namespace rook-ceph \
  --set csi.kubeletDirPath="/var/lib/k0s/kubelet"
```

### 1-2. ArgoCDを使う場合

```sh
$ argocd app create --file apps/rook.yaml
```

### 2. Ceph Clusterの状態を確認

```sh
$ kubectl -n rook-ceph get pod
NAME                                  READY   STATUS    RESTARTS   AGE
rook-ceph-operator-7dfddd4676-x6522   1/1     Running   0          62s
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

## 4. 外部Cephクラスターに接続する用のCeph Clusterを作成

```sh
$ wget https://raw.githubusercontent.com/rook/rook/release-1.16/deploy/charts/rook-ceph-cluster/values-external.yaml
$ helm install --create-namespace --namespace $NAMESPACE rook-ceph-cluster --set operatorNamespace=rook-ceph rook-release/rook-ceph-cluster -f values-external.yaml
```
