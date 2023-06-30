### CVMにはFTPサービスが付属していますか。
ユーザーが実際のニーズに応じて、FTPサービスをインストールおよび設定できます。
- Windowsに含まれるFTPサービスを使用してFTPサイトを構築するには、[Windows CVMでFTPサービスの構築](https://intl.cloud.tencent.com/document/product/213/10414)をご参照ください。
- vsftpdソフトウェアを使用してFTPサイトを構築するには、[Linux CVMでFTP サービスの構築](https://intl.cloud.tencent.com/document/product/213/10912)をご参照ください。

### Windows CVMにファイルをアップロードするにはどうすればよいですか。
- ローカルコンピュータがWindows OSなら、[MSTSCを使用してファイルをWindows CVMにアップロード](https://intl.cloud.tencent.com/document/product/213/2761)することができます。   
- ローカルコンピュータがLinux OSなら、[RDSを使用してファイルをWindows CVMにアップロード](https://intl.cloud.tencent.com/document/product/213/34822)することができます。
- ローカルコンピュータがMac OSなら、[MRDを使用してファイルをWindows CVMにアップロード](https://intl.cloud.tencent.com/document/product/213/34820)することができます。

### ローカルホストとWindows CVM間でデータを転送する方法。
以下の方法でデータを転送できます。
- RDPファイルを使用してローカルWindowsコンピューターからWindows CVMにログインする場合、ローカルファイルを直接CVMにドラッグしてアップロードできます。
- [MSTSCを使用してファイルをWindows CVMにアップロード](https://intl.cloud.tencent.com/document/product/213/2761)します。
- [Linux CVMでFTP サービスの構築](https://intl.cloud.tencent.com/document/product/213/10912)を介して、ファイルをCVMに転送します。　

### WinSCPを使用してどのようにファイルをLinux CVMにアップロードしますか。
詳細については、[WindowsシステムがWinSCPを使用してLinux CVMにファイルをアップロード](https://intl.cloud.tencent.com/document/product/213/2131) セクションをご参照ください。　

### Linux CVMにファイルをアップロードまたはダウンロードするにはどうすればよいですか。
詳細については、[LinuxシステムがSCPを使用してLinux CVMにファイルをアップロード](https://intl.cloud.tencent.com/document/product/213/2133)セクションをご参照ください。

### FTPを使用してファイルをアップロードするとき、クライアント側とサーバー側の接続がタイムアウトした場合はどうすればよいですか。
サーバー側のファイアウォールまたはセキュリティグループが接続をブロックしている可能性があります。この問題をトラブルシューティングするには、以下の手順に従ってください：
1. サーバーのファイアウォール設定を確認します。
2. ファイアウォールを無効にするか、ルールを追加します。
