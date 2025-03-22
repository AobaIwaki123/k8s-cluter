# asdfのインストールとプラグインの追加方法

## Install asdf

```sh
$ wget https://github.com/asdf-vm/asdf/releases/download/v0.16.6/asdf-v0.16.6-linux-amd64.tar.gz
$ tar -xzvf asdf-v0.16.6-linux-amd64.tar.gz 
$ sudo install asdf /usr/bin
```

## Pluginの追加方法

- PLUGIN_NAME: プラグイン名
- PLUGIN_URL: プラグインが公開されているGitHubのURL
- PLUGIN_VERSION: プラグインのバージョン (adsf listで確認できる)

```sh
$ asdf plugin add {PLUGIN_NAME} {PLUGIN_GITHUB_URL}
$ asdf install {PLUGIN_NAME} latest # たまにlatestが使えない場合があるので注意
$ asdf set {PLUGIN_NAME} {PLUGIN_VERSION}
```
