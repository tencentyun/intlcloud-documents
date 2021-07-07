
### How does a game client initiate a matchmaking request?

Currently, a matchmaking request can be initiated only by calling the TencentCloud API. You need a server to process matchmaking requests from your players, and call TencentCloud GPM API to initiate matchmaking requests.

### What rule types does GPM support?

Currently, GPM support rule types such as distance, comparison, collection, latency and distance sort. We plan to support more in the future.

### What’s the maximum number of players GPM supports for a single game session?

Currently, GPM supports matching up to 200 players in a single game session for a large match, and up to 40 players for a small match.

### How can I get the matchmaking status and results?
There are two ways to get the matchmaking status and results. We recommend that you use the first method below for better matchmaking performance.
1. Automatic event notifications
2. Manually calling the API for querying matchmaking progress


### How are matchmaking results processed?

GPM can automatically place matchmaking results into GSE to launch game server sessions, or you can process them by yourself.

### Can I use GPM independently?

Yes, you can use GPM independently. However, we recommend that you use it with GSE for increased efficiency.

