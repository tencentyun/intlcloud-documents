This document describes how to design a script for matching rules.

## JSON Rule Structure
The structure of a matchmaking rule script is as follows:
![](https://main.qcloudimg.com/raw/aad1e2502fc20e8a93d2afcdacb50a3a.png)

## Parameter Details

### version
This required parameter describes the version information. Currently, its value can only be "v1.0", as shown below:
```json
"version": "v1.0"
```
### playerAttributes

This optional parameter is an array consisting of 0-5 player attributes.
- **Parameters**
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>name</td>
<td>string</td>
<td>Yes</td>
<td>Attribute name, which corresponds to the attribute name passed in to the <a href="https://intl.cloud.tencent.com/zh/document/product/1072/39931" target="_blank">StartMatching</a> API. The `name` parameter in the array is unique, which contains letters and digits only.</td>
</tr>
<tr>
<td>type</td>
<td>string</td>
<td>Yes</td>
<td>Attribute type. Valid values: `number`, `string`</td>
</tr>
<tr>
<td>default</td>
<td>number/string</td>
<td>No</td>
<td>Default value of the attribute specified in `type`.<ul><li>If the attribute value is not passed in a matchmaking request, the default value will be used.</ul><ul><li>If no default value is provided, a matchmaking request must specify the attribute value.</ul></td>
</tr>
</tbody></table>

- **Sample code**
```json
"playerAttributes": [
		{
			"name": "skill",
			"type": "number",
			"default": 10
        },
        {
            "name": "gameMode",
			"type": "string",
			"default": "classic"
        }
	]
```

### teams

This required parameter indicates all team types in a complete match. Currently, a team consists of up to 40 players.
- **Parameters**
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>name</td>
<td>string</td>
<td>Yes</td>
<td>Team type. The `name` parameter in the array is unique, which contains letters and digits.</td>
</tr>
<tr>
<td>maxPlayers</td>
<td>number</td>
<td>Yes</td>
<td>Maximum number of players in a team of this type</td>
</tr>
<tr>
<td>minPlayers</td>
<td>number</td>
<td>Yes</td>
<td>Minimum number of players in a team of this type</td>
</tr>
<tr>
<td>number</td>
<td>number_list</td>
<td>No</td>
<td><ul><li>Number of teams of this type.</li><li>The `number_list` parameter only contains two elements in the format of [MinTeamCount, MaxTeamCount].</li><li>If this parameter is not specified, the default value [1,1] will be used, indicating that a complete match involves only one team of this type .</li><li>Currently, `MinTeamCount` must be equal to `MaxTeamCount, and a team must have fixed number of players.</li></ul></td>
</tr>
</tbody></table>

- **Sample code**
```json
"teams": [
		{
			"name": "soldier",
			"maxPlayers": 4,
			"minPlayers": 4,
			"number": [2,2]
		},
		{
			"name": "king",
			"maxPlayers": 4,
			"minPlayers": 4
		}
	]
```


### rules

This optional parameter is an array consisting of 0-10 matchmaking rules. Valid values: `distanceRule`, `comparisonRule`, and `latencyRule`. For more information about rules, see [Rule Types](https://intl.cloud.tencent.com/document/product/1072/39870).
- **Parameters**
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Required</th>
<th>Applicable Rule</th>
</tr>
</thead>
<tbody><tr>
<td>name</td>
<td>string</td>
<td>Yes</td>
<td>All rules</td>
</tr>
<tr>
<td>type</td>
<td>string</td>
<td>Yes</td>
<td>All rules</td>
</tr>
<tr>
<td>description</td>
<td>string</td>
<td>No</td>
<td>All rules</td>
</tr>
<tr>
<td>measurements</td>
<td>-</td>
<td>-</td>
<td>distanceRule, comparisonRule</td>
</tr>
<tr>
<td>referenceValue</td>
<td>-</td>
<td>-</td>
<td>distanceRule, comparisonRule</td>
</tr>
<tr>
<td>operation</td>
<td>-</td>
<td>-</td>
<td>comparisonRule</td>
</tr>
<tr>
<td>maxDistance</td>
<td>-</td>
<td>-</td>
<td>distanceRule, latencyRule</td>
</tr>
<tr>
<td>minDistance</td>
<td>-</td>
<td>-</td>
<td>distanceRule</td>
</tr>
<tr>
<td>maxLatency</td>
<td>-</td>
<td>-</td>
<td>latencyRule</td>
</tr>
<tr>
<td>distanceReference</td>
<td>-</td>
<td>-</td>
<td>latencyRule</td>
</tr>
<tr>
<td>partyAggregation</td>
<td>string</td>
<td>No</td>
<td>All rules</td>
</tr>
</tbody></table>

>?The “Type” and “Required” fields of the `measurements`, `referenceValue`, `operation`, `maxDistance`, `minDistance`, `maxLatency` and `distanceReference` parameters are determined by the rule type. For more information, see [Rule Types](https://intl.cloud.tencent.com/document/product/1072/39870).

- **Sample code**
```json
 "rules": [{
        "name": "FairTeamSkill",
        "type": "distanceRule",
        "measurements": [ "avg(teams[*].players.playerAttributes[skill])" ],
        "referenceValue": "avg(flatten(teams[*].players.playerAttributes[skill]))",
        "maxDistance": 10
    }, {
        "name": "RedTeamSelection",
        "type": "comparisonRule",
        "operation": "=",
        "measurements": ["flatten(teams[red].players.playerAttributes[colour])"],
        "referenceValue": "red"
    }, {
        "name": "FastConnection",
        "type": "latencyRule",
        "maxLatency": 50
    }]
```

### expansions

A matchmaking rule expansion contains 0-5 targets that consist of 1-10 steps. You can configure `waitTimeSeconds` to adjust the limitations of the matchmaking rule.
- **Parameters**
<table class="typical">
	<tbody>
	<tr>
		<th colspan="2">Parameter</th>
		<th>Type</th>
		<th>Required</th>
        <th>Description</th>
        <th>Valid Value</th>
	</tr>
	<tr>
		<td colspan="2">target</td>
		<td>string</td>
		<td>Yes</td>
        <td >Target to be adjusted</td>
        <td ><ul><li>Teams: minPlayers, maxPlayers<br> <li>distanceRule: minDistance, maxDistance <br> <li>latencyRule: maxLatency, maxDistance</ul></td>
	</tr>
	<tr>
		<td rowspan="2" >steps</td>
		<td>waitTimeSeconds</td>
        <td>number</td>
        <td>Yes</td>
        <td>Wait time in second</td>
        <td>number</td>
	</tr>
    	<tr>
		<td>value</td>
        <td>number</td>
        <td>Yes</td>
        <td>Updated target value after `waitTimeSeconds`</td>
		<td>number</td>
	</tr>
</tbody></table>
- **Sample code**
```json
    "expansions": [{
        "target": "teams[soldier].minPlayers",
        "steps": [{
            "waitTimeSeconds": 5,
            "value": 6
        }, {
            "waitTimeSeconds": 15,
            "value": 4
        }]
    }, {
        "target": "rules[FastConnection].maxLatency",
        "steps": [{
            "waitTimeSeconds": 10,
            "value": 100
        }, {
            "waitTimeSeconds": 20,
            "value": 150
        }]
    }]
```

## Expressions

### Operator
<table>
<thead>
<tr>
<th>Operator</th>
<th style="
    width: 40%;
">Input</th>
<th style="
    width: 26%;
">Output</th>
<th style="
    width: 20%;
">Description</th>
</tr>
</thead>
<tbody><tr>
<td>avg</td>
<td>List&lt; number &gt; List&lt; List&lt; number &gt;&gt;</td>
<td>number, List&lt; number &gt;</td>
<td>Obtains the average value of the list.</td>
</tr>
<tr>
<td>flatten</td>
<td>List&lt; List&lt; ? &gt;&gt;</td>
<td>List&lt; ? &gt;</td>
<td>Changes the two-dimensional list to a flat list that contains all elements.</td>
</tr>
</tbody></table>


### Expression
<table>
<thead>
<tr>
<th>Expression</th>
<th>Description</th>
<th style="
    width: 21%;
">Result Type</th>
<th>Usage</th>
</tr>
</thead>
<tbody><tr>
<td>teams[soldier].maxPlayers</td>
<td>Maximum number of players in the `soldier` team</td>
<td>number</td>
<td><li>Used to configure `target` under `expansions`</li></td>
</tr>
<tr>
<td>teams[soldier].players.playerAttributes[xxx]</td>
<td>List of attributes xxx of players in the `soldier` team</td>
<td>List&lt; List&lt; ? &gt;&gt;</td>
<td><li>Used to configure `measurements` under `rules`<br> </li><li>Used to configure `referenceValue` under `rules`</li></td>
</tr>
<tr>
<td>teams[*].players.playerAttributes[xxx]</td>
<td>List of attributes xxx of players in all teams</td>
<td>List&lt; List&lt; ? &gt;&gt;</td>
<td><li>Used to configure `measurements` under `rules`<br> </li><li>Used to configure `referenceValue` under `rules`</li></td>
</tr>
<tr>
<td>teams[soldier].players[playerId]</td>
<td>List of IDs of players in the `soldier` team</td>
<td>List&lt; List&lt; string &gt;&gt;</td>
<td><li>Used to configure `measurements` under the rule type `comparisonRule`</li></td>
</tr>
<tr>
<td>rules[FairTeamSkill].maxDistance</td>
<td>The `maxDistance` parameter of the `FairTeamSkill` rule</td>
<td>number</td>
<td><li>Used to configure `target` under `expansions`</li></td>
</tr>
</tbody></table>
