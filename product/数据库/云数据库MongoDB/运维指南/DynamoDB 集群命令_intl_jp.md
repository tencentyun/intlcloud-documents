

### DynamoDBプロトコルの対応状況の説明
<table class="table-striped">
	<tbody>
		<tr>
		 <th>API名</th>
			<th>パラメータ</th>
			<th>サポートするかどうか</th>
		</tr>
		<tr>
		  <td rowspan="7">CreateTable</td>
			<td>必須入力のパラメータ:TableName</td>
			<td>はい</td>
		</tr>	
		<tr>
			<td>必須入力のパラメータ:AttributeDefinitions</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>必須入力のパラメータ:KeySchema</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>必須入力のパラメータ:ProvisionedThroughput</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：GlobalSecondaryIndexes</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：LocalSecondaryIndexes</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：StreamSpecification</td>
			<td>いいえ</td>
		</tr>
		<tr>
		  <td rowspan="5">BatchWriteItem</td>
			<td>必須入力のパラメータ：RequestItems</td>
			<td>はい</td>
		</tr>		
		<tr>
			<td>必須入力のパラメータ：PutRequest</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>必須入力のパラメータ：DeleteRequest</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ReturnConsumedCapacity</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ReturnItemCollectionMetrics</td>
			<td>いいえ</td>
		</tr>
		<tr>
		  <td rowspan="5">BatchGetItem</td>
			<td>RequestItems</td>
			<td>はい</td>
		</tr>	
		<tr>
			<td>ProjectionExpression</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>ExpressionAttributeNames</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ReturnConsumedCapacity</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ConsistentRead</td>
			<td>いいえ</td>
		</tr>
		<tr>
		  <td rowspan="7">DeleteItem</td>
			<td>ConditionExpression </td>
			<td>はい</td>
		</tr>	
		<tr>
			<td>Key</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>TableName</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：Expected</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ConditionOperator</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ReturnItemCollectinMetricst</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ReturnConsumedCapacity</td>
			<td>いいえ</td>
		</tr>
			<tr>
		  <td rowspan="1">DeleteTable</td>
			<td>必須入力のパラメータ：TableName</td>
			<td>はい</td>
		</tr>	
		<tr>
			<td rowspan="6" >DescribeTable</td>
			<td >必須入力のパラメータ：TableName</td>
			<td>はい</td>
		</tr>
			<tr>
			<td>応答パラメータ：Backfilling</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>応答パラメータ：ProvisionedThroughput </td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>応答パラメータ：LatestStreamArn</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>応答パラメータ：LatestStreamLabel</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>応答パラメータ：StreamSpecification </td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td rowspan="6" >GetItem</td>
			<td >必須入力のパラメータ：TableName</td>
			<td>はい</td>
		</tr>
			<tr>
			<td>必須入力のパラメータ：Key</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ConsistentRead</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ReturnConsumedCapacity</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ReturnConsumedCapacity</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ProjectionExpression</td>
			<td>いいえ</td>
		</tr>	
		<tr>
			<td rowspan="3" >ListTables</td>
			<td >必須入力のパラメータ：TableName</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：Limit</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ExclusiveStartTableName </td>
			<td>はい</td>
		</tr>
		<tr>
			<td rowspan="9" >PutItem</td>
			<td >必須入力のパラメータ：TableName</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>必須入力のパラメータ：Item</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ConditionExpression</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：Expected</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ConditionOperator</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ReturnItemCollectinMetrics</td>
			<td>いいえ</td>
		</tr>	
			<tr>
			<td>オプション入力のパラメータ：ReturnConsumedCapacity</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>応答パラメータ：ConsumedCapacity</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>応答パラメータ：ItemCollectionMetrics</td>
			<td>いいえ</td>
		</tr>	
		<tr>
			<td rowspan="13" >Query</td>
			<td >必須入力のパラメータ：TableName</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：FilterExpression</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：KeyConditions</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ConditionExpression</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：Select</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ReturnItemCollectinMetrics</td>
			<td>いいえ</td>
		</tr>	
			<tr>
			<td>オプション入力のパラメータ：ReturnConsumedCapacity</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ScanIndexForward</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ConditionOperator</td>
			<td>いいえ</td>
		</tr>	
			<tr>
			<td>オプション入力のパラメータ：ConsistentRead</td>
			<td>いいえ</td>
		</tr>	
			<tr>
			<td>オプション入力のパラメータ：Expected</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：IndexName</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>ProjectionExpression</td>
			<td>はい</td>
		</tr>		
		<tr>
			<td rowspan="9" >UpdateItem</td>
			<td >必須入力のパラメータ：Key</td>
			<td>はい</td>
		</tr>
			<tr>
			<td>必須入力のパラメータ：TableName</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：Expected</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ConditionOperator</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ReturnConsumedCapacity</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ReturnItemCollectinMetrics</td>
			<td>いいえ</td>
		</tr>	
		<tr>
			<td>UpdateExpression</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>応答パラメータ：ConsumedCapacity</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>応答パラメータ：.ItemCollectionMetrics</td>
			<td>いいえ</td>
		</tr>		
		<tr>
			<td rowspan="4" >UpdateTable</td>
			<td >必須入力のパラメータ：TableName</td>
			<td>はい</td>
		</tr>
			<tr>
			<td>オプション入力のパラメータ：TGlobalSecondaryIndexUpdates</td>
			<td>はい</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：ProvisionedThroughput</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td>オプション入力のパラメータ：StreamSpecification</td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td >Scan</td>
			<td ></td>
			<td>いいえ</td>
		</tr>
					<tr>
			<td >TagResourcee</td>
			<td ></td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td >UntagResource</td>
			<td ></td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td >ListTagsOfResource</td>
			<td ></td>
			<td>いいえ</td>
		</tr>
		<tr>
			<td >DescribeLimits</td>
			<td ></td>
			<td>いいえ</td>
		</tr>
	</tbody>
</table>

