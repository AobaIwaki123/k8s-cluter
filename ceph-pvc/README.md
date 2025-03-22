# CephFSを用いたPVCの構築

```sh
$ kubectl apply -f https://raw.githubusercontent.com/ceph/ceph-csi/devel/deploy/cephfs/kubernetes/csi-cephfsplugin-provisioner.yaml
$ kubectl apply -f https://raw.githubusercontent.com/ceph/ceph-csi/devel/deploy/cephfs/kubernetes/csi-cephfsplugin.yaml
```

```sh
$ kubectl create secret generic ceph-secret \
  --type="kubernetes.io/rbd" \
  --from-literal=adminID=admin \
  --from-literal=adminKey='AQDx...' \
  --namespace=harbor
```

```sh
$ helm upgrade --install harbor harbor/harbor -n harbor -f values.yml
```
