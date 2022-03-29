>!Since the product logic no longer meets the technical development of game industry, Game Player Matching GPM will be deprecated on June 1st, 2022. Please complete service migration before May 31, , 2022.
This document describes GPM matching rules.

## Difference Rule

A difference rule is used to limit the difference between the measurements and the reference value.

- #### Attributes
<table class="typical">
	<tbody>
	<tr>
		<th>Attribute</th>
		<th>Description</th>
		<th>Required</th>
		<th>Valid Value</th>
	</tr>
	<tr>
		<td>name</td>
		<td >Rule name</td>
		<td>Yes</td>
		<td >The rule name in one `RuleScript` is unique, which can only contain letters and digits.
	</tr>
		<tr>
		<td>type</td>
		<td >Rule type</td>
		<td>Yes</td>
		<td >`distanceRule`</td>
	</tr>
		<tr>
		<td>description</td>
		<td >Rule description</td>
		<td>No</td>
		<td >Strings</td>
	</tr>
		<tr>
		<td>measurements</td>
		<td >Measured value. It is used to compare with the `referenceValue`</td><td>Yes</td>
		<td >An operation expression that can be parsed into a number or list of numbers. For example, <ul><li>"avg(teams[*].players.playerAttributes[skill])"<li>"avg(flatten((teams[*].players.playerAttributes[skill])"</ul> </td>
	</tr>
		<tr>
		<td>referenceValue</td>
		<td >Comparison reference value</td>
		<td>Yes</td>
		<td >A number or an operation expression that can be parsed into a numeric value. For example,<ul><li>60<li>"avg(flatten((teams[*].players.playerAttributes[skill])"</ul></td>
	</tr>
		<tr>
		<td>minDistance</td>
		<td >Minimum distance</td>
		<td >`minDistance` and `maxDistance` cannot be both empty.</td><td >A number between 0 to 99999.</td>
	</tr>
		<tr>
		<td>maxDistance</td>
		<td >Maximum distance</td>
		<td >`minDistance` and `maxDistance` cannot be both empty.</td>
		<td >A number between 0 to 99999</td>
	</tr>
		<tr>
		<td>partyAggregation</td>
		<td >Processing method for multiplayer MatchTicket</td>
		<td>No</td>
		<td ><ul><li>Valid values: `each`, `min`, `max`, `avg`, `any` <li>Default value: `each` <li>For more information about `partyAggregation`, see <a  href= https://intl.cloud.tencent.com/document/product/1072/39215>Multi-player Match</a></ul></td>
	</tr>
</tbody></table>


- #### Implementation
  GPM will search for suitable MatchTicket that allows the absolute value of difference between `measurements` and `referenceValue` to be no more than `maxDistance` and no less than `minDistance`.
    - If the `measurement` expression is parsed into a number, it will be compared with `referenceValue`.
    - If the `measurement` expression is parsed into a list of numbers, each of its elements will be compared with `referenceValue`.


- #### Samples
The following sample codes show that the average skill deviation of each team from that of all teams in a game battle is no more than 10.
```json
 "rules": [{
        "name": "FairTeamSkill",
        "type": "distanceRule",
        "measurements": [ "avg(teams[*].players.playerAttributes[skill])" ],
        "referenceValue": "avg(flatten(teams[*].players.playerAttributes[skill]))",
        "maxDistance": 10
    }]
```

## Comparison Rule
A comparison rule is used to indicate the relationship between string or numeric attributes by comparison operators.
- #### Attributes
<table class="typical">
	<tbody>
	<tr>
		<th>Attribute</th>
		<th>Description</th>
		<th>Required</th>
		<th>Valid Value</th>
	</tr>
	<tr>
		<td>name</td>
		<td >Rule name</td>
		<td>Yes</td>
		<td >The rule name in one `RuleScript` is unique, which can only contain letters and digits.
	</tr>
		<tr>
		<td>type</td>
		<td >Rule type</td>
		<td>Yes</td>
		<td >`comparisonRule`</td>
	</tr>
		<tr>
		<td>description</td>
		<td >Rule description</td>
		<td>No</td>
		<td >Strings</td>
	</tr>
		<tr>
		<td>measurements</td>
		<td >Measured value. It is used to compare with `referenceValue`</td>
		<td>Yes</td>
		<td >An operation expression that can be parsed into a number, list of numbers, string, or list of strings. For example, <ul><li>"flatten(teams[*].players.playerAttributes[gender])" <li>"avg(flatten(teams[*].players.playerAttributes[skill]))"</ul></td>
	</tr>
		<tr>
		<td>referenceValue</td>
		<td >Comparison reference value</td>
		<td>No</td>
		<td >A number, string, or an operation expression that can be parsed into a number, such as "avg(flatten((teams[*].players.playerAttributes[skill])"</td>
	</tr>
		<tr>
		<td>operation</td>
		<td >Comparison operator</td>
		<td>Yes</td>
		<td >Valid values: `=`, `!=`, `<`, `<=`, `>`, `>=` (For strings, the valid values include `=` and `!=`)</td>
	</tr>
	</tr>
		<tr>
		<td>partyAggregation</td>
		<td >Processing method for multiplayer MatchTicket</td>
		<td>No</td>
		<td ><ul><li>Valid values: `each`, `min`, `max`, `avg`, `any`  <li>Default value: each <li>For more information about `partyAggregation`, see <a  href= https://intl.cloud.tencent.com/document/product/1072/39215>Multi-player Match</a></ul></td>
	</tr>
</tbody></table>

- #### Implementation
  GPM will search for suitable MatchTicket that allows the relationship between `measurements` and `referenceValue` to satisfy the comparison operator specified in `operation`.
    - If the `measurement` expression is parsed into a number, it will be compared with `referenceValue`.
    - If the `measurement` expression is parsed into a list of numbers, each of its elements will be compared with `referenceValue`.
    - If the `measurement` expression is parsed into a string, it will be judged according to whether it is the same as `referenceValue`.
    - If the `measurement` expression is parsed into a list of strings, each of its elements will be judged according to whether each is the same as `referenceValue`.
    - If `referenceValue` is not specified, each element of `measurements` will take the defined player attribute or not according to `operation`.
- #### Samples
    - Sample 1: players matched should choose the same gameMode
```json
 "rules": [{
        "name": "SameGameMode",
        "type": "comparisonRule",
        "operation": "=",
        "measurements": ["flatten(teams[*].players.playerAttributes[gameMode])"]
    }]
```
    - Sample 2: the color attribute of the red team players must be `red`
```json
 "rules": [{
        "name": "RedTeamSelection",
        "type": "comparisonRule",
        "operation": "=",
		"measurements": ["flatten(teams[red].players.playerAttributes[colour])"],
		"referenceValue": "red"
    }]
```


## Latency Rule
A latency rule is used to match players to servers according to the region latency, ensuring matched players from different regions have similar response time.
>? GPM matches players according to the region latency without updating or choosing regions for players. After players are successfully matched based on latency rules, at least one region meets the rule conditions for battle players. Then, GSE will choose the region for battle servers. For more information, see [Nearby Resource Scheduling](https://intl.cloud.tencent.com/document/product/1055/37404).
>

- #### Attributes
<table>
  <tbody>
  <tr>
      <th>Attribute</th>
      <th>Description</th>
      <th>Required</th>
      <th>Valid Value</th>
  </tr>
  <tr>
      <td>name</td>
      <td>Rule name</td>
      <td>Yes</td>
      <td>The rule name in one `RuleScript` is unique, which can only contain letters and digits.
  </td></tr>
      <tr>
      <td>type</td>
      <td>Rule type</td>
      <td>Yes</td>
      <td>latencyRule</td>
  </tr>
      <tr>
      <td>description</td>
      <td>Rule description</td>
      <td>No</td>
      <td>Strings</td>
  </tr>
      <tr>
      <td>maxLatency</td>
      <td>Acceptable maximum latency to the service region</td>
      <td>Yes</td>
      <td>A number between 0 to 999999</td>
  </tr>
      <tr>
      <td>maxDistance</td>
      <td>Maximum difference between the latency of each player to the service region and `distanceReference`</td>
      <td>No. It must be used with `distanceReference`.</td>
      <td >A number between 0 to 999999</td>
  </tr>
      <tr>
      <td>distanceReference</td>
      <td>Reference value</td>
      <td>No. It must be used with `maxDistance`.</td>
      <td>Valid values: `min`, `avg`<ul><li>`min`: the minimum latency of all matched players to a region</li><li>`avg`: the average latency of all matched players to a region</li></ul></td>
  </tr>
      <tr>
      <td>partyAggregation</td>
      <td>Processing method for multi-player MatchTicket</td>
      <td>No</td>
      <td><ul><li>Valid values: `each`, `min`, `max`, `avg`, `any`</li><li>Default value: `each`</li><li>For more information about `partyAggregation`, see <a href="https://intl.cloud.tencent.com/document/product/1072/39215" target="_blank">Multi-player Team Match</a></li></ul></td>
  </tr>
</tbody></table>
- #### Implementation
Each player inputs the latency from their respective location to every region when sending a matchmaking request. GPM will search for suitable MatchTicket that allows at least one region to meet the latency rule for matched players.
>? GPM does not support latency test. You need to do so by yourself or use the [Latency Test Tool](https://intl.cloud.tencent.com/document/product/1055/39060) provided by GSE.
- #### Samples
    - Sample 1: all players matched to a game have latencies of no more than 150 ms to at least one region
```json
"rules": [{
        "name": "lowLatency",
        "type": "latencyRule",
        "maxLatency": 150
    }]
```
    - Sample 2: all players matched to a game have latencies of no more than 150 ms to at least one region, and their latency difference is less than 80 ms.
```json
"rules": [{
        "name": "lowLatency",
        "type": "latencyRule",
		"maxLatency": 150,
		"maxDistance": 80,
		"distanceReference":"min"
    }]
```
