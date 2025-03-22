# CephFSを用いたPVCの構築

## CephFS CSI Driverのインストール

```sh
$ kubectl apply -f https://raw.githubusercontent.com/ceph/ceph-csi/devel/deploy/cephfs/kubernetes/csi-cephfsplugin-provisioner.yaml
$ kubectl apply -f https://raw.githubusercontent.com/ceph/ceph-csi/devel/deploy/cephfs/kubernetes/csi-cephfsplugin.yaml
```

## CephFSのSecretの作成

```sh
$ kubectl create secret generic ceph-secret \
  --type="kubernetes.io/rbd" \
  --from-literal=adminID=admin \
  --from-literal=adminKey='LNnyP1IWrVjM181' \
  --namespace=harbor
```

## CephFSのStorageClassの作成

```sh
$ kubectl apply -f storage-class.yml
```

## Helm設定のアップデート

```sh
$ helm upgrade --install harbor harbor/harbor -n harbor -f values.yml
```
