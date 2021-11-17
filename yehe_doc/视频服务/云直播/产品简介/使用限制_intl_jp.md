CSSサービスをご利用される前に、サービスの使用制限事項を知っておく必要があります。

<table>
<tr><th>制限項目</th><th>説明</th></tr>
<tr>
<td>CSSドメイン名</td>
<td><ul style="margin:0">
 <li>デフォルトで、各アカウントにつき複数の再生およびプッシュドメイン名を作成できます。ドメイン名のアクセラレーションリージョンが中国大陸エリアまたはグローバルエリアの場合は、ドメイン名が工信部でICP登録され、かつ現在のICP登録情報が正常に使用できるものである必要があります。</li>
    <li>各アカウントにつき管理できるドメイン名はデフォルトで100個に制限されています。業務の規模が大きい場合は、<a href="https://console.cloud.tencent.com/workorder/category">チケットを提出</a>してドメイン名の数量上限の引き上げを申請することができます。</li>
    <li>ドメイン名の長さ設定は45文字以下にすることをお勧めします。<strong>45文字</strong>を超える場合は、<a href="https://console.cloud.tencent.com/workorder/category">チケットを提出</a>して対策をご相談いただく必要があります。</li>
<li>CSSで管理するドメイン名が正常にCSSプッシュ/再生を行えるようにするには、ドメイン名解決を完了する必要があります。具体的な内容は、<a href="https://intl.cloud.tencent.com/document/product/267/31057">ドメイン名CNAME設定</a>をご参照ください。</li></ul></td>
</tr><tr>
<td>CSSプッシュ</td>
<td>CSSサービスは、プッシュのビットレートを制限せず、一般的な解像度と対応するビットレートをサポートします。プッシュのラグを回避するために、ビットレートが4Mbpsを超えないようにすることをお勧めします。</td>
</tr><tr>
<td>CSS再生</td>
<td><ul style="margin:0">
	<li>ライブストリーミングアドレスのStreamNameとプッシュアドレスのStreamNameが一致する場合のみ、対応するストリームを再生できます。</li>
	<li>ライブストリーミング再生の視聴者数は制限されません。帯域幅の上限設定をサポートしています。</li>
	<li/>大規模で突発的な増加がある場合は、3営業日前に<a href="https://console.cloud.tencent.com/workorder/category">チケットを提出</a>するか、またはビジネスマネージャーに連絡して対策をご相談ください。大規模で突発的な増加には次の2つのシナリオがあります。<ul style="margin:0">
		<li/>突発的な1日のピーク帯域幅が200Gbpsを超え、かつ突発的な増加が通常の日のピーク値の200%となるシナリオ。
		<li/>1日のピーク帯域幅の突発的な増加が500Gbpsを超えるシナリオ。
	</ul>
</ul></td>
</tr><tr>
<td>テンプレート設定</td>
<td>テンプレートの関連付け設定の完了後、約5分～10分後に有効になります。</td>
</tr><tr>
<td>日次決済課金方式の切り替え</td>
<td>日次決済課金はトラフィック/帯域幅ピーク値に応じた2種類の課金方式間の切り替えをサポートしています。1日1回に限り切り替えができます（変更完了後、翌日に有効化）。</td>
</tr><tr>
<td>プッシュサポートプロトコル</td>
<td>RTMP、SRTプロトコルをサポートしています。詳しい説明については、<a href="https://intl.cloud.tencent.com/document/product/267/7968">よくあるご質問</a>をご参照ください。</td>
</tr><tr>
<td>再生サポートプロトコル</td>
<td><ul style="margin:0">
	<li>標準ライブストリーミングRTMP、FLVおよびHLS再生プロトコルをサポートしています。 詳細な説明は<a href="https://intl.cloud.tencent.com/document/product/267/7968">よくあるご質問</a>をご参照ください。</li>
	<li>ライブイベントストリーミングはWebRTC再生プロトコルをサポートしています。</li>
</ul></td>
</tr><tr>
<td>Live Video Caster</td>
<td><ul style="margin:0">
	<li>各アカウントにつき<b>3</b>個のLive Video Casterインスタンスを作成することができ、Live Video Casterインスタンスを削除すると新たに追加することができます。複数のLive Video Casterが必要な場合は、<a href="https://console.cloud.tencent.com/workorder/category">チケットを提出</a> して申請してください。</li>
	<li>VODの再生リスト入力は、最大で5個のVODファイルをサポートしています。</li>
	<li>サードパーティへのプッシュ転送は、最大3チャネルまでサポートしています。そのうち1チャネルはデフォルトでは現在のTencent Cloud CSSアカウントへの転送となり、他の2チャネルはサードパーティへの転送となります。</li>
</ul></td>
</tr></table>


