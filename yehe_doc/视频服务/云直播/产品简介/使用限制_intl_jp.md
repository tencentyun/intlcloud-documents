CSSサービスをご利用される前に、サービスの使用制限事項を知っておく必要があります。

<table>
<tr><th>制限項目</th><th>説明</th></tr>
<tr>
<td>CSSドメイン名</td>
<td><ul style="margin:0">
 <li>デフォルトでは各アカウントに複数の再生およびプッシュドメイン名を作成することができます。中国本土（大陸）で使用するドメイン名は必ず中国国家工業情報化部にICP登録を行ったものでなければならず、かつ現在のICP登録情報が正常に使用できなければなりません。</li><li>各アカウントにつき管理できるドメイン名はデフォルトで100個に制限されています。業務の規模が大きい場合は、<a href="https://console.cloud.tencent.com/workorder/category">チケットを提出</a>してドメイン名の数量上限の引き上げを申請することができます。</li><li>ドメイン名は30桁を超えない長さに設定することをお勧めします。<strong>30桁</strong>を超えている場合は、<a href="https://console.cloud.tencent.com/workorder/category">チケットを提出</a>して解決する必要があります。</li>
<li>CSSの管理するドメイン名が正常にCSSプッシュ/再生を行えるようにするには、ドメイン名解決を完了する必要があります。具体的には<a href="https://intl.cloud.tencent.com/document/product/267/31057">ドメイン名CNAME設定</a>をご参照ください。</li></td>
</tr><tr>
<td>CSSプッシュ</td>
<td>CSSサービスはプッシュビットレートを制限しておらず、一般的な解像度および対応するビットレートをサポートしています。プッシュラグが発生しないよう、ビットレートは4Mbps以下にすることをお勧めします。</td>
</tr><tr>
<td>CSS再生</td>
<td><ul style="margin:0">
<li>ライブストリーミングアドレスのStreamNameとプッシュアドレスのStreamNameが一致する場合のみ、対応するストリームを再生できます。</li><li>CSS再生の視聴者数は制限しておらず、ネットワーク帯域幅の制限の設定をサポートしています。</li></td>
</tr><tr>
<td>テンプレート設定</td>
<td>テンプレートの関連付け設定の完了後、約5分～10分後に有効になります。</td>
</tr><tr>
<td>日次決済課金方式の切り替え</td>
<td>日次決済課金はトラフィック/帯域幅ピーク値に応じた2種類の課金方式間の切り替えをサポートしています。1日1回に限り切り替えができます（変更完了後、翌日に有効化）。</td>
</tr><tr>
<td>プッシュサポートプロトコル</td>
<td>RTMP、SRT出力プロトコルをサポートしています。 詳細な説明は<a href="https://intl.cloud.tencent.com/document/product/267/7968">よくあるご質問</a>をご参照ください。</td>
</tr><tr>
<td>再生サポートプロトコル</td>
<td><ul style="margin:0">
<li>標準ライブストリーミングRTMP、FLVおよびHLS再生プロトコルをサポートしています。 詳細な説明は<a href="https://intl.cloud.tencent.com/document/product/267/7968">よくあるご質問</a>をご参照ください。</li>
<li>ライブイベントストリーミングはwebRTC再生プロトコルをサポートしています。</li>
<li>プル再生のサポートする帯域幅は最大200Gであり、これ以上が必要な場合は<a href="https://console.cloud.tencent.com/workorder/category">チケットを提出</a>するか、またはビジネスマネージャーにご連絡いただき、解決する必要があります。</li></td>
</tr><tr>
<td>Live Video Caster</td>
<td><ul style="margin:0">
<li>各アカウントにつき<b>3</b>個のLive Video Casterインスタンスを作成することができ、Live Video Casterインスタンスを削除すると新たに追加することができます。複数のLive Video Casterが必要な場合は、<a href="https://console.cloud.tencent.com/workorder/category">チケットを提出</a> して申請してください。</li>
<li>VODの再生リスト入力は、最大で5個のVODファイルをサポートしています。</li>
<li>サードパーティへの転送は、最大3チャネルまでサポートされます。そのうち1チャネルはデフォルトでは現在のTencent Cloud CSSアカウントへの転送、その他の2チャネルはサードパーティへの転送となります。</li></td>
</tr></table>
 
