## k0sctlでk8s clusterを構築

```sh
$ make apply # k0sctl apply --config k0sctl.yml
$ make config # k0sctl kubeconfig > ~/.kube/config
```

## k0sctlでk8s clusterを削除

```sh
$ make reset # k0sctl reset --config k0sctl.yml
```

