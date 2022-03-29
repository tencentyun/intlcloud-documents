>!Since the product logic no longer meets the technical development of game industry, Game Player Matching GPM will be deprecated on June 1st, 2022. Please complete service migration before May 31, , 2022.
This document describes GPM’s MatchTicket parameters. For more information about relevant concepts, see [Glossary](https://intl.cloud.tencent.com/document/product/1072/38351#P).

## Status

MatchTicket status changes during the lifecycle of a matchmaking request. The updated status will be recorded in the **Status** parameter.

#### MatchTicket statuses

- **SEARCHING**: MatchTicket in this status indicates that GPM is searching for other satisfactory tickets in the match pool to be matched to this MatchTicket within the timeout period. If no ticket is found during this period, the MatchTicket status will change to **TIMEDOUT**.
- **PLACING**: MatchTicket in this status indicates that GPM is placing the matchmaking result of a complete match to the Tencent Cloud Game Server Engine (GSE) to start a new game server session in GSE. Only MatchTickets with a MatchCode configured to request resources from GSE will be in this status.
- **COMPLETED**: MatchTicket in this status indicates that a satisfactory match is completed, and its lifecycle in GPM ends.
    - For a MatchTicket without requesting battle server resources, this status indicates that the matchmaking request is completed.
    - For a MatchTicket automatically requiring battle server resources from GSE, this status indicates that the matchmaking request is completed and the matchmaking result is placed to the specified GSE server queue.
- **CANCELLED**: MatchTicket in this status means that the user cancels the matchmaking request at the **SEARCHING** stage.
- **TIMEDOUT**: MatchTicket in this status indicates that no satisfactory tickets are found for the matchmaking request within the specified timeout period at the **SEARCHING** stage. TimeOut is a MatchCode parameter that is defined when [a match is created](https://intl.cloud.tencent.com/document/product/1072/39203).
- **FAILED**: MatchTicket in this status indicate that the matchmaking request fails due to internal error at the **SEARCHING or PLACING** stage.



## MatchResult Fields

- If the value of **`MatchType` is `NORMAL`, the MatchResult fields should be parsed as follows**:
    - **Parameters**
<table>
<thead>
<tr>
<th align="left">Field</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">MatchedPlayers</td>
<td>Array of MatchedPlayer</a></td>
<td>Players matched to a game battle</td>
</tr>
</tbody></table>
    - **Sample code**
```json
"MatchResult": "{\"MatchedPlayers\":[{\"PlayerId\":\"xxxx\", \"PlayerSessionId\":\"\", \"MatchTicketId\":\"xxxxxxx\"}, {\"PlayerId\":\"xxxxx\", \"PlayerSessionId\":\"\", \"MatchTicketId\":\"xxxxxxx\"}]}"
```

- If the value of **`MatchType` is `GSE`, the MatchResult fields should be parsed as follows**:
    - **Parameters**
<table>
<thead>
<tr>
<th align="left">Field</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">MatchedPlayers</td>
<td>Array of MatchedPlayer</a></td>
<td>Players matched to a game battle</td>
</tr>
<tr>
<td align="left">DnsName</td>
<td>string</td>
<td>DNS flag returned from GSE. This field may be empty.</td>
</tr>
<tr>
<td align="left">GameServerSessionId</td>
<td>string</td>
<td>Game server session ID returned from GSE</td>
</tr>
<tr>
<td align="left">IpAddress</td>
<td>string</td>
<td>IP address returned from GSE</td>
</tr>
<tr>
<td align="left">Port</td>
<td>number</td>
<td>Port number returned from GSE</td>
</tr>
</tbody></table>
    - **Sample code**
```json
"MatchResult": "{\"DnsName\":\"\", \"GameServerSessionId\":\":gameserversession/fleet-xxx\", \"IpAddress\":\"xx.xx.xx.xx\", \"Port\":xxx, \"MatchedPlayers\":[{\"PlayerId\":\"xxx\", \"PlayerSessionId\":\"psess-xxxxxx\", \"MatchTicketId\":\"xxx\"}, {\"PlayerId\":\"xxx\", \"PlayerSessionId\":\"psess-xxxxxxx\", \"MatchTicketId\":\"xxxxxxx\"}]}"
```


- **MatchedPlayer**
<table>
<thead>
<tr>
<th align="left">Field</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">PlayerId</td>
<td>string</td>
<td>Player ID, which is passed in when a match is initiated.</td>
</tr>
<tr>
<td align="left">PlayerSessionId</td>
<td>string</td>
<td>Player session ID returned from GSE. This field is empty if the value of MatchType is `NORMAL`.</td>
</tr>
<tr>
<td align="left">MatchTicketId</td>
<td>string</td>
<td>MatchTicket ID of the current players.</td>
</tr>
</tbody></table>


