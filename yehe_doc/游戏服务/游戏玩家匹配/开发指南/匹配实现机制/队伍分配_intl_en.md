>!Since the product logic no longer meets the technical development of game industry, Game Player Matching GPM will be deprecated on June 1st, 2022. Please complete service migration before May 31, , 2022.
This document uses a rule as an example to describe how to slot players to team in GPM.

## Sample Rule

The following rule shows a complete match of players to one red and two blue teams. Each team has 3 players in a 3v3v3 battle structure.
```json
{
    "version": "v1.0",
    "teams": [{
        "name": "red",
        "maxPlayers": 3,
        "minPlayers": 3
    }, {
        "name": "blue",
        "maxPlayers": 3,
        "minPlayers": 3,
        "number": [2,2]
    }]
}
```

### Use case 1: team is not specified

- #### A single player initiates a match
Suppose the player A initiates a matchmaking request in which the `team` parameter is left empty, GPM may assign player A to red, blue 1, or blue 2 team. Then, the `team` parameter will be updated to "red_000", "blue_000", or "blue_001".


- #### Multiple players initiate a team match
Suppose players A and B initiate a team matchmaking request in which their `team` parameters are left empty, GPM will assign both players to the same team. Then, their `team` parameters will be both updated to "red_000", "blue_000", or "blue_001".


### Use case 2: team is specified

- #### A single player initiates a match
Suppose the player A initiates a matchmaking request in which the `team` parameter is specified to `red`, GPM will assign the player A to the red team. Then, the `team` parameter will be updated to "red_000".

- #### Multiple players initiate a team match
Suppose both players A and B initiate a team matchmaking request in which their `team` parameters are specified to `blue`, GPM will assign both players to blue 1 or blue 2 team. Then, their `team` parameters will be both updated to "blue_000" or "blue_001".

>! Currently, players cannot specify different teams in a GPM team match.
