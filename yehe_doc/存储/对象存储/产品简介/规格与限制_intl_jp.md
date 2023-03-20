<table>
    <tr>
        <th>カテゴリー</th> 
        <th>仕様と制限</th> 
    			<th>詳細説明</th> 
   </tr>
    <tr>
        <td>QPS</td>
    			<td>制限</td>
    			<td><ul  style="margin: 0;"><li>読み取り/書き込みタイプリクエスト：中国大陸パブリッククラウドリージョンではデフォルトで各バケットにつき30000QPSを専有し、その他のリージョンでは各バケットにつき3000QPSを専有します。</li>
					<li>バケット内オブジェクトリストアップ/過去バージョン/現在実行中のマルチパートアップロードタスク：全リージョンの各バケットにつきデフォルトで1000QPSとなります。</li>
                    <li>バケット作成/バケット削除/バケットリストアップ：全リージョンの各APPIDにつきデフォルトで50QPSとなります。</li>					
                    <li> データ取得リクエスト：全リージョンの各バケットにつきデフォルトで100QPSとなります。</li>
                    <li> 1回のみのリスト作成タスクリクエスト：全リージョンの各バケットにつきデフォルトで1QPSとなります。</li>
					<li>単一ファイルアップロード/削除/Listホットスポット頻度制御：50QPS。</li>
					<li>単一ファイルダウンロードホットスポット頻度制御：1000QPS。
<br>これより高いQPSが必要な場合は、<a href="https://intl.cloud.tencent.com/document/product/436/13653">リクエスト速度およびパフォーマンスの最適化</a>をご参照ください。</li></ul></td>
    </tr>
		    <tr>
        <td>帯域幅</td>
    			<td>制限</td>
					<td>中国大陸パブリッククラウドリージョンでの1バケットのデフォルトの帯域幅は、アップストリーム・ダウンストリーム共有で15Gbit/s、その他のリージョンではアップストリーム・ダウンストリーム共有で10Gbit/sとなります。帯域幅がこの閾値に達すると、リクエストによってトラフィックコントロールがトリガーされます。これ以上の帯域幅が必要な場合は、<a href="https://console.cloud.tencent.com/workorder/category">アフターサービスエンジニア</a>までご連絡ください。</td>	
    </tr>
    	<tr>
        <td rowspan="5">ストレージタイプ</td>
    			<td>標準ストレージ（マルチAZ）/標準ストレージの制限</td>
    			<td>課金制限：<br>保存期間、ストレージユニットに制限はありません。<br>標準ストレージ料金の詳細については、<a href="https://buy.cloud.tencent.com/price/cos">製品価格</a>をご参照ください。</td>
    </tr>
    	 <tr>
        <td>低頻度ストレージ（マルチAZ）/低頻度ストレージの制限</td>
    	<td>課金制限：<ul  style="margin: 0;"><li>保存期間が30日未満の場合は、30日として計算します。</li><li>ストレージユニットが64KB未満の場合は64KBとして計算し、64KB以上の場合は実際のサイズに基づいて計算します。<br>低頻度ストレージ料金の詳細については、<a href="https://buy.cloud.tencent.com/price/cos">製品価格</a>をご参照ください。</li></ul></td>
    </tr>
    	<tr>
        <td>INTELLIGENT_TIERINGストレージ（マルチAZ）/INTELLIGENT_TIERINGストレージの制限</td>
    	<td><li>課金制限：<br>64KB未満のオブジェクトは引き続き高頻度アクセスレイヤーに保存されます。単一のストレージファイルのサイズにかかわらず、実際のデータサイズに基づいて計算します。<br>INTELLIGENT_TIERINGストレージ料金の詳細については、
<a href="https://buy.cloud.tencent.com/price/cos">製品価格</a>をご参照ください。</td>
    </tr>
    	 <tr>
        <td>アーカイブストレージの制限</td>
    			<td>課金制限：<ul  style="margin: 0;"><li>保存期間が90日未満の場合は、90日として計算します。</li>
					<li>ストレージユニットが64KB未満の場合は64KBとして計算し、64KB以上の場合は実際のサイズに基づいて計算します。<br>アーカイブストレージ料金の詳細については、<a href="https://buy.cloud.tencent.com/price/cos">製品価格</a>をご参照ください。</li></ul></td>
    </tr>
    	 <tr>
        <td>ディープアーカイブストレージの制限</td>
    			<td>課金制限：<ul  style="margin: 0;"><li>保存期間が180日未満の場合は、180日として計算します。</li>
					<li>ストレージユニットが64KB未満の場合は64KBとして計算し、64KB以上の場合は実際のサイズに基づいて計算します。<br>ディープアーカイブストレージ料金の詳細については、<a href="https://buy.cloud.tencent.com/price/cos">製品価格</a>をご参照ください。</li></ul></td>
    </tr>
     <tr>
        <td rowspan="4">バケット</td>
    			<td>制限</td>
    			<td><ul  style="margin: 0;"><li>バケットはいったん作成すると、名前および所在リージョンの変更はできません。</li>
					<li>同一のユーザーアカウントにおけるバケット名は固有であり、リネームもサポートしていません。</li>
					<li>名前は、始まりまたは終わりを「-」とすることはできず、小文字アルファベット、数字[a-z,0-9]、ハイフン「-」およびそれらの組み合わせのみサポートしています。バケット名の最大文字数は<a href="https://intl.cloud.tencent.com/document/product/436/6224">リージョンの略称</a>およびAPPIDの文字数の影響により、組み合わせたリクエストドメイン名全体の文字数合計が最大60文字までとなります。</li></ul></td>
     </tr>
    	 <tr>
    			<td>バケット数</td>
    			<td>各ルートアカウントにつき最大200個までです（デフォルト）。</td>
    		</tr>
				<tr>
    			<td>オブジェクト数</td>
    			<td>各バケット内のオブジェクト数に制限はありません。</td>
    		</tr>
				<tr>
    			<td>バケットタグ</td>
    			<td>同じバケット内のタグ数は最大50個までです。タグキーは重複できません。</td>
    		</tr>
    		<tr>
    			<td rowspan="5">オブジェクト</td>
    			<td>制限</td>
					<td >オブジェクトキーの長さは1～850Bまでです。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/13324">オブジェクトの概要</a>をご参照ください。</td>
    		</tr>
    			<tr>
    			<td>アップロード</td>
    			<td><ul  style="margin: 0;"><li>コンソールによってアップロードできる単一のオブジェクトは最大512GBまでです。</li>
					<li> API/SDKによってアップロードできる単一のオブジェクトは最大48.82TB (50,000GB )までです。
						<br>アップロードインターフェースの仕様：
						<ul  style="margin: 0;"><li>シンプルアップロード：単一のオブジェクトは最大5GBまでです。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/14113">シンプルアップロード</a>をご参照ください。</li>
						<li>マルチパートアップロード：単一のオブジェクトは最大48.82TBまでです。パートのサイズは1MB～5GBで、最終のパートは1MB未満とすることができます。パート数は1～10000です。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/14112">マルチパートアップロード</a>をご参照ください。</li></ul>
					</li>
					<li> 現在はマルチAZ設定を有効化したバケットには、標準ストレージ（マルチAZ）、低頻度ストレージ（マルチAZ）などの、マルチAZの特性を持つストレージタイプをアップロードすることができます。バケットが同時にINTELLIGENT_TIERINGストレージ設定を有効化している場合は、INTELLIGENT_TIERINGストレージ（マルチAZ）タイプもアップロードできます。</li>
					<li>現時点ではバケットがINTELLIGENT_TIERINGストレージ設定を有効にしている場合にのみ、INTELLIGENT_TIERINGストレージタイプのオブジェクトをアップロードすることができます。異なるストレージレイヤー間でのオブジェクトの切り替えは、INTELLIGENT_TIERINGストレージ設定内のパラメータによって決定されます。</li></ul></td>
    		</tr>
    		<tr>
    			<td >コピー</td>
    			<td ><ul  style="margin: 0;"><li>単一アカウントの同一リージョンまたはリージョン間でのオブジェクトのコピーをサポートしています。</li>
					<li>同一リージョン内でのオブジェクトのコピーは無料です。リージョン間でオブジェクトのコピーを行う場合はトラフィック料金が発生します。詳細については、<a href="https://buy.cloud.tencent.com/price/cos">料金説明</a>のトラフィック料金に関する情報をご参照ください。 </li>
					<li>コピーインターフェースの仕様：
						<ul  style="margin: 0;"><li>シンプルコピー：コピーできる単一のオブジェクトは最大5GBまでです。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/14117">シンプルコピー</a>をご参照ください。</li>
						<li>5GBを超える場合はマルチパートコピーを用いる必要があります。コピーできる単一のオブジェクトは最大48.82TBまでです。詳細については、<a href="https://intl.cloud.tencent.com/document/product/436/14118">マルチパートコピー</a>をご参照ください。</li></ul>
					</li>
					<li>マルチAZ設定を有効にしているバケットでは、マルチAZストレージタイプをシングルAZストレージタイプにコピーすることはサポートされていません。</li>
					<li>現時点では、標準ストレージ、低頻度ストレージ、INTELLIGENT_TIERINGストレージタイプをINTELLIGENT_TIERINGストレージタイプとしてコピーすることはサポートしていません。</li></ul></td>
    		</tr>
    		<tr>
    			<td>一括削除</td>
    			<td>API、SDKによって一括削除を開始します。1回に最大1000個のオブジェクトを削除できます。</td>
    		</tr>
				<tr>
    			<td>オブジェクトタグ</td>
    			<td>同一のオブジェクトに最大10個までオブジェクトタグをつけることができます。また、タグは重複できません。</td>
    		</tr>
    		 <tr>
    			<td >アクセスポリシー</td>
    			<td >ルール数</td>
    			<td >各ルートアカウント（すなわち同一のAPPID）の、バケットACLルールの数は最大1000個までです。</td>
    		</tr>
    		<tr>
    			<td rowspan="3">ライフサイクル</td>
    			<td>ルール数</td>
    			<td >各バケットにつき最大1000個までです。</td>
    		</tr>
    		<tr>
    			<td>ストレージタイプの切り替え</td>
    			<td >標準ストレージから低頻度ストレージ：最短1日。<br>標準/低頻度ストレージからアーカイブストレージまたはディープアーカイブストレージ：最短1日。<br>注意：<br>1. 標準ストレージ（マルチAZ）および低頻度ストレージ（マルチAZ）の低頻度ストレージ、アーカイブストレージおよびディープアーカイブストレージタイプへの移行は現時点ではサポートされていません。<br>2. ライフサイクルの切り替え操作は64KB未満のオブジェクトに対しては実行できません。</td>
    		</tr>
    		 <tr>
    			<td>期限切れによる削除</td>
    			<td >標準/低頻度/アーカイブストレージの期限切れによる削除：最短1日。</td>
    		</tr>         
    		<tr>
    			<td colspan="2">SDKの種類</td>
    			<td >12種類：Android、C、C++、.NET、Go、iOS、Java、JavaScript、Node.js、PHP、Python、ミニプログラムSDK。</td>
    		</tr>        
    		<tr>
    			<td colspan="2">API予約フィールド</td>
    			<td >APIドキュメントにあるインターフェースパラメータはすべてCOSの予約フィールドであり、次のパラメータが含まれます。<br>acl、uploads、policy、cors、delete、versions、location、referer、lifecycle、versioning、notification、replication、website、logging、tagging、accelerate、domain、inventory、origin、object-lock、live、encryption、intelligenttiering、symlinkなどがあります。</br></td>
    		</tr>
</table>


