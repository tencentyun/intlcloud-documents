### 샤딩 전략
1. 데이터 범위를 지원하는 샤딩 메커니즘
2. 연합 필드의 샤드 키를 지원합니다.
3. 샤딩 인스턴스의 모든 데이터 집합은 반드시 샤딩을 사용해야 합니다. 비샤딩 데이터는 독리적인 복제본 세트 인스턴스에 보관하는 것을 권장합니다.

### 인증 메커니즘
SCRAM-SHA-1과 MONGODB-CR 두 가지 메커니즘을 완벽하게 호환합니다.

### 샤딩 클러스터 명령 지원 상황
<table class="table-striped">
	<tbody>
		<tr>
		 <th>&nbsp;</th>
			<th>명령</th>
			<th>하위 명령</th>
			<th>지원 상황</th>
		</tr>
		<tr>
		  <td rowspan="39">CRUD 기본 명령</td>
			<td rowspan="22">find</td>
			<td>filter</td>
			<td>지원</td>
		</tr>		
		<tr>
			<td>sort</td>
			<td>지원</td>
		</tr>
		<tr>
			<td>projection</td>
			<td>지원</td>
		</tr>
		<tr>
			<td>hint</td>
			<td>지원</td>
		</tr>
		<tr>
			<td>skip</td>
			<td>지원</td>
		</tr>
		<tr>
			<td>limit</td>
			<td>지원</td>
		</tr>
		<tr>
			<td>batchSize</td>
			<td>지원</td>
		</tr>
		<tr>
			<td>singleBatch</td>
			<td>지원</td>
		</tr>
		<tr>
			<td>comment</td>
			<td>지원</td>
		</tr>
		<tr>
			<td>maxScan</td>
			<td>지원</td>
		</tr>
		<tr>
			<td>maxTimeMS</td>
			<td>지원하지 않음</td>
		</tr>
		<tr>
			<td>readConcern</td>
			<td>지원</td>
		</tr>
		<tr>
			<td>max</td>
			<td>지원</td>
		</tr>
		<tr>
			<td>min</td>
			<td>지원</td>
		</tr>
		<tr>
			<td>returnKey</td>
			<td>지원</td>
		</tr>
		<tr>
			<td>showRecordId</td>
			<td>지원</td>
		</tr>
		<tr>
			<td>snapshot</td>
			<td>지원하지 않음</td>
		</tr>
		<tr>
			<td>tailable</td>
			<td>지원하지 않음</td>
		</tr>
		<tr>
			<td>oplogReplay</td>
			<td>지원하지 않음</td>
		</tr>
		<tr>
			<td>noCursorTimeout</td>
			<td>지원</td>
		</tr>
		<tr>
			<td>awaitData</td>
			<td>지원하지 않음</td>
		</tr>
		<tr>
			<td>allowPartialResults</td>
			<td>지원하지 않음</td>
		</tr>		
		<tr>
			<td rowspan="1" >insert</td>
			<td >샤드 기 필드가 반드시 있어야 합니다. 배치로 삽입하는 경우, 샤드 기가 반드시 일치해야 합니다.</td>
			<td>지원</td>
		</tr>		
		<tr>
			<td rowspan="1">update</td>
			<td >업데이트 필드는 샤드 키일 수 없습니다.</td>
			<td>지원</td>
		</tr>		
		<tr>
			<td rowspan="1">delete</td>
			<td></td>
			<td>지원</td>
		</tr>			
		<tr>
			<td rowspan="1">findandmodify</td>
			<td></td>
			<td>지원</td>
		</tr>		
		<tr>
			<td rowspan="1">count</td>
			<td></td>
			<td>지원</td>
		</tr>		
			<tr>
			<td rowspan="1">distinct</td>
			<td>샤드 키가 반드시 있어야 합니다.</td>
			<td>지원</td>
		</tr>
    <tr>
			<td rowspan="1">aggregate</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
		 <tr>
			<td rowspan="1">group</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
		 <tr>
			<td rowspan="1">mapReduce</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>			
		<tr>
			<td rowspan="1">getmore</td>
			<td></td>
			<td>지원</td>
		</tr>		
		<tr>
			<td rowspan="1">getLastError</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>
		<tr>
			<td rowspan="1">getPrevError</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>
			<tr>
			<td rowspan="1">resetError</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
			<tr>
			<td rowspan="1">eval</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
			<tr>
			<td rowspan="1">geoNear</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
			<tr>
			<td rowspan="1">geoSearch</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>
			<tr>
			<td rowspan="1">parallelCollectionScan</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>
			<tr>
		  <td rowspan="6">진단 명령</td>
			<td rowspan="1">collStats</td>
			<td></td>
			<td>지원</td>
		</tr>		
			<tr>
			<td rowspan="1">dbstats</td>
			<td></td>
			<td>지원</td>
		</tr>		
			<tr>
			<td rowspan="1">explain</td>
			<td></td>
			<td>지원</td>
		</tr>		
			<tr>
			<td rowspan="1">listDatabases</td>
			<td></td>
			<td>지원</td>
		</tr>		
			<tr>
			<td rowspan="1">serverStatus</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>
			<tr>
			<td rowspan="1">top</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>
			<tr>
		  <td rowspan="2">샤딩 명령</td>
			<td rowspan="1">enableSharding</td>
			<td></td>
			<td>지원</td>
		</tr>		
			<tr>
			<td rowspan="1">shardCollection</td>
			<td></td>
			<td>지원</td>
		</tr>		
		 <tr>
		  <td rowspan="30">관리 명령</td>
			<td rowspan="1">listCollections</td>
			<td></td>
			<td>지원</td>
		</tr>
			<tr>
			<td rowspan="1">dropDatabase</td>
			<td></td>
			<td>지원</td>
		</tr>
			<tr>
			<td rowspan="1">drop</td>
			<td></td>
			<td>지원</td>
		</tr>
			<tr>
			<td rowspan="1">creareIndexes</td>
			<td></td>
			<td>지원</td>
		</tr>				
			<tr>
			<td rowspan="1">listIndexes</td>
			<td></td>
			<td>지원</td>
		</tr>			
		<tr>
			<td rowspan="1">dropIndexes</td>
			<td></td>
			<td>지원</td>
		</tr>		
			<tr>
			<td rowspan="1">logout</td>
			<td></td>
			<td>지원</td>
		</tr>				
			<tr>
			<td rowspan="1">renameCollection</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>			
			<tr>
			<td rowspan="1">copydb</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>				
			<tr>
			<td rowspan="1">create</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>				
		<tr>
			<td rowspan="1">clone</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>			
		<tr>
			<td rowspan="1">cloneCollection</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>				
		<tr>
			<td rowspan="1">cloneCollectionAsCapped</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
		<tr>
			<td rowspan="1">convetToCapped</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>			
		<tr>
			<td rowspan="1">filemd5</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
		<tr>
			<td rowspan="1">fsync</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>			
		<tr>
			<td rowspan="1">clean</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
		<tr>
			<td rowspan="1">connPoolSync</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
			<tr>
			<td rowspan="1">connectionStatus</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
		<tr>
			<td rowspan="1">compact</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
			<tr>
			<td rowspan="1">collMod</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
			<tr>
			<td rowspan="1">reIndex</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
			<tr>
			<td rowspan="1">setParameter</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
			<tr>
			<td rowspan="1">getParameter</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
			<tr>
			<td rowspan="1">repairDatabase</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
			<tr>
			<td rowspan="1">repairCursor</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
			<tr>
			<td rowspan="1">touch</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
		<tr>
			<td rowspan="1">shutdown</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
		<tr>
			<td rowspan="1">logrotate</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>			
		<tr>
			<td rowspan="1">killop</td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>		
		<tr>
		  <td rowspan="1">사용자 관리 명령</td>
			<td rowspan="1"></td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>
			<tr>
		  <td rowspan="1">역할 관리 명령</td>
			<td rowspan="1"></td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>
				 <tr>
		  <td rowspan="30">복제본 세트 명령</td>
			<td rowspan="1"></td>
			<td></td>
			<td>지원하지 않음</td>
		</tr>
	</tbody>
</table>
