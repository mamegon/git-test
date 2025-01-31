# 立て方（AWS EC2）
## 参考URL
https://gitlab-docs.creationline.com/omnibus/installation/

## 起動
### サーバ準備
1. デフォルトのVPCのサブネットにInternet Gatewayがあることを確認
1. SGの作成（MyIPからSSH、HHTP、HTTPSを許可）
1. EC2をパブリックサブネットで起動（Amazon Linux 2023、t3large、30GB）

### GitLabインストール
1. 起動したインスタンスに接続
1. 右記ページのコマンドの通り実行（postfix除く）：https://about.gitlab.com/install/#amazonlinux-2023

### ログイン
ホストはEC2のIPアドレス
ユーザはroot
パスワードはサーバにログインし以下で確認
```
sudo grep 'Password:' /etc/gitlab/initial_root_password
```

# 立て方（Docker）
## 参考URL
https://gitlab-docs.creationline.com/ee/install/docker.html

## 注意
以下の通りで建てられるが、WindowsPCに負荷がかかり重いので断念。

## 起動
xxxxはUser名に変換
事前にDockerDesktopを起動
以下のコマンドは1行として貼り付けをする。
```
$GITLAB_HOME = "C:\Users\xxxx\Desktop\work\code\tmp-gitlab"

docker run --detach `
  --hostname gitlab.example.com `
  --publish 443:443 --publish 80:80 --publish 22:22 `
  --name gitlab `
  --restart always ` 
  --volume $GITLAB_HOME/config:/etc/gitlab `
  --volume $GITLAB_HOME/logs:/var/log/gitlab ` 
  --volume $GITLAB_HOME/data:/var/opt/gitlab `
  --shm-size 256m `
  gitlab/gitlab-ee:latest
```

## ログイン
ホストはlocalhost
ユーザはroot
パスワードは以下で確認
```
docker exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password
```