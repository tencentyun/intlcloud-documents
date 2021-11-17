Event rule is one of the most basic resource unit in EventBridge. You can configure an event bus to receive events from an event source and use event rules to filter events. This document describes how to create an event rule in the EventBridge console.



## Directions

1. Log in to the EventBridge console and select **[Event Rule](https://console.cloud.tencent.com/eb/rule)** on the left sidebar.
2. At the top of the **Event Rule** list page, select the event bus and region for the event rule to be created.
3. Click **Create Event Rule** and enter the relevant information 
	 - **Event Match**: its specifies what events can be matched. You can customize the event pattern or select an existing template rule.
    For more information on the event pattern, please see [Event Pattern](https://intl.cloud.tencent.com/document/product/1108/42288).
    - **Event Target**: it specifies the triggered target that eventually receives the matched events.
4. Click **OK**.
