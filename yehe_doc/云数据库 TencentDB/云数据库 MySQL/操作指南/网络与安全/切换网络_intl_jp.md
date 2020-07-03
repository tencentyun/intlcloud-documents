## 操作シナリオ
Tencent Cloudネットワークは[基幹ネットワークとVirtual Private Cloud（VPC）](https://intl.cloud.tencent.com/document/product/215/31807)に分かれ、ユーザーに異なる優良なサービスを提供します。これに基づき、お客様がネットワークを管理しやすいよう、当社では以下の更に柔軟なサービスを提供します。
- **ネットワーク間の切り替え**
  - 基幹ネットワークのVirtual Private Cloudへの切り替え：1台のCDBの基幹ネットワークをVirtual Private Cloudに切り替えることをサポートします。
  - Virtual Private Cloud AのVirtual Private Cloud Bへの切り替え：1台のCDBのVirtual Private Cloud AをVirtual Private Cloud Bに切り替えることをサポートします。
- **カスタマイズIPの設定**

## 注意事項
- ネットワークを切り替えると、このインスタンスのプライベートネットワークIPが変更される場合があります。デフォルトでは24時間後に古いアクセスIPが無効になりますので、クライアント側のプログラムを速やかに変更してください。古いIPアドレスの回収時間を0時間に設定した場合、ネットワークを変更した後、直ちに古いIPアドレスを回収します。
- 宛先VPCはインスタンスの所属地域及びAvailability Zone内のVPCネットワークとサブネットのみを選択できます。
- 基幹ネットワークをVirtual Private Cloudに切り替えた後は不可逆となり、CDBがVirtual Private Cloudに切り替わった後、他のVirtual Private Cloud及び基幹ネットワークのクラウドサービスと相互に接続されません。

##　操作手順
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンスリストでインスタンス名又は「操作」列の【管理】をクリックすると、インスタンスの詳細ページに進みます。
2. インスタンスの基本情報の「所属ネットワーク」の後、ネットワーク間の切り替えのタイプに基づき、【VPCネットワークへの転換】又は【ネットワークの変更】をクリックします。
3. ポップアップされたダイアログボックスでVirtual Private Cloud及び対応するサブネットを選択し、【確定】をクリックします。
>
>- IPアドレスが指定されていない場合、システムは自動割り当てを行います。
>- CDBのあるVPCを選択することをお勧めします。そうでない場合、（2つのVPC間に[Peering Connection](https://intl.cloud.tencent.com/document/product/553/18827)又は[Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003/30049)を作成しない限り）Cloud Virtual Machineはプライベートネットワークを介してMySQLにアクセスすることができなくなります。
>
   - **基幹ネットワークのVirtual Private Cloudへの転換**
   - **Virtual Private CloudのVirtual Private Cloudへの変換**
![](https://main.qcloudimg.com/raw/274c2057ec225eab9e16b1c18bafa94c.png)
4. インスタンスの詳細ページに戻ると、インスタンスの所属ネットワークを確認することができます。
![](https://main.qcloudimg.com/raw/5342a64814664fa784e256ecbd6f934f.png)
