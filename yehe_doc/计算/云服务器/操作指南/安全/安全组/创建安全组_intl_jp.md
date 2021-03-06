## シナリオ
セキュリティグループはCVMインスタンスの仮想ファイアウォールであり、各CVMインスタンスは少なくとも1つのセキュリティグループに関連付ける必要があります。CVMインスタンスを作成する際に、セキュリティグループを作成したことがない場合には、Tencent Cloudは、デフォルトのセキュリティグループを作成するための「**すべてのポートを開放する**」と「**22、80、443、3389ポートとICMPプロトコル**を開放する」の2つのテンプレートが用意されています。詳細については、[セキュリティグループの概要](https://intl.cloud.tencent.com/document/product/213/12452)をご参照ください。

CVMインスタンスをデフォルトのセキュリティグループに設定したくない場合には、このドキュメントの説明に従って、自分でセキュリティグループを作成することもできます。このドキュメントでは、CVMコンソールでセキュリティグループを作成する方法について説明します。


## 操作手順

1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. 左側のナビゲーションバーで【[セキュリティグループ](https://console.cloud.tencent.com/cvm/securitygroup)】をクリックすると、セキュリティグループ管理ページに進みます。
3. セキュリティグループ管理ページで【リージョン】を選択し、【+New】をクリックします。
4. ポップアップダイアログボックスで、次の設定を完了します。次図に示す通り：
![](https://main.qcloudimg.com/raw/575b2a589a58aef436bc5208facf4614.png)
 - テンプレート:セキュリティグループ内のCVMインスタンスに配備する必要があるサービスに応じて、適切なテンプレートを選択します。以下の表に示すとおりです。
<table>
	<tr><th>テンプレート</th><th>説明</th><th>ケース</th></tr>
	<tr><td>すべてのポートを開放</td><td>デフォルトではすべてのポートをパブリックネットワークとプライベートネットワークに開放し、セキュリティ上の問題が発生する可能性があります。</td><td>-</td></tr>
	<tr><td>22、80、443、3389ポートとICMPプロトコルを開放</td><td>デフォルトでは22、80、443、3389ポートとICMPプロトコルを開放し、プライベートネットワークはすべて開放されています。</td><td>セキュリティグループ内のインスタンスはWebサービスを配備する必要があります。</td></tr>
	<tr><td>カスタマイズ</td><td>セキュリティグループの作成が完了した後、必要に応じてセキュリティグループルールを自ら追加します。操作の詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/34272">セキュリティグループルールの追加</a>をご参照ください。</td><td>-</rd></tr>
</table>
 - 名前：セキュリティグループの名前。
 - プロジェクト：デフォルトで「デフォルトプロジェクト」が選択されていますが、後で管理しやすいようにその他のプロジェクトを指定することができます。
 - 備考：後で管理しやすいようにセキュリティグループを簡単に記述します。
5. 【OK】をクリックして、セキュリティグループの作成を完了します。
セキュリティグループを新規作成する際にテンプレートの「カスタマイズ」を選択した場合には、作成が完了したら、【Add rules now】をクリックして、[セキュリティグループルールの追加](https://intl.cloud.tencent.com/document/product/213/34272)を実行します。
