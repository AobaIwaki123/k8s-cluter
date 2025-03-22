# CephFSを用いたPVCの構築

https://www.tunamaguro.dev/articles/20240318-kubernetes%E3%81%8B%E3%82%89Proxmox%E3%81%AECeph%E3%82%92%E4%BD%BF%E3%81%86/

## Helm Repoの追加
```sh
$ helm repo add rook-release https://charts.rook.io/release
$ helm install --create-namespace --namespace rook-ceph rook-ceph rook-release/rook-ceph
NAME: rook-ceph
LAST DEPLOYED: Sat Mar 22 06:28:21 2025
NAMESPACE: rook-ceph
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
The Rook Operator has been installed. Check its status by running:
  kubectl --namespace rook-ceph get pods -l "app=rook-ceph-operator"

Visit https://rook.io/docs/rook/latest for instructions on how to create and configure Rook clusters

Important Notes:
- You must customize the 'CephCluster' resource in the sample manifests for your cluster.
- Each CephCluster must be deployed to its own namespace, the samples use `rook-ceph` for the namespace.
- The sample manifests assume you also installed the rook-ceph operator in the `rook-ceph` namespace.
- The helm chart includes all the RBAC required to create a CephCluster CRD in the same namespace.
- Any disk devices you add to the cluster in the 'CephCluster' must be empty (no filesystem and no partitions).
```

## ArgocdでRookをデプロイ

```sh
$ argocd app create --file ./rook.yaml
```

- ProxmoxでPoolを作成

## Ceph External Clusterの作成
```sh
$ wget https://raw.githubusercontent.com/rook/rook/release-1.13/deploy/examples/create-external-cluster-resources.py
$ python3 create-external-cluster-resources.py --namespace rook-ceph-external --rbd-data-pool-name k8s-pv-pool --format bash --skip-monitoring-endpoint --v2-port-enable
# 出力をenv.shなどに保存
```

- 環境変数をk8s-clientで読み込む

```sh
$ source env.sh
```

## 諸々のリソースを作成

```sh
$ wget https://raw.githubusercontent.com/rook/rook/release-1.13/deploy/examples/import-external-cluster.sh
. import-external-cluster.sh

--2025-03-22 06:43:02--  https://raw.githubusercontent.com/rook/rook/release-1.13/deploy/examples/import-external-cluster.sh
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.110.133, 185.199.109.133, 185.199.111.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.110.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 12595 (12K) [text/plain]
Saving to: ‘import-external-cluster.sh’

import-external-cluster.sh                  100%[==========================================================================================>]  12.30K  --.-KB/s    in 0.002s  

2025-03-22 06:43:02 (5.76 MB/s) - ‘import-external-cluster.sh’ saved [12595/12595]

namespace/rook-ceph-external created
secret/rook-ceph-mon created
configmap/rook-ceph-mon-endpoints created
secret/rook-csi-rbd-node created
secret/rook-csi-rbd-provisioner created
secret/rook-csi-cephfs-node created
secret/rook-csi-cephfs-provisioner created
storageclass.storage.k8s.io/ceph-rbd created
storageclass.storage.k8s.io/cephfs created
```

## 外部に接続する用のCeph Clusterを作成

```sh
$ wget https://raw.githubusercontent.com/rook/rook/release-1.13/deploy/charts/rook-ceph-cluster/values-external.yaml
$ helm install --create-namespace --namespace $NAMESPACE rook-ceph-cluster --set operatorNamespace=rook-ceph rook-release/rook-ceph-cluster -f values-external.yaml
coalesce.go:237: warning: skipped value for rook-ceph-cluster.cephObjectStores: Not a table.
coalesce.go:237: warning: skipped value for rook-ceph-cluster.cephFileSystems: Not a table.
coalesce.go:237: warning: skipped value for rook-ceph-cluster.cephBlockPools: Not a table.
coalesce.go:237: warning: skipped value for rook-ceph-cluster.cephBlockPools: Not a table.
coalesce.go:237: warning: skipped value for rook-ceph-cluster.cephFileSystems: Not a table.
coalesce.go:237: warning: skipped value for rook-ceph-cluster.cephObjectStores: Not a table.
W0322 06:43:31.403908   52673 warnings.go:70] unknown field "spec.upgradeOSDRequiresHealthyPGs"
NAME: rook-ceph-cluster
LAST DEPLOYED: Sat Mar 22 06:43:30 2025
NAMESPACE: rook-ceph-external
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
The Ceph Cluster has been installed. Check its status by running:
  kubectl --namespace rook-ceph-external get cephcluster

Visit https://rook.io/docs/rook/latest/CRDs/Cluster/ceph-cluster-crd/ for more information about the Ceph CRD.

Important Notes:
- You can only deploy a single cluster per namespace
- If you wish to delete this cluster and start fresh, you will also have to wipe the OSD disks using `sfdisk`
```

## ArgocdでCeph External Clusterをデプロイ

```sh
$ argocd app create --file rook/ceph-external-cluster.yaml
$ argocd app sync argocd/rook-ceph-external-cluster
```

## 必要なディレクトリを作成

```sh
$ sudo mkdir -p /var/lib/kubelet/plugins_registry/
$ sudo chown root:root /var/lib/kubelet/plugins_registry/
```

```sh
$ sudo mkdir -p /var/lib/kubelet/plugins/rook-ceph.rbd.csi.ceph.com
$ sudo mkdir -p /var/lib/kubelet/plugins_registry/
```
