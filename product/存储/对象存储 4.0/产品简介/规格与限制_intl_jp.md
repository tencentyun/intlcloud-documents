<table>
    <tr>
        <th>分類</th> 
        <th>仕様と制限</th> 
    			<th>詳細説明</th> 
   </tr>
    <tr>
        <td>QPS</td>
    			<td>制限</td>
    			<td>各アカウントはデフォルトで1200qpsです。その以上のQPSを必要とする場合、<a href="/document/product/436/13653">リクエスト速度とパフォーマンス最適化</a>を参照してください </td>
    </tr>
    	 <tr>
        <td rowspan="3">ストレージタイプ</td>
    			<td>スタンダートストレージ制限</td>
    			<td>課金制限：<br>ストレージ時間、ストレージユニット無制限<br>スタンダートストレージ課金の詳細について、<a href="https://cloud.tencent.com/document/product/436/6239">費用説明</a></td>を参照してください
    </tr>
    	 <tr>
        <td>低頻度ストレージ制限</td>
    			<td>課金制限：<br>ストレージ時間が30日未満の場合、30日として計算します<br>ストレージユニットが64KB未満の場合、64KBとして計算します<br>低頻度ストレージ課金の詳細について、<a href="https://cloud.tencent.com/document/product/436/6239">費用説明</a></td>を参照してください
    </tr>
    	 <tr>
        <td>CAS制限</td>
    			<td>課金制限：<br>ストレージ時間が90日未満の場合、90日として計算します<br>ストレージユニットが48KB未満の場合、48KBとして計算します<br>CAS課金の詳細について、<a href="https://cloud.tencent.com/document/product/436/6239">費用説明</a></td>を参照してください				
    </tr>
     <tr>
        <td rowspan="3">バケット</td>
    			<td>制限</td>
    			<td>1. バケットを作成すると、名前と所在地域を変更できません<br>2. 同じユーザーのアカウントのすべてのバケット名が唯一で名前を変更できません<br>3. 名前は小文字英数字「a-z、0-9」、ハイフン「-」およびそれらの組合せ、1～40文字のみをサポートします</td>
     </tr>
    	 <tr>
    			<td> バケット数</td>
    			<td>各アカウントは最大200個（デフォルト）です</td>
    		</tr>
    			<td> オブジェクト数</td>
    			<td> 各バケットのオブジェクト数は制限ありません</td>
    		<tr>
    			<td rowspan="4">オブジェクト</td>
    			<td>制限</td>
					<td >オブジェクトのキーの長さは1～850Bで、詳細について、<a href="https://cloud.tencent.com/document/product/436/13324">オブジェクト概要</a></td>を参照してください
    		</tr>
    			<tr>
    			<td>アップロード</td>
    			<td>1.コンソールは単一オブジェクトを最大512GBまでアップロードできます<br>2. API/SDKは単一オブジェクトを最大48.82TB（50,000GB）までアップロードできます<br>アップロードAPI仕様：<br>&nbsp;&nbsp;a）簡易アップロード：単一オブジェクト最大5GB。詳細について、次を参照してください<a href="https://cloud.tencent.com/document/product/436/14113">簡易アップロード</a> <br>&nbsp;&nbsp;b）分割アップロード：単一オブジェクト最大48.82TB、パートの大きさ1MB~5GB、最後のパートは1MB未満可能です。パート数は1~10000です。詳細について、<a href="https://cloud.tencent.com/document/product/436/14112">分割アップロード</a></td>を参照してください
    		</tr>
    		<tr>
    			<td >レプリケーション</td>
    			<td >1. 同じ地域/地域間のオブジェクトレプリケーションをサポートします<br>2. 同じ地域のオブジェクトレプリケーションは無料で、地域間のオブジェクトレプリケーションはトラフィック費用が発生します。詳細について、<a href="https://cloud.tencent.com/document/product/436/6239">費用説明</a> 内トラフィック費用情報を参照してください  <br>3. レプリケーションAPI仕様：<br>&nbsp;&nbsp;a) 簡易レプリケーション：単一オブジェクトのレプリケーション最大5GB。詳細について、次を参照してください<a href="https://cloud.tencent.com/document/product/436/14117">簡易レプリケーション</a><br>&nbsp;&nbsp;b) が5GB以上の場合、分割レプリケーションを使用します。単一オブジェクトのレプリケーション最大48.82TB。詳細について、<a href="https://cloud.tencent.com/document/product/436/14118">分割レプリケーション</a></td>を参照してください
    		</tr>
    		<tr>
    			<td>一括削除</td>
    			<td>API、SDKで一括削除を実行する場合、1回に最大1000個のオブジェクトを削除できます</td>
    		</tr>
    		 <tr>
    			<td >アクセスポリシー</td>
    			<td >ルール数</td>
    			<td >各アカウント、オブジェクトとバケットのACL+バケットのPolicyの和は、最大1000件です</td>
    		</tr>
    		<tr>
    			<td rowspan="3">ライフサイクル</td>
    			<td>ルール数</td>
    			<td >各バケットは最大1000件です</td>
    		</tr>
    		<tr>
    			<td >ストレージタイプの変換</td>
    			<td >スタンダートから低頻度へ：最小1日<br>スタンダート／低頻度からアーカイブへ：最小1日 </td>
    		</tr>
    		 <tr>
    			<td >期限切れ削除</td>
    			<td >スタンダート／低頻度／ファイリング期限切れ削除：最小1日</td>
    		</tr>         
    		<tr>
    			<td colspan="2">SDK言語</td>
    			<td >10種類：<br>Andriod/C/C++/Go/iOS/Java/JavaScript/Node.js/PHP/Python</td>
    </tr>
</table>

