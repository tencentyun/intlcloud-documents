>!Since the product logic no longer meets the technical development of game industry, Game Player Matching GPM will be deprecated on June 1st, 2022. Please complete service migration before May 31 , 2022.

### Rule Name
A rule name is defined by the developer to distinguish rules. One rule name can be used repeatedly.

### RuleCode
The auto-generated RuleCode is used to identify a unique rule. RuleCode can be associated with a matchmaking service.

### Rule Script
A rule script in JSON defines how a matchmaking rule is implemented, which is a core part of rules.
	
### Match Name
A match name is defined by the developer to distinguish matchmaking services. One match name can be used repeatedly.

### MatchCode

The auto-generated MatchCode is used to identify a unique matchmaking service, which can be used as a request parameter of the [`StartMatching`](https://intl.cloud.tencent.com/document/product/1072/39904) API.

### Server Queue
A server queue is configured to place the matchmaking result when a matchmaking request is created. After the matchmaking service is completed, GPM will use matchmaking results to request [GSE’s](https://intl.cloud.tencent.com/document/product/1055/36667) server fleet and start a game server session.

### Timeout
A timeout is defined for a match, during which, GPM processes the matchmaking request.

### Notification Address
A notification address is configured to receive the MatchTicket status change when GPM processes a matchmaking request. This notification address helps you track the status and results of your matchmaking requests.

### Custom Data
The custom data is predefined for a matchmaking request, which will be included in the event notification and sent to the address you configured.

### Game Server Session Data
The game server session data is predefined for a matchmaking request to create game server sessions.

### Game Attribute
Game attributes are predefined for a matchmaking request to create game server sessions.

