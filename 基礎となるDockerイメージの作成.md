## 基礎となる Dockerイメージの作成
この文章は`base/Dockerfile`の内容を説明する

### 目標とするLAMP構成
- CentOS6
- Apache 2.4
- PHP 5.6
- MySQL 5.6

### 基本となるCentOS6を公式レポジトリから取得する
```
docker pull centos:centos6
```

#### Docker ファイル内の httpd.conf を取得する方法
```
docker run [イメージ] cat /etc/httpd/conf/httpd.conf > httpd.conf
```

### Apache 設定ファイルの編集
- 実行ユーザー・グループを webuser とする
- webuser のホームディレクトリに Apache の DocumentRoot を設定する
- ログローテイションを有効にする
- その他使用していないオプションを削除

#### php.ini の設定
- メモリ使用量を増加
- UTF-8をデフォルトの文字コードに設定
- 処理のタイムアウト対策
- エラー出力設定
- PHP バージョンを非表示
