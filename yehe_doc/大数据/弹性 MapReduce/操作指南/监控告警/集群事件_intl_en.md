## Feature Overview
Critical changes and exceptions that occur in the cluster are recorded as events. You can query cluster events and configure alarms in Cloud Monitor for severe events to improve your cluster troubleshooting efficiency.

## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select **Cluster List**, and click the ID/Name of the target cluster to enter the cluster details page.
2. On the cluster details page, select **Cluster Monitoring** > **Cluster Event**, where you can directly view all operation events of the current cluster.

The severity levels are as follows:
 - Fatal: exceptional server or service events, which may last a while and may cause service unavailability if no human intervention is conducted.
 - Severe: events of an alerting nature, which haven't caused server or service unavailability yet but will lead to fatal events if left unattended for a long time.
 - General: general events in the cluster, which generally do not need special treatment.
