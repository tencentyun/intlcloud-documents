## Overview

This document describes how to create a game server queue. You can use a queue to create a group of cross-region server fleets and place game server sessions in any fleet in the queue, so as to minimize latency, deliver a better player experience, use more fleet capacity more efficiently, provide high capacity for new games more swiftly, and make the game more elastically available.

## Prerequisites

You have completed the [GSE Application Form](https://intl.cloud.tencent.com/apply/p/k0b6pvbhs6) and your application has been approved.


## Directions
1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse/asset) and click **Queue** on the left sidebar.
2. Click **Create** in the top-left corner.
3. Enter information such as [Basic Info](#.E5.9F.BA.E6.9C.AC.E4.BF.A1.E6.81.AF), [Latency Policy](#.E5.BB.B6.E8.BF.9F.E7.AD.96.E7.95.A5), and [Target](#.E7.9B.AE.E6.A0.87).

#### Basic info
 - Identifier: enter a valid identifier.
 - Timeout Allocation: enter the max time that a game server session request can be retained in a multi-region deployment.
![](https://main.qcloudimg.com/raw/2e5f440e4ab642b5e1c4d63255fa275e.png)

#### Latency policy
Set a group of policies for max player latency which increases as the policy priority is lowered. You can use the policies that are executed in priority order to strike a balance between the optimal game experience and the player wait time.
 - **Example**:
	 Define the following policies for a queue whose timeout duration is 30 seconds. Specify the max latency as 60 ms for the first policy, and then keep specifying a greater value for the next policy until the last one (150 ms) which defines the absolute max latency for any player. To ensure all game server sessions are placed regardless of the latency, you can set the max latency to a very high value for the last policy. 	 
  - **Policy settings**:
![](https://main.qcloudimg.com/raw/56520abadad90057ca24f3bd458accc3.png)
   - **Execution result**:
      In this example, the first policy uses the first 10 seconds of the timeout duration to search for a fleet whose latency for any player is below 60 milliseconds. The second policy uses the next 10 seconds to search for a fleet whose latency for any player is below 100 milliseconds. The third policy uses the last 10 seconds to search for a fleet whose latency for any player is below 150 milliseconds. If there are no fleets whose player latency is below the max player latency in a policy, GSE will return the result directly without waiting until the specified timeout in the policy. If there is a fleet whose latency is below the max player latency, but it is not idle, GSE will wait until it times out.
					
#### Target
The target is a list of server fleets where GSE schedules resources. You can specify a fleet with a server fleet ID or alias ID and set the priority for the targets in the queue. If you set both latency policy and target, the latency policy shall prevail. When selecting targets for a queue, please consider the following points:
   - **The priority of targets in the queue really matters.** If you provide latency data in a game server session placement request, GSE will adjust the target priority to find the available resources with the minimum player latency; otherwise, GSE will follow the priority order in the target list, and in this case, game sessions will generally be hosted on the first listed fleet and will be placed on a backup fleet only when necessary.
   - **You can add any existing server fleets or aliases from any region.**
   - **A queue should contain at least two fleets, which should be in at least two different regions if possible,** as this can reduce the impact of regional speed-down of fleets, manage unexpected changes in player needs more efficiently, and make service hosting more elastic.
   - **If you have associated a server fleet with an alias (recommended), you'd better use the alias when setting the fleet as a target in the queue.**
   - **All targets in the queue must run a game asset package compatible with the game clients of this queue.** Please note that new game session requests processed by the queue may be placed on any target in the queue.
   - **You need to determine where in the region your queue is to be created.** Ideally, you can initiate game server session placement requests through a game client service (such as session directory service). To implement this, we recommend you create a queue in a region close to where the client service is deployed, which can minimize the latency in submitting such requests.
![](https://main.qcloudimg.com/raw/52b0ab85b5e3a0dca52b649c70ca96d2.png)

4. Click **OK** to create a game server queue. Once created successfully, you can modify or delete it or perform other operations on the queue list page.





