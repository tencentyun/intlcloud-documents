### シャードポリシー
1.範囲パーティションをサポートするシャードメカニズム
2.ユニオンフィールドをサポートするシャードキー。
3.シャードインスタンスにあるすべてのデータセットはシャーディングを使用する必要があります。シャーディングしないデータを個別のレプリカセットインスタンスに配置することをお勧めします。

### 認証メカニズム
SCRAM-SHA-1とMONGODB-CRの両方のメカニズムと完全に互換性があります。

### シャードクラスタコマンドの対応状況
<table class="table-striped">
	<tbody>
		<tr>
		 <th>&nbsp;</th>
			<th>コマンド</th>
			<th>サブコマンド</th>
			<th>対応状況</th>
		</tr>
		<tr>
		  <td rowspan="39">CRUD基本コマンド</td>
			<td rowspan="22">find</td>
			<td>filter</td>
			<td>対応</td>
		</tr>		
		<tr>
			<td>sort</td>
			<td>対応</td>
		</tr>
		<tr>
			<td>projection</td>
			<td>対応</td>
		</tr>
		<tr>
			<td>hint</td>
			<td>対応</td>
		</tr>
		<tr>
			<td>skip</td>
			<td>対応</td>
		</tr>
		<tr>
			<td>limit</td>
			<td>対応</td>
		</tr>
		<tr>
			<td>batchSize</td>
			<td>対応</td>
		</tr>
		<tr>
			<td>singleBatch</td>
			<td>対応</td>
		</tr>
		<tr>
			<td>comment</td>
			<td>対応</td>
		</tr>
		<tr>
			<td>maxScan</td>
			<td>対応</td>
		</tr>
		<tr>
			<td>maxTimeMS</td>
			<td>未対応</td>
		</tr>
		<tr>
			<td>readConcern</td>
			<td>対応</td>
		</tr>
		<tr>
			<td>max</td>
			<td>対応</td>
		</tr>
		<tr>
			<td>min</td>
			<td>対応</td>
		</tr>
		<tr>
			<td>returnKey</td>
			<td>対応</td>
		</tr>
		<tr>
			<td>showRecordId</td>
			<td>対応</td>
		</tr>
		<tr>
			<td>snapshot</td>
			<td>未対応</td>
		</tr>
		<tr>
			<td>tailable</td>
			<td>未対応</td>
		</tr>
		<tr>
			<td>oplogReplay</td>
			<td>未対応</td>
		</tr>
		<tr>
			<td>noCursorTimeout</td>
			<td>対応</td>
		</tr>
		<tr>
			<td>awaitData</td>
			<td>未対応</td>
		</tr>
		<tr>
			<td>allowPartialResults</td>
			<td>未対応</td>
		</tr>		
		<tr>
			<td rowspan="1" >insert</td>
			<td >シャードキーフィールドを入れなければなりません。一括挿入のときにシャードキーが一致しなければなりません</td>
			<td>対応</td>
		</tr>		
		<tr>
			<td rowspan="1">update</td>
			<td >更新フィールドはシャードキーにしてはいけません</td>
			<td>対応</td>
		</tr>		
		<tr>
			<td rowspan="1">delete</td>
			<td></td>
			<td>対応</td>
		</tr>			
		<tr>
			<td rowspan="1">findandmodify</td>
			<td></td>
			<td>対応</td>
		</tr>		
		<tr>
			<td rowspan="1">count</td>
			<td></td>
			<td>対応</td>
		</tr>		
			<tr>
			<td rowspan="1">distinct</td>
			<td>シャードキーを入れなければなりません</td>
			<td>対応</td>
		</tr>
    <tr>
			<td rowspan="1">aggregate</td>
			<td></td>
			<td>未対応</td>
		</tr>		
		 <tr>
			<td rowspan="1">group</td>
			<td></td>
			<td>未対応</td>
		</tr>		
		 <tr>
			<td rowspan="1">mapReduce</td>
			<td></td>
			<td>未対応</td>
		</tr>			
		<tr>
			<td rowspan="1">getmore</td>
			<td></td>
			<td>対応</td>
		</tr>		
		<tr>
			<td rowspan="1">getLastError</td>
			<td></td>
			<td>未対応</td>
		</tr>
		<tr>
			<td rowspan="1">getPrevError</td>
			<td></td>
			<td>未対応</td>
		</tr>
			<tr>
			<td rowspan="1">resetError</td>
			<td></td>
			<td>未対応</td>
		</tr>		
			<tr>
			<td rowspan="1">eval</td>
			<td></td>
			<td>未対応</td>
		</tr>		
			<tr>
			<td rowspan="1">geoNear</td>
			<td></td>
			<td>未対応</td>
		</tr>		
			<tr>
			<td rowspan="1">geoSearch</td>
			<td></td>
			<td>未対応</td>
		</tr>
			<tr>
			<td rowspan="1">parallelCollectionScan</td>
			<td></td>
			<td>未対応</td>
		</tr>
			<tr>
		  <td rowspan="6">診断コマンド</td>
			<td rowspan="1">collStats</td>
			<td></td>
			<td>対応</td>
		</tr>		
			<tr>
			<td rowspan="1">dbstats</td>
			<td></td>
			<td>対応</td>
		</tr>		
			<tr>
			<td rowspan="1">explain</td>
			<td></td>
			<td>対応</td>
		</tr>		
			<tr>
			<td rowspan="1">listDatabases</td>
			<td></td>
			<td>対応</td>
		</tr>		
			<tr>
			<td rowspan="1">serverStatus</td>
			<td></td>
			<td>未対応</td>
		</tr>
			<tr>
			<td rowspan="1">top</td>
			<td></td>
			<td>未対応</td>
		</tr>
			<tr>
		  <td rowspan="2">シャードコマンド</td>
			<td rowspan="1">enableSharding</td>
			<td></td>
			<td>対応</td>
		</tr>		
			<tr>
			<td rowspan="1">shardCollection</td>
			<td></td>
			<td>対応</td>
		</tr>		
		 <tr>
		  <td rowspan="30">管理コマンド</td>
			<td rowspan="1">listCollections</td>
			<td></td>
			<td>対応</td>
		</tr>
			<tr>
			<td rowspan="1">dropDatabase</td>
			<td></td>
			<td>対応</td>
		</tr>
			<tr>
			<td rowspan="1">drop</td>
			<td></td>
			<td>対応</td>
		</tr>
			<tr>
			<td rowspan="1">creareIndexes</td>
			<td></td>
			<td>対応</td>
		</tr>				
			<tr>
			<td rowspan="1">listIndexes</td>
			<td></td>
			<td>対応</td>
		</tr>			
		<tr>
			<td rowspan="1">dropIndexes</td>
			<td></td>
			<td>対応</td>
		</tr>		
			<tr>
			<td rowspan="1">logout</td>
			<td></td>
			<td>対応</td>
		</tr>				
			<tr>
			<td rowspan="1">renameCollection</td>
			<td></td>
			<td>未対応</td>
		</tr>			
			<tr>
			<td rowspan="1">copydb</td>
			<td></td>
			<td>未対応</td>
		</tr>				
			<tr>
			<td rowspan="1">create</td>
			<td></td>
			<td>未対応</td>
		</tr>				
		<tr>
			<td rowspan="1">clone</td>
			<td></td>
			<td>未対応</td>
		</tr>			
		<tr>
			<td rowspan="1">cloneCollection</td>
			<td></td>
			<td>未対応</td>
		</tr>				
		<tr>
			<td rowspan="1">cloneCollectionAsCapped</td>
			<td></td>
			<td>未対応</td>
		</tr>		
		<tr>
			<td rowspan="1">convetToCapped</td>
			<td></td>
			<td>未対応</td>
		</tr>			
		<tr>
			<td rowspan="1">filemd5</td>
			<td></td>
			<td>未対応</td>
		</tr>		
		<tr>
			<td rowspan="1">fsync</td>
			<td></td>
			<td>未対応</td>
		</tr>			
		<tr>
			<td rowspan="1">clean</td>
			<td></td>
			<td>未対応</td>
		</tr>		
		<tr>
			<td rowspan="1">connPoolSync</td>
			<td></td>
			<td>未対応</td>
		</tr>		
			<tr>
			<td rowspan="1">connectionStatus</td>
			<td></td>
			<td>未対応</td>
		</tr>		
		<tr>
			<td rowspan="1">compact</td>
			<td></td>
			<td>未対応</td>
		</tr>		
			<tr>
			<td rowspan="1">collMod</td>
			<td></td>
			<td>未対応</td>
		</tr>		
			<tr>
			<td rowspan="1">reIndex</td>
			<td></td>
			<td>未対応</td>
		</tr>		
			<tr>
			<td rowspan="1">setParameter</td>
			<td></td>
			<td>未対応</td>
		</tr>		
			<tr>
			<td rowspan="1">getParameter</td>
			<td></td>
			<td>未対応</td>
		</tr>		
			<tr>
			<td rowspan="1">repairDatabase</td>
			<td></td>
			<td>未対応</td>
		</tr>		
			<tr>
			<td rowspan="1">repairCursor</td>
			<td></td>
			<td>未対応</td>
		</tr>		
			<tr>
			<td rowspan="1">touch</td>
			<td></td>
			<td>未対応</td>
		</tr>		
		<tr>
			<td rowspan="1">shutdown</td>
			<td></td>
			<td>未対応</td>
		</tr>		
		<tr>
			<td rowspan="1">logrotate</td>
			<td></td>
			<td>未対応</td>
		</tr>			
		<tr>
			<td rowspan="1">killop</td>
			<td></td>
			<td>未対応</td>
		</tr>		
		<tr>
		  <td rowspan="1">ユーザー管理コマンド</td>
			<td rowspan="1"></td>
			<td></td>
			<td>未対応</td>
		</tr>
			<tr>
		  <td rowspan="1">ロール管理コマンド</td>
			<td rowspan="1"></td>
			<td></td>
			<td>未対応</td>
		</tr>
				 <tr>
		  <td rowspan="30">レプリカセットコマンド</td>
			<td rowspan="1"></td>
			<td></td>
			<td>未対応</td>
		</tr>
	</tbody>
</table>

