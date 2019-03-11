## 基礎となる Dockerイメージの作成

### 構成
- CentOS6
- Apache 2.4
- PHP 5.6

###
### Apache 設定ファイルの編集
- 実行ユーザー・グループを webuser とする
- webuser のホームディレクトリに Apache の DocumentRoot を設定する
- ログローテイションを有効にする

#### Docker ファイル内の httpd.conf を取得する
```
docker run [イメージ] cat /etc/httpd/conf/httpd.conf > httpd.conf
```


#### php.ini の設定
- メモリ使用量を増加
- UTF-8をデフォルトの文字コードに設定
- タイムアウト対策