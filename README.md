# Serverless + API Gateway + Auth0サンプル

本リポジトリは、API GatewayにAuth0認証を追加したサンプルです。

## 前提条件

### 必須ソフト
以下ソフトがインストールされていること

1. serverless cli(Framework Core: 2.65.0以上)
2. aws cli(2.2.20以上)

### 必須アカウント
以下サービスのアカウントを用意すること

1. [AWS](https://aws.amazon.com/jp/)
2. [Auth0](https://auth0.com/jp)

### aws cli認証設定が完了している
[ここ](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/cli-configure-files.html)を参考にaws cliの認証設定を完了させる

### Auth0 API、APP

1. 任意の[Auth0 API](https://auth0.com/docs/get-started/set-up-apis) を登録する
2. 1.のAPIに紐づいた [Machine to Machine](https://auth0.com/docs/get-started/create-apps/machine-to-machine-apps) のApplicationを登録する

## 動かし方
以降のコマンド例のカレントディレクトリは```<本リポジトリをcloneした場所>```であるとします。

### セットアップ

```shell
cp .env.template .env

# .envに環境に応じた値をセットする
vim .env
```

### デプロイ

```shell
sls deploy

# APIサーバのURLが表示されるので、控えておく
# メモし忘れても、AWS CloudFormationの画面でAPI APIGatewayをたどれば確認できる
```

### API呼び出し

```shell
# 以下URLを参考にauth0のアクセストークンを取得する
# https://auth0.com/docs/tokens/access-tokens/get-access-tokens
ACCESS_TOKEN=<auth0 access token>
$ curl -XGET "Authorization: Bearer ${ACCESS_TOKEN}" "https://<API GatewayのURL>/"
```