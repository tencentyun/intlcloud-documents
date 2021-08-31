## Push to All Users Overview
The push to all users service is a group of RESTful APIs implemented based on the IM communication architecture. This service is used to meet message push requirements of the application, including pushing messages to all users, pushing messages by tag, and pushing messages by attribute. Clients can receive pushed messages by using the online and offline push features (Android background notifications and APNs) of the SDK. The group push service also supports offline storage of messages, helping operators achieve their operational goals more efficiently.

>!
>- An account can receive messages pushed to all users only after it has been logged in to or manually imported.
>- This service **is available only to users of the Ultimate Edition (it becomes unavailable if you are downgraded to the Pro Edition). You can apply for this service by submitting a ticket. After your application is submitted, we will assess your need. Your application will be approved only if we think this service is appropriate for your situation.

## Basic Features

- Push messages to all users of the application.
- Push messages by user tag.
- Push messages by user attribute.

## Strengths

The group push service is provided based on the client IM SDK and IM backend, which guarantee messaging capabilities and system availability.

- Message delivery is guaranteed based on the IM SDK, and the service provides simple message broadcasting capabilities for applications.
- You can set up to 10 push attributes for each user. Each attribute can be set separately without affecting the others.
- The service pushes messages based on multiple attributes connected by AND or OR logic.
- The service pushes messages based on multiple tags connected by AND or OR logic.
- The service pushes messages only to online users and retains messages offline for up to 7 days.
- You can customize messages.
- You can specify the sender account.

## Use Cases
### Pushing messages to all users
Example 1: a game application plans to provide special offers on Christmas and needs to push the notification to all users. In this case, the group push service can be used to boost efficiency. In addition, to inform more users of this promotion, you can set the offline message retention period. In this way, even if some users are not online when the message is pushed, they can still receive the message when they go online within this offline retention period. This improves the quality and effectiveness of the promotion.
Example 2: a livestreaming application plans to launch a large-scale live marketing activity and needs to push the notification to all users. In this case, you can push the notification to all users starting 7 days before the activity and set the offline message retention period to 7 days. When the activity starts, you can push the notification to all users again, without specifying an offline retention period. In this way, all online users can receive the notification and join the live room, attracting more users into the live room.

### Pushing messages to users by user tag
For example, a financial product plans to push a financial planning service to users who follow "stock A" or "stock B". In this case, you can push messages by tag:

1. When a user follows "stock A" or "stock B", add the corresponding tag to the user by calling the API for adding tags.
2. When a user unfollows "stock A" or "stock B", delete the corresponding tag of the user by calling the API for deleting tags.
3. Set the push condition to "stock A" or "stock B" (by using the TagsOr feature) in the API for pushing messages. In this way, all users that follow "stock A" or "stock B" can receive the messages.


### Pushing messages by user attribute
For example, users of a game are classified into non-members, ordinary members, gold members, and platinum members. Assume the operator plans to push an activity to platinum members in Shenzhen. In this case, they can push the message by attribute:

1. Set the application attribute names. In this example, the game users have two attributes: membership tier and city. You can set attribute 0 as the membership tier and attribute 1 as the city.
2. When the membership tier of a user changes (for example, when the membership expires or the user purchases a membership), modify the membership tier attribute of the user by calling the API for setting user attributes. For example, when a user purchases a gold membership, set the membership tier attribute of the user to "gold member".
3. When the city where a user is located changes, modify the city attribute of the user by calling the API for setting user attributes. For example, when the city changes from Beijing to Shanghai, set the city attribute of the user to "Shanghai".
4. During the activity, you can call the push API and set the membership tier attribute to platinum and the city attribute to Shenzhen. Then, all platinum members in Shenzhen will receive the pushed message.

>! In this scenario, pushing by attribute is preferable to pushing by tag. If you push the message by tag, when the city of the user changes from Shenzhen to Guangzhou, the application needs to delete the "Shenzhen" tag of the user and then add the "Guangzhou" tag, which involves two API calls. However, if you push the message by attribute, only one API call is required to modify the city attribute of the user.

## Related APIs
- [Pushing Messages to All Users](https://intl.cloud.tencent.com/document/product/1047/37166) 
- [Setting Application Attribute Names](https://intl.cloud.tencent.com/document/product/1047/37167) 
- [Obtaining Application Attribute Names](https://intl.cloud.tencent.com/document/product/1047/37168) 
- [Setting User Attributes](https://intl.cloud.tencent.com/document/product/1047/37170)  
- [Deleting User Attributes](https://intl.cloud.tencent.com/document/product/1047/37171)  
- [Obtaining User Attributes](https://intl.cloud.tencent.com/document/product/1047/37169)  
- [Adding User Tags](https://intl.cloud.tencent.com/document/product/1047/37173)  
- [Obtaining User Tags](https://intl.cloud.tencent.com/document/product/1047/37172)  
- [Deleting User Tags](https://intl.cloud.tencent.com/document/product/1047/37174)  
- [Deleting All Tags for Users](https://intl.cloud.tencent.com/document/product/1047/37175)  
