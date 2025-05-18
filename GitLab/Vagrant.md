以下URLからVagrant公式にアクセスし`Windows binary download > AMD64`を選択しインストール（再起動が必要）
https://developer.hashicorp.com/vagrant/install

`disksize`プラグインを追加
```bash
vagrant plugin install vagrant-disksize
```

適当なディレクトリ（ここでは`gitlab`）を作成し以下コマンドでVagrantfileを作成
```bash
vagrant init
```

