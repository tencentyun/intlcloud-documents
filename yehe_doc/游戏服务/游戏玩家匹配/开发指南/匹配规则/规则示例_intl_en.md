
>!Since the product logic no longer meets the technical development of game industry, Game Player Matching GPM will be deprecated on June 1st, 2022. Please complete service migration before May 31, , 2022.

This document describes typical rule examples.

## 4V4V4 Difference and Latency Rules

Use case: the average skill difference between each team and all matched teams is no more than 10 when a matchmaking request is initiated. In addition, all players have latencies of no more than 50 ms to at least one region. Add an expansion rule, which will be relaxed a while later.
```json
{
	"version": "v1.0",
	"playerAttributes": [
		{
			"name": "skill",
			"type": "number",
			"default": 10
		}
	],
	"teams": [
		{
			"name": "red",
			"maxPlayers": 4,
			"minPlayers": 4
		},
		{
			"name": "green",
			"maxPlayers": 4,
			"minPlayers": 4
		},
		{
			"name": "blue",
			"maxPlayers": 4,
			"minPlayers": 4
		}
	],
	"rules": [
		{
			"name": "FairTeamSkill",
			"type": "distanceRule",
			"measurements": [
				"avg(teams[*].players.playerAttributes[skill])"
			],
			"referenceValue": "avg(flatten(teams[*].players.playerAttributes[skill]))",
			"maxDistance": 10
		},
		{
			"name": "FastConnection",
			"type": "latencyRule",
			"maxLatency": 50
		}
	],
	"expansions": [
		{
			"target": "rules[FairTeamSkill].maxDistance",
			"steps": [
				{
					"waitTimeSeconds": 5,
					"value": 50
				},
				{
					"waitTimeSeconds": 15,
					"value": 100
				}
			]
		},
		{
			"target": "rules[FastConnection].maxLatency",
			"steps": [
				{
					"waitTimeSeconds": 10,
					"value": 100
				},
				{
					"waitTimeSeconds": 20,
					"value": 150
				}
			]
		}
	]
}
```




## XV8 Asymmetric Matching and Comparison Rule
Use case: two teams with different number of players are matched to a game battle, where team A has variable players, and team B has fixed players. These players should select the same game mode.
```json
{
    "version": "v1.0",
    "playerAttributes": [{
        "name": "gameMode",
        "type": "string",
        "default": "turn-based"
    }],
    "teams": [{
        "name": "red",
        "maxPlayers": 7,
        "minPlayers": 2
    }, {
        "name": "blue",
        "maxPlayers": 8,
        "minPlayers": 8 
    }],
    "rules": [ {
        "name": "SameGameMode",
        "type": "comparisonRule",
        "operation": "=",
        "measurements": ["flatten(teams[*].players.playerAttributes[gameMode])"]
    }]
}
```

## 0V5 Man-machine Battle

Use case: a team of 5 players are matched to a battle against a user-defined robot
```json
{
    "version": "v1.0",
    "playerAttributes": [{
        "name": "skill",
        "type": "number"
    }],
    "teams": [{
        "name": "Marauders",
        "maxPlayers": 5,
        "minPlayers": 5
    }],
    "rules": [{
        "name": "lowLatency",
        "description": "Sets maximum acceptable latency",
        "type": "latencyRule",
        "maxLatency": 150
    }],
    "expansions": [{
        "target": "rules[lowLatency].maxLatency",
        "steps": [{
            "waitTimeSeconds": 12,
            "value": 200
        }]
    }]
}
```


## 2V2 One of the Two Teams without a Constraint Rule
```json
{
    "version": "v1.0",
    "playerAttributes": [{
        "name": "skill",
        "type": "number"
    }],
    "teams": [{
        "name": "red",
        "maxPlayers": 2,
        "minPlayers": 2
    },{
        "name": "blue",
        "maxPlayers": 2,
        "minPlayers": 2
    }],
    "rules": [{
        "name": "redTeamRule",
        "type": "distanceRule",
        "measurements":["teams[red].players.playerAttributes[skill]"],
        "referenceValue":10,
        "maxDistance": 5
    }]
}
```
