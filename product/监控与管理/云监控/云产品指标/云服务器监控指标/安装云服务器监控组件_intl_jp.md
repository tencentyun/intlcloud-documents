Tencent Cloud CMを使用して**CVM**のメトリックデータを確認し、アラームを生成する必要がある場合、Tencent Cloud CVM上で監視コンポーネントを正確にインストールする必要があります。CVMメトリックデータの収集は、監視コンポーネントによって決まります。

注：監視データが正常に報告されるよう保証するため、CVMはtcp dport 80ポートを開放する必要があります。

## Linuxインストールガイド

[Linuxインスタンスへのログイン](/doc/product/213/5436)をした後、以下のコマンドを実行してインストールを行うことができます。操作は以下のとおりです。

```
wget http://update2.agent.tencentyun.com/update/linux_stargate_installer
chmod +x linux_stargate_installer
./linux_stargate_installer
```

インストールが完了すると、以下の図のとおりになります。
![](//mccdn.qcloud.com/img568a75015695c.png)
![](//mccdn.qcloud.com/img568a750882880.png)
![](//mccdn.qcloud.com/img568a751592aea.png)

## Windowsインストールガイド

1）[Windowsインスタンスへのログイン](/doc/product/213/5435)をした後、プライベートネットワークで`http://update2.agent.tencentyun.com/update/windows-stargate-installer.exe`にアクセスし、インストールパッケージ`windows-stargate-installer.exe`をインストールします。

2）このプログラムを実行すると、自動的にインストールされます。

インストールが完了すると、以下の図のとおりになります。
![](//mccdn.qcloud.com/img568a758c4c308.png)
![](//mccdn.qcloud.com/img568a75948c917.png)
