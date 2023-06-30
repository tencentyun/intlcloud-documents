## ユースケース
ユーザーがEIP経由でインターネットにアクセスする場合は、NATモードまたはEIP直通モードを選択することができます。デフォルトは NATモードです。
- NATモードでは、EIPはローカルマシンで表示されません。
- EIP直通モードでは、EIPはローカルマシンで表示され、設定ごとに毎回手動でEIPアドレスを追加する必要がないため、開発コストを最小限に抑えることができます。
- NATモードは、ほとんどのニーズを満たすことができますが、CVMインスタンス内でパブリックIPを確認する場合は、EIP直通モードを使用する必要があります。

## 使用制限
- 現在、EIP直通モードはベータテスト期間中であり、ホワイトリストに登録されているユーザーのみ利用でき、VPC内のデバイスのみをサポートしています。 この機能をご利用になりたい場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してください。
- NATゲートウェイは、直通モードが有効になっている EIPとバインドできますが、直通効果はありません。
- CVMでは、EIP直通モードとNATゲートウェイを同時に有効にすることはできません。CVMが存在するサブネットに関連付けられたルーティングテーブルが、NATゲートウェイを介してパブリックネットワークにアクセスするルーティングポリシーを設定している場合、CVMのEIPを介して直通機能を実現できません。[NATゲートウェイとEIPの優先順位を調整](https://intl.cloud.tencent.com/document/product/1015/32734)することで、CVMがEIPを介してパブリックネットワークにアクセスできるようにすることができます。この場合、EIP直通機能を実現できます。
## 操作手順
EIP直通モードを使用するには、コンソールでEIPを有効にし、OS内でIPをENIに追加する必要があります。また、アプリケーションに基づいてOSでルーティングを構成する必要があります。そのため、プライベートネットワークトラフィックがプライベートIPを通過し、パブリックネットワークトラフィックがパブリックIPを通過するように、IPを構成するためのスクリプトを提供します。
>具体的なアプリケーションに応じてルーティングを構成してください。
>
### Linux CVMでEIP直通を構成する
>
>- Linuxスクリプトは、CentOS 6 以降およびUbuntuをサポートします。
>- Linuxスクリプトは、プライマリENI（eth0）のみをサポートし、現在、セカンダリENIはサポートしません。
>- プライマリENIにバインドされているパブリックIPがEIPでない場合は、先にパブリックIPアドレスをEIPに変換する必要があります。詳細については、[パブリックIPからEIPへの変換](https://intl.cloud.tencent.com/document/product/213/16586#converting-public-ip-to-eip )をご参照ください。
#### シナリオ
Linuxスクリプトは、次のシナリオに適用できます。プライベートIPとパブリックIPの両方がプライマリENI（eth0）にバインドされ、パブリックネットワークアドレスがパブリックIPを介してアクセスされ、プライベートネットワークアドレスがプライベートIPを介してアクセスされます。

#### 手順1： EIP直通スクリプトをダウンロードする
EIP直通モードを有効にするプロセスを開始すると、ネットワークの中断を引き起こす可能性があります。そのため、事前にEIP直通用のスクリプトをダウンロードしてCVMにアップロードする必要があります。次のいずれかの方法でスクリプトを取得できます。
- **方式1：EIP直通スクリプトをアップロードする**
 1.EIP直通の構成スクリプトをダウンロードします。
 2. Linux スクリプトをローカルにダウンロードした後、EIP直通が必要なCVMにアップロードします。
- **方法2：コマンドを直接使用する**
CVMにログインし、CVMで次のコマンドを実行してスクリプトをダウンロードします。
```
wget https://network-data-1255486055.cos.ap-guangzhou.myqcloud.com/eip_direct.sh
```

#### 手順2：EIP直通スクリプトを実行する
1. EIP直通が必要なCVMにログインします。
2. EIP直通スクリプトを実行します。詳細手順：
 1. 次のコマンドを実行して、実行権限を追加します。
```
chmod +x eip_direct.sh
```
 2. 次のコマンドを実行して、スクリプトを実行します。
```
./eip_direct.sh install XX.XX.XX.XX
```
そのうち、XX.XX.XX.XXはEIPアドレスで、オプションです。入力しない場合、`./eip_direct.sh install`を直接実行します。

#### 手順3：EIP直通を有効にする
1. [EIPコンソール](https://console.cloud.tencent.com/cvm/eip?rid=1)にログインします。
2. ターゲットEIPを見つけ、右側の操作バーで【More】＞【 Direct connection】をクリックします。


### Windows CVMでEIP直通を構成する
>
>- WindowsでEIP直通を使用するには、プライベートIPとパブリックIPそれぞれ1枚のENIが必要です。パブリックIPをプライマリENIにバインドし、プライベートIPをセカンダリENIにバインドします。
- WindowsでEIPを構成するプロセスに、インターネットに接続できない場合があります。この場合、[ VNCを介してWindowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32496)することをお勧めします。
- プライマリENIにバインドされているパブリックIPがEIPでない場合は、先にパブリックIPアドレスをEIPに変換する必要があります。詳細については、[パブリックIPアドレスのEIPアドレスへの変換]( https://intl.cloud.tencent.com/document/product/213/16586#converting-public-ip-to-eip)をご参照ください。

#### シナリオ
Windowsスクリプトは、次のシナリオに適用できます。パブリックネットワークトラフィックはプライマリENIを通過し、プライベートネットワークトラフィックはセカンダリENIを通過します。

#### 手順1： EIP直通スクリプトをダウンロードする<span id="step1" />
EIP直通モードを有効にするプロセスを開始すると、ネットワークの中断を引き起こす可能性があります。そのため、事前にEIP直通用のスクリプトをダウンロードしてCVMにアップロードする必要があります。
CVMのブラウザで次のリンクを開いて、EIP直通スクリプトのダウンロードを行ってください。
```
https://windows-1254277469.cos.ap-guangzhou.myqcloud.com/eip_windows_direct.bat
```

#### 手順2：セカンダリENIを構成する
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/overview)にログインします。
2. インスタンスリストで、構成するCVM IDをクリックし、詳細ページに進みます。
3. 【 ENI 】タブを選択し、【 Bind ENI】をクリックし、プライマリENIと同じサブネットのENIを新規作成します。
![](https://main.qcloudimg.com/raw/2da530f15e824ff99858f08397687cf6.png)
4. ポップアップボックスで、【Create and Bind an ENI】を選択し、関連情報を入力し、【Assign IP】のセクションで【Automatic Assignment】を選択し、【OK】をクリックします。
![](https://main.qcloudimg.com/raw/cb6fe49d3bbefd792355ade6e62f29f3.png)

#### 手順3：プライマリENIのEIP直通を構成する
1. [EIPコンソール](https://console.cloud.tencent.com/cvm/eip?rid=1)にログインします。
2. プライマリENIにバインドされているEIPを見つけて、右側の操作バーで【More】＞【Direct Connection】をクリックします。

#### 手順4： CVMでIPを構成する
1. CVMにログインします。この操作により、パブリックネットワークが切断される可能性があります。したがって、[VNCを介してWindowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32496)する必要があります。
2. OSのインターフェースで、左下の<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px;width:25px">を選択し、<img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: -3px 0px;">をクリックして、「Windows PowerShell」ウィンドウを開き、`firewall.cpl ` を入力してEnterキーを押すと、「Windowsファイアウォール」ページを開きます。
3. 画面左側の項目から【Windowsファイアウォールの有効化または無効化】をクリックします。「設定のカスタマイズ」画面が表示されます。
![](https://main.qcloudimg.com/raw/e6d6a44be911ec5f60a6205b6f47a2c7.png)
4. 「プライベートネットワークの設定」と「パブリックネットワークの設定」のいずれか、もしくは両方で【Windows ファイアウォールを無効にする（推奨されません）】を選択し、【OK】をクリックします。
![](https://main.qcloudimg.com/raw/cdb7703dec781e98101f7f3fd7ecf71f.png)
5. [手順1](#step1)でダウンロードしたスクリプトをダブルクリックして実行し、パブリックIPアドレスを入力して、Enterキーを2回押します。 
6. 「Windows PowerShell」ウィンドウで`ipconfig`を入力してEnterキーを押すと、プライマリENI上のIPv4アドレスがパブリックネットワークアドレスに変更されていることが分かります。

> EIP直通が有効になっている場合、プライマリENIに再度プライベートIPを構成しないでください。構成した場合、CVMはパブリックネットワークにアクセスできなくなります。

