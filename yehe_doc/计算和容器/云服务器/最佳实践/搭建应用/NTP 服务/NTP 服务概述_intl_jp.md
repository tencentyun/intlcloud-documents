ネットワークタイムプロトコル（Network Time Protocol，NTP）は、ネットワーク内の各コンピューターの時刻を同期するために使用されるプロトコルです。 その目的は、コンピューターの時計を協定世界時UTCに同期させることです。

Tencent Cloudは、プライベートネットワークデバイス用のプライベートネットワークNTPサーバーを提供します。Tencent Cloud以外のデバイスの場合、Tencent Cloudが提供するパブリックネットワークNTPサーバーを使用できます。

### プライベートネットワーク NTP サーバー

```
ntpupdate.tencentyun.com
```

### パブリックネットワークNTPサーバー

```
time1.cloud.tencent.com 
time2.cloud.tencent.com 
time3.cloud.tencent.com
time4.cloud.tencent.com
time5.cloud.tencent.com
```

LinuxシステムのNTPクロックソースサーバーの設定方法の詳細については、[「 LinuxインスタンスのNTPサービスの設定」](https://cloud.tencent.com/document/product/213/30393)をご参照ください。
WindowsシステムのNTPクロックソースサーバーの設定方法の詳細については、[「 WindowsインスタンスのNTPサービスの設定」](https://cloud.tencent.com/document/product/213/30394)をご参照ください。

