バージョン
 GitLab: v17.11.2
# GitLabの導入
### インストール

GitLab Community Editionをインストールする

```bash
sudo apt-get update
sudo apt-get install -y curl openssh-server ca-certificates tzdata perl
sudo apt-get install -y postfix

curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash

sudo EXTERNAL_URL="http://localhost" apt-get install gitlab-ce
```

参考：https://kz99.hatenablog.com/entry/2023/08/15/142639
### サーバ操作
```
sudo gitlab-ctl stop # サービス停止
sudo gitlab-ctl reconfigure # 設定ファイル読み込み
sudo gitlab-ctl start # サービス起動
sudo gitlab-ctl restart # サービス再起動
```
### アクセス

前提：WSLの場合localhostフォワーディングされている

ブラウザで`http://localhost`にアクセス

以下入力してログイン
ユーザ名：root
パスワード：<サーバの`/etc/gitlab/initial_root_password`記載のパスワード>

User Settings > Passwordを選択し適当にパスワードを変更
`hogefuga`にした

##  ホスト側の接続設定

`~/.ssh/id_rsa.pub`をアカウントのSSH Keyに追加
`~/.ssh/config`を設定：
```
Host gitlab
  HostName localhost
  User root
  IdentityFile ~/.ssh/id_rsa
```

### プロジェクト作成
ホームから`Groups > New group`を選択しGroup作成
`New Project`を選択しからプロジェクト作成
通常の手順でclone, pushできるはず

# GitLab Runnerの導入

通常GitLab RunnerはGitLabとは別のマシンにインストールする
ここではWSL2に直接インストールする

```bash
curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash
sudo apt install gitlab-runner
```

参考：https://docs.gitlab.com/runner/install/linux-repository/

# GitLab Runnerの作成

前提：プロジェクトのメンテナであること

\[GitLab UIでの操作\]
UIから対象プロジェクトを開きサイドバーの`Settings > CI/CD`を選択
`Runners > New project runner`を選択
`Tags > Run untagged jobs`にチェック[^要確認]
`Create runner`を選択すると画面遷移する
PlatformとしてLinuxを選択

\[GitLab Runnerサーバでの操作\]

```bash
gitlab-runner register  --url http://localhost  --token <your_runner_authentication_token>
```

`executor`を選択するプロンプトには`shell`と回答

```bash
gitlab-runner run
```

UIのRunnersに緑の丸がついたrunnerが登録される

参考： https://docs.gitlab.com/runner/register/