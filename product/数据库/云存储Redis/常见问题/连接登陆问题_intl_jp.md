### CVM とデータベースを同じリージョンに配置する場合、Redis を接続するには？
CVM とデータベースを同じリージョンに配置する場合、イントラネットアクセスを使用してください。接続については [接続ガイド](https://cloud.tencent.com/document/product/239/30877)を参照してください。

### CVM とデータベースを異なるリージョンに配置する場合、Redis を接続するには？
基本ネットワークと VPC ネットワークの相互運用を行います。[Classiclink](https://cloud.tencent.com/document/product/215/20083)を参照してください。
VPC ネットワーク間の相互運用については、[Peering Connection（PC）](https://cloud.tencent.com/document/product/215/20082)を参照してください。

### TencentDB for Redis の ping が通らない場合、どのよう対処する？ 
Redis はデフォルトの状態で`ping`を禁止しています。telnet を使用して接続性を検査できます。

### Redis の外部ネットワークアクセスを開通するには？ 
TencentDB for Redis は現在、外部ネットワークアクセスに対応していません。
外部ネットワークアクセスに対応する必要がある場合、外部ネットワーク付きの CVM を介して、Iptable が代理する方法で実行できます。

### パスワードなしで Redis にログインするには？ 
現在のところ、パスワードなしでログインすることはできません。

