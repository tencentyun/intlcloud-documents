Node specification management is used to set hardware specifications when adding more core, task, or router nodes. Each node type can have up to 3 specifications and will automatically select the current default specification during scaling. If the current default specification is sold out or unavailable, you can set a new default specification. You are recommended to keep the configuration of resources such as CPU cores, memory size, and disk capacity in the new specification the same as that of the existing nodes for optimal compatibility with current component parameters.

1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and select **Cloud Hardware Management** > **More** > **Set Node Specification** on the left sidebar. The billing mode is pay-as-you-go.
![](https://main.qcloudimg.com/raw/bee79bdccb2bd86d061d1d7f5c712549.png)
2. The default initial specification of the core nodes is the specification selected when the cluster is created. You can set or delete the default one for normal scaling.
3. The task and router nodes have no default specification. Please add the specification as prompted. 
![](https://main.qcloudimg.com/raw/fb5874c67ccafdf8311d980139f8f44d.png)
