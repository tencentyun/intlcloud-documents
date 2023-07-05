ネットワークタイムプロトコル（Network Time Protocol，NTP）は、ネットワーク内の各コンピューターの時刻を同期するために使用されるプロトコルです。その目的は、コンピューターの時計を協定世界時UTCに同期させることです。

Tencent Cloudは、プライベートネットワークデバイス用のプライベートネットワークNTPサーバーを提供します。Tencent Cloud以外のデバイスの場合、Tencent Cloudが提供するパブリックネットワークNTPサーバーを使用できます。

### プライベートネットワーク NTP サーバー

```ruby
time1.tencentyun.com
time2.tencentyun.com
time3.tencentyun.com
time4.tencentyun.com
time5.tencentyun.com
```

### パブリックネットワークNTPサーバー
```ruby
ntp.tencent.com
ntp1.tencent.com
ntp2.tencent.com
ntp3.tencent.com
ntp4.tencent.com
ntp5.tencent.com
```
以下は、古いパブリックネットワークNTPサーバーアドレスです。古いアドレスは引き続き使用できますが、新しいパブリックネットワークNTPサーバーアドレスを構成して使用することをお勧めします。
```ruby
time.cloud.tencent.com
time1.cloud.tencent.com 
time2.cloud.tencent.com 
time3.cloud.tencent.com
time4.cloud.tencent.com
time5.cloud.tencent.com
```

LinuxシステムのNTPクロックソースサーバーの設定方法の詳細については、[『LinuxインスタンスのNTPサービスの設定』](https://intl.cloud.tencent.com/document/product/213/32381)をご参照ください。
WindowsシステムのNTPクロックソースサーバーの設定方法の詳細については、[『WindowsインスタンスのNTPサービスの設定』](https://intl.cloud.tencent.com/document/product/213/32380)をご参照ください。



