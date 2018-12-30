## CFn サンドボックス

### ec2-drift.yaml
ドリフト検知の実験。

0. 状態の変更
    - 起動 => 停止 = 検知なし
0. 設定した値を変更する
    - インスタンスタイプ変更 t2.micro => t2.nano = 検知あり（起動状態は関係ない）NOT_EQUAL
    - Tag: Name 削除 = 検知 REMOVE
0. 設定していない値を変更する
    - Tag: Name 新規追加 = 検知せず
    - Tag: Name 変更 = 検知 NOT_EQUAL
    - Monitoring: 未設定 => true
    - SecurityGroupIngress 追加 => 検知あり ADD
0. AWS::NoValue設定した値を変更する
    - Monitoring: !Ref AWS::NoValue => true = 検知せず
    - Monitoring: true => false = 検知あり NOT_EQUAL
