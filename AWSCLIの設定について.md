## AWS CLIの設定について

### コンソールにて
AWS Access Key と AWS Secret Access Key を作成する

### Linuxへのインストール
```
sudo pip install awscli
```

### 設定

次のコマンドを実行

```
aws configure
```
以下の内容を聞いてくるので、IAMの認証情報で発行したアクセスキーを登録する。

```
AWS Access Key ID [None]: *************ID
AWS Secret Access Key [None]: ******************************KEY
Default region name [None]: ap-northeast-1
Default output format [None]: json
```

### 設定の確認
設定の確認は以下の通り

```
aws configure list
      Name                    Value             Type    Location
      ----                    -----             ----    --------
   profile                <not set>             None    None
access_key                <not set>             None    None
secret_key                <not set>             None    None
    region                <not set>             None    None
```

### バージョンアップ
```
sudo pip install -U awscli
```
### プロファイル切り替えて使う場合は、アカウント毎にプロファイルを作成

```
aws configure --profile profile_name
```

cliを実行する毎にプロファイルを指定する

```
aws s3 list --profile profile_name
```
もしくは
```
export AWS_DEFAULT_PROFILE=profile_name
```
