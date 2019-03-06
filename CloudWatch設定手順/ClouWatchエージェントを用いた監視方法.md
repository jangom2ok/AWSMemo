# CloudWatchエージェントを使用したメトリクス取得方法

### 監視対象にロールを割り当てる。
- 「ロールの割り当て方法.md」を参考に監視対象にロールを割り当てる
- ロールにアタッチするポリシーは`AmazonEC2RoleforSSM`と`CloudWatchAgentAdminPolicy`の２つである。

### ssmエージェントのインストール
1. - `mkdir /tmp/ssm`<br>
   - `yum install https://s3.ap-northeast-1.amazonaws.com/amazon-ssm-ap-northeast-1/latest/linux_amd64/amazon-ssm-agent.rpm`
   - `sudo status amazon-ssm-agent`
   - 上記コマンドを実行しエージェントをインストールする。

### CloudWatchエージェントのインストール
1. AWSコンソールから、AWS SystemManagerを選択する。
1. ランコマンドを選択し、コマンドの実行選択する。
1. 検索フィールドに[ドキュメント名のプレフィックス] [等しい] [AWS-ConfigureAWSPackage]と入力し、表示された**AWS-ConfigureAWSPackage**にチェックを入れる。
1. ターゲットは［インスタンスの手動選択］で監視対象にチェックを入れる。
1. コマンドのパラメータで以下を設定する。
  - Action : Install
  - Name : AmazonCloudWatchAgent
  - Version : latest
1. その他の設定は特に触らず、実行を選択する。
1. ステータスに成功！と表示されればインストールが完了する。

### CloudWatchエージェントの設定
1. ` /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard`を実行し、設定ウィザードを起動する、
1. 全ての質問に答え終わり、`Successfully put config to parameter store AmazonCloudWatch-CentOS7.
Program exits now.`と表示されれば設定が完了する。
  - ウィザードの設定項目は全て英語。内容については別途のドキュメントに記載。
  - **注意** collectDを使用する場合、自動でインストールされないので手動でインストールする
    - `yum install collectd`でインストール出来る。

### CloudWatchエージェントの開始
1. AWSコンソールからAWS SystemManagerを選択する
1. ランコマンドを選択し、コマンドの実行を選択する。
1. 検索フィールドに[ドキュメント名のプレフィックス] [等しい] [AmazonCloudWatch-ManageAgent] と入力し、表示された**AmazonCloudWatch-ManageAgent**にチェックを入れる。
1. ターゲットは［インスタンスの手動選択］で監視対象にチェックを入れる。
1. コマンドのパラメータで以下を設定する。
  - Action : configure
  - Mode : ec2
  -  Optional Configuration Source : ssm
  - Optional Configuration Location : (ウィザードで指定した設定ファイル名を入力)
  - Optional Restart : yes
1. その他の設定は特に触らず、実行を選択する。
1. ステータスに成功！と表示されれば起動が完了する。

### メトリクスの反映
1. CloudWatchにエージェントが収集した値が反映されるまで時間がかかる場合がある。
