[](id:que1) 
### メール送信を簡単にテストするにはどうすればよいですか。
お客様はご自身のアカウントを使用してテストを行うことができ、1000通の無料利用枠をご用意しております。プッシュ型メールは現在、テスト用アカウントを提供していません。

[](id:que5) 
### 最初から直ちに大量のメールを送信することはできますか。
最初から直ちに大量のメールを送信することはできません。メールの送信量は日々漸増する必要があり、一足飛びに目標の規模に達することはできません。Eメールサービスプロバイダ(ISP)から高いレピュテーションを得るためには、メール送信を開始する前に自動warm upが必要です。一斉送信モードから、デフォルトでwarm up標準版ルールに進みます。[製品の機能](https://intl.cloud.tencent.com/document/product/1084/43285)をご参照ください。

[](id:que6) 
### warm upとは何ですか。
warm upとは、IPのウォームアップのことです。メールサービスプロバイダは通常、1IPあたりに送信できる1日の総送信量には上限があり、高トラフィック送信のニーズを満たすには、メール送信量を徐々に増やしていく必要があります。

[](id:que7) 
一斉送信モードから、デフォルトでwarm up標準版ルールに進みます。製品のバックエンドが一連のポリシーに従ってその日の送信クォータを自動的に割り当てることで、すべてのプロセスが人手を介さずに自動的に完了します。その日の最大受信量を超えると、自動的に送信は中断され、残りの未送信メールはキューキャッシュに入れられ、現在時刻から24時間後に自動的に送信されます。標準版warm up計画は次のとおりです。
<table style="width: 200px;">
   <tr>
      <th width="0px" style="text-align:center">時間</td>
      <th width="0px" style="text-align:center">送信量/日</td>
   </tr>
	<tr>
		<td style="text-align:center"style="text-align:center">1日目</td>
		<td style="text-align:center">100</td>
	</tr>
	<tr>
		<td style="text-align:center">2日目</td>
		<td style="text-align:center"sdval="200" >200</td>
	</tr>
	<tr>
		<td style="text-align:center">3日目</td>
		<td style="text-align:center"sdval="500" >500</td>
	</tr>
	<tr>
		<td style="text-align:center">4日目</td>
		<td style="text-align:center"sdval="1000" >1000</td>
	</tr>
	<tr>
		<td style="text-align:center">5日目</td>
		<td style="text-align:center"sdval="2000" >2000</td>
	</tr>
	<tr>
		<td style="text-align:center">6日目</td>
		<td style="text-align:center"sdval="5000" >5000</td>
	</tr>
	<tr>
		<td style="text-align:center">7日目</td>
		<td style="text-align:center"sdval="10000" >10000</td>
	</tr>
	<tr>
		<td style="text-align:center">8日目</td>
		<td style="text-align:center"sdval="20000" >20000</td>
	</tr>
	<tr>
		<td style="text-align:center">9日目</td>
		<td style="text-align:center"sdval="30000" >30000</td>
	</tr>
	<tr>
		<td style="text-align:center">10日目</td>
		<td style="text-align:center"sdval="40000" >40000</td>
	</tr>
	<tr>
		<td style="text-align:center">11日目</td>
		<td style="text-align:center"sdval="60000" >60000</td>
	</tr>
	<tr>
		<td style="text-align:center">12日目</td>
		<td style="text-align:center"sdval="80000" >80000</td>
	</tr>
	<tr>
		<td style="text-align:center">13日目</td>
		<td style="text-align:center"sdval="100000" >100000</td>
	</tr>
	<tr>
		<td style="text-align:center">14日目</td>
		<td style="text-align:center"sdval="120000" >120000</td>
	</tr>
	<tr>
		<td style="text-align:center">15日目</td>
		<td style="text-align:center"sdval="150000" >150000</td>
	</tr>
	<tr>
		<td style="text-align:center">16日目</td>
		<td style="text-align:center"sdval="200000" >200000</td>
	</tr>
	<tr>
		<td style="text-align:center">17日目</td>
		<td style="text-align:center"sdval="400000" >400000</td>
	</tr>
	<tr>
		<td style="text-align:center">18日目</td>
		<td style="text-align:center"sdval="600000" >600000</td>
	</tr>
	<tr>
		<td style="text-align:center">19日目</td>
		<td style="text-align:center"sdval="800000" >800000</td>
	</tr>
		<tr>
		<td style="text-align:center">20日目</td>
		<td style="text-align:center"sdval="800000" >1000000</td>
	</tr>
</table>

カスタマイズルール：

高品質なメールのため、標準版warm up計画がお客様のご要望に合わない場合は、パーソナライズされたカスタムwarm up計画を作成することもできますので、専任のビジネスマネージャーにお申し付けください。
