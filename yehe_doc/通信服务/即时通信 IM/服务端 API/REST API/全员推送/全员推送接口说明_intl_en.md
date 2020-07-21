## About Pushing to All Users
The service of pushing to all users is a set of RESTful APIs implemented on the basis of the IM communication architecture. This service is used to support the message push needs of apps, such as pushing to all users, pushing by tag, and pushing by attribute. Clients can receive messages pushed online and offline (Android backend notifications and APNs) through the SDK.

>!
>- To use the service of pushing to all users, you must have logged in to your account before or have manually imported the account.
>- This feature **can only be applied for by Ultimate Edition users (but not by Pro Edition users). You can apply for this feature by submitting a ticket, and we will evaluate your needs for approval. If we determine that this feature suits your needs, we will approve your application so that you can use the feature**.

## Basic Capabilities of Pushing to All Users

- Supports pushing messages to all users in the app.
- Supports pushing messages based on a specified user tag.
- Supports pushing messages based on a specified user attribute.

## Strengths

The service of pushing to all users is based on the client IM SDK and IM backend, which ensure messaging capabilities and system reliability:

- By using the IM SDK, this service ensures that messages can reach their targets and provides message broadcasting capabilities for apps.
- This service allows you to set up to 10 push attributes for each user. These attributes can be set separately without affecting each other.
- For the feature of pushing by attribute, you can use the AND or OR logic to connect multiple attributes.
- For the feature of pushing by tag, you can use the AND or OR logic to connect multiple tags.
- You can configure this service to push messages to only online users and store messages offline for up to 7 days.
- This service supports custom messages.

## Sample Application Scenarios
### Sample scenarios for pushing to all users
1. Assume that a game app plans to launch a promotion event on Christmas and wants to push messages to all users. To do this, the app can use the service of pushing to all users. In addition, to inform more users of this event, it can set the offline message storage period so that users who are offline during the message push can still receive the pushed messages when they log in within the offline message storage period. In this way, the service enhances the effectiveness of the promotional event.
2. Assume that a livestreaming app plans to launch a massive live marketing event and needs to push notifications to all users. To do this, the app can use the service of pushing to all users seven days before the event and set the offline message storage period to seven days. When the event begins, the app can also push messages to all users without setting an offline message storage period. In this way, online users will receive notifications about the start of the event, and more users will be attracted to the livestreaming room.
3. In a livestreaming app, a user purchases and uses a megaphone tool. At this time, the app can use the service of pushing to all users without setting an offline message storage period. In this way, all other online users will receive the message broadcast by this user.

### Sample scenario for pushing by user tag
For example, a financial product plans to push a financial management service to users who follow "stock A" or "stock B". For that purpose, the product can use the feature of pushing by tag:

1. When a user follows "stock A" or "stock B", call the tag addition API to add the corresponding tag to the user.
2. When a user unfollows "stock A" or "stock B", call the tag deletion API to delete the corresponding tag of the user.
3. In the push API, set the push tag condition to "stock A" or "stock B" (that is, by using the TagsOr feature), so that all users who follow either "stock A" or "stock B" will receive pushed messages.


### Sample scenario for pushing by user attribute
For example, assume that the members of a game are classified into the following types: non-member, ordinary member, gold member, and platinum member. If operational personnel plan to push an event to platinum members in Shenzhen, they can use the feature of pushing by attribute as follows:

1. Set app attribute names. In this example, two user attributes are used: member level and city. Then, set attribute 0 as the member level and attribute 1 as the city.
2. When a user’s member level changes (for example, the user’s membership expires or the user pays to become a member), call the API for setting user attributes to modify the member level attribute of the user. For example, when a user pays to become a gold member, set the user’s member level attribute to "Gold Member".
3. When a user changes his or her city information, call the API for setting user attributes to modify the city attribute of the user. For example, when a user changes his or her city from Beijing to Shanghai, set the user’s city attribute to "Shanghai".
4. During the operational event, call the push API and set the push attribute conditions as follows: "Member Level" = "Platinum Member"; "City" = "Shenzhen". In this way, all platinum members in Shenzhen will receive the pushed messages.

>! For the preceding scenario, pushing by attribute is more suitable than pushing by tag. This is because when users change their city from Shenzhen to Guangzhou, you need to first delete the "Shenzhen" tag and then add the "Guangzhou" tag, which requires two API calls. In comparison, by using pushing by attribute, you can modify the city attribute directly with a single API call.

## Scenarios Unsuitable for Message Push and Suggestions
This service is not suitable for high-frequency message sending. We recommend that you use pushing to all users, pushing by attribute, and pushing by tag for low-frequency marketing event notifications.

## Related APIs
- [Pushing to All Users](https://intl.cloud.tencent.com/document/product/1047/37166) 
- [Setting App Attribute Names](https://intl.cloud.tencent.com/document/product/1047/37167) 
- [Obtaining App Attribute Names](https://intl.cloud.tencent.com/document/product/1047/37168) 
- [Setting User Attributes](https://intl.cloud.tencent.com/document/product/1047/37170)  
- [Deleting User Attributes](https://intl.cloud.tencent.com/document/product/1047/37171)  
- [Obtaining User Attributes](https://intl.cloud.tencent.com/document/product/1047/37169)  
- [Adding User Tags](https://intl.cloud.tencent.com/document/product/1047/37173)  
- [Obtaining User Tags](https://intl.cloud.tencent.com/document/product/1047/37172)  
- [Deleting User Tags](https://intl.cloud.tencent.com/document/product/1047/37174)  
- [Deleting All Tags of a User](https://intl.cloud.tencent.com/document/product/1047/37175)  
