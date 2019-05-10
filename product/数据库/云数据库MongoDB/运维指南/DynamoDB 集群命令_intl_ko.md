

### DynamoDB 프로토콜 지원 상황 설명
<table class="table-striped">
	<tbody>
		<tr>
		 <th>API 이름</th>
			<th>매개변수</th>
			<th>지원 여부</th>
		</tr>
		<tr>
		  <td rowspan="7">CreateTable</td>
			<td>필수 입력 매개변수: TableName</td>
			<td>예</td>
		</tr>	
		<tr>
			<td>필수 입력 매개변수: AttributeDefinitions</td>
			<td>예</td>
		</tr>
		<tr>
			<td>필수 입력 매개변수: KeySchema</td>
			<td>예</td>
		</tr>
		<tr>
			<td>필수 입력 매개변수: ProvisionedThroughput</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: GlobalSecondaryIndexes</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: LocalSecondaryIndexes</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: StreamSpecification</td>
			<td>아니요</td>
		</tr>
		<tr>
		  <td rowspan="5">BatchWriteItem</td>
			<td>필수 입력 매개변수: RequestItems</td>
			<td>예</td>
		</tr>		
		<tr>
			<td>필수 입력 매개변수: PutRequest</td>
			<td>예</td>
		</tr>
		<tr>
			<td>필수 입력 매개변수: DeleteRequest</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ReturnConsumedCapacity</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ReturnItemCollectionMetrics</td>
			<td>아니요</td>
		</tr>
		<tr>
		  <td rowspan="5">BatchGetItem</td>
			<td>RequestItems</td>
			<td>예</td>
		</tr>	
		<tr>
			<td>ProjectionExpression</td>
			<td>예</td>
		</tr>
		<tr>
			<td>ExpressionAttributeNames</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ReturnConsumedCapacity</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ConsistentRead</td>
			<td>아니요</td>
		</tr>
		<tr>
		  <td rowspan="7">DeleteItem</td>
			<td>ConditionExpression </td>
			<td>예</td>
		</tr>	
		<tr>
			<td>Key</td>
			<td>예</td>
		</tr>
		<tr>
			<td>TableName</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: Expected</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ConditionOperator</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ReturnItemCollectinMetricst</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ReturnConsumedCapacity</td>
			<td>아니요</td>
		</tr>
			<tr>
		  <td rowspan="1">DeleteTable</td>
			<td>필수 입력 매개변수: TableName</td>
			<td>예</td>
		</tr>	
		<tr>
			<td rowspan="6" >DescribeTable</td>
			<td >필수 입력 매개변수: TableName</td>
			<td>예</td>
		</tr>
			<tr>
			<td>응답 매개변수: Backfilling</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>응답 매개변수: ProvisionedThroughput </td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>응답 매개변수: LatestStreamArn</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>응답 매개변수: LatestStreamLabel</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>응답 매개변수: StreamSpecification </td>
			<td>아니요</td>
		</tr>
		<tr>
			<td rowspan="6" >GetItem</td>
			<td >필수 입력 매개변수: TableName</td>
			<td>예</td>
		</tr>
			<tr>
			<td>필수 입력 매개변수: Key</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ConsistentRead </td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ReturnConsumedCapacity</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ReturnConsumedCapacity</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ProjectionExpression</td>
			<td>아니요</td>
		</tr>	
		<tr>
			<td rowspan="3" >ListTables</td>
			<td >필수 입력 매개변수: TableName</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: Limit</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ExclusiveStartTableName </td>
			<td>예</td>
		</tr>
		<tr>
			<td rowspan="9" >PutItem</td>
			<td >필수 입력 매개변수: TableName</td>
			<td>예</td>
		</tr>
		<tr>
			<td>필수 입력 매개변수: Item</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ConditionExpression</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: Expected</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ConditionOperator</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ReturnItemCollectinMetrics</td>
			<td>아니요</td>
		</tr>	
			<tr>
			<td>옵션 입력 매개변수: ReturnConsumedCapacity</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>응답 매개변수: ConsumedCapacity</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>응답 매개변수: ItemCollectionMetrics</td>
			<td>아니요</td>
		</tr>	
		<tr>
			<td rowspan="13" >Query</td>
			<td >필수 입력 매개변수: TableName</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: FilterExpression</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: KeyConditions</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ConditionExpression</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: Select</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ReturnItemCollectinMetrics</td>
			<td>아니요</td>
		</tr>	
			<tr>
			<td>옵션 입력 매개변수: ReturnConsumedCapacity</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ScanIndexForward </td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ConditionOperator </td>
			<td>아니요</td>
		</tr>	
			<tr>
			<td>옵션 입력 매개변수: ConsistentRead</td>
			<td>아니요</td>
		</tr>	
			<tr>
			<td>옵션 입력 매개변수: Expected</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: IndexName</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>ProjectionExpression</td>
			<td>예</td>
		</tr>		
		<tr>
			<td rowspan="9" >UpdateItem</td>
			<td >필수 입력 매개변수: Key</td>
			<td>예</td>
		</tr>
			<tr>
			<td>필수 입력 매개변수: TableName</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: Expected</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ConditionOperator</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ReturnConsumedCapacity</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ReturnItemCollectinMetrics</td>
			<td>아니요</td>
		</tr>	
		<tr>
			<td>UpdateExpression</td>
			<td>예</td>
		</tr>
		<tr>
			<td>응답 매개변수: ConsumedCapacity</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>응답 매개변수: .ItemCollectionMetrics</td>
			<td>아니요</td>
		</tr>		
		<tr>
			<td rowspan="4" >UpdateTable</td>
			<td >필수 입력 매개변수: TableName</td>
			<td>예</td>
		</tr>
			<tr>
			<td>옵션 입력 매개변수: TGlobalSecondaryIndexUpdates</td>
			<td>예</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: ProvisionedThroughput</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td>옵션 입력 매개변수: StreamSpecification</td>
			<td>아니요</td>
		</tr>
		<tr>
			<td >Scan</td>
			<td ></td>
			<td>아니요</td>
		</tr>
					<tr>
			<td >TagResourcee</td>
			<td ></td>
			<td>아니요</td>
		</tr>
		<tr>
			<td >UntagResource</td>
			<td ></td>
			<td>아니요</td>
		</tr>
		<tr>
			<td >ListTagsOfResource</td>
			<td ></td>
			<td>아니요</td>
		</tr>
		<tr>
			<td >DescribeLimits</td>
			<td ></td>
			<td>아니요</td>
		</tr>
	</tbody>
</table>

