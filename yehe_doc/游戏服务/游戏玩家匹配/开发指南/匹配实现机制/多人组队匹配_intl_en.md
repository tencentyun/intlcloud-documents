>!Since the product logic no longer meets the technical development of game industry, Game Player Matching GPM will be deprecated on June 1st, 2022. Please complete service migration before May 31, , 2022.
The document describes the GPM team match mechanism.


## Initiating Team Match

Players passed in the [StartMatching](https://intl.cloud.tencent.com/document/product/1072/39904) API initiate a team match. These players have the same MatchTicket.

#### GPM rule on team match ticket

- **partyAggregation**
  Configure the `partyAggregation` parameter in the rule script to define the calculations of team player attributes.
<table>
<thead>
<tr>
<th align="left">Valid Value</th>
<th>Description</th>
<th>Applied Parameters</th>
</tr>
</thead>
<tbody><tr>
<td align="left">avg</td>
<td>Each player owning the same MatchTicket will use the average team attribute.</td>
<td>number and latency</td>
</tr>
<tr>
<td align="left">min</td>
<td>Each player owning the same MatchTicket will use the minimum attribute value of the team.</td>
<td>number and latency</td>
</tr>
<tr>
<td align="left">max</td>
<td>Each player owning the same MatchTicket will use the maximum attribute value of the team.</td>
<td>number and latency</td>
</tr>
<tr>
<td align="left">each</td>
<td>Each player owning the same MatchTicket will use their respective attribute value.</td>
<td>string, number, and latency</td>
</tr>
<tr>
<td align="left">any</td>
<td>Each player owning the same MatchTicket will use the same random attribute value of the team.</td>
<td>string, number, and latency</td>
</tr>
</tbody></table>

>! The `partyAggregation` parameter defined in the player attribute rule only takes effect on players owning the same MatchTicket that specify the same team.

## Examples

See below for a sample rule configuration:
```json
{
    "version": "v1.0",
    "playerAttributes": [{
        "name": "skill",
        "type": "number"
    }],
    "teams": [{
        "name": "red",
        "maxPlayers": 4,
        "minPlayers": 4
    }],
    "rules": [ {
			"name": "TeamSkill",
			"measurements": [
				"avg(teams[red].players.playerAttributes[skill])"
			],
			"referenceValue": 30,
            "maxDistance": 10,
            "partyAggregation":"max"
		}]
}
```
This rule shows that four players need to be matched to the red team, and the difference between the TeamSkill average and the reference value 30 should be less than 10. The `partyAggregation` parameter is configured to “max”, indicating that the each player owning the same MatchTicket should use the maximum attribute value of the team, as shown below:
- Assume MatchTicket1 applies to three team match players: player_A, player_B, and player_C.
- Assume MatchTicket2 applies to one team match player: player_D.
- The skill attributes of the four players are: A (20), B (30), C (35), and D (30).

As shown above, max (A, B, C) = 35, and max (D) = 30. To determine whether MatchTicket1 and MatchTicket 2 satisfy the matchmaking conditions of the TeamSkill rule, GPM firstly replace the value as follows:
 - A'(35), B'(35), C'(35), and D'(30)

Since avg (A', B', C', D') is equal to 33.75, the TeamSkill rule will be fulfilled. MatchTicket1 and MatchTicket2 can be successfully matched.

