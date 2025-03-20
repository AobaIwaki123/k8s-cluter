# 前準備

## Install asdf

```sh
$ wget https://github.com/asdf-vm/asdf/releases/download/v0.16.5/asdf-v0.16.5-linux-amd64.tar.gz
$ tar -xvzf asdf-v0.16.5-linux-amd64.tar.gz
$ sudo install asdf /usr/bin
```

## Install golang with asdf

```sh
$ asdf plugin add golang https://github.com/asdf-community/asdf-golang.git
$ asdf install golang latest
$ asdf set golang 1.24.1
$ adsf list
golang
 *1.24.1
```

## Install k0sctl 

```sh
$ go install github.com/k0sproject/k0sctl@latest
```

## Install k9s

```sh
$ wget https://github.com/derailed/k9s/releases/latest/download/k9s_linux_amd64.deb
$ sudo apt install ./k9s_linux_amd64.deb
$ rm k9s_linux_amd64.deb
```

## Install Helm with asdf

```sh
$ asdf plugin add helm https://github.com/Antiarchitect/asdf-helm.git
$ asdf install helm latest
$ asdf set helm 3.17.2
$ asdf list
helm
 *3.17.2
```

## Install kubectl with asdf

```sh
$ asdf plugin add kubectl https://github.com/asdf-community/asdf-kubectl.git
$ asdf install kubectl latest
$ asdf set kubectl 1.32.3
$ asdf list
kubectl
 *1.32.3
```

## Install argocd with asdf

```sh
$ asdf plugin add argocd https://github.com/beardix/asdf-argocd.git
$ asdf install argocd latest
$ asdf set argocd 2.14.7
$ asdf list
argocd
 *2.14.7
```
