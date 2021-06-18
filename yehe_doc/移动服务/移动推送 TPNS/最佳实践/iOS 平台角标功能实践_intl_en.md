TPNS provides a series of badge control methods. The following introduces how to implement the badge feature in two classic scenarios.
This document describes iOS badge best practices. For Android badge adaptation, see [here](https://intl.cloud.tencent.com/document/product/1024/35828).

## Scenario 1: Clearing the Application's Badge Number and Notification Bar Messages When Opening the Application

### Scenario description

- When the application is not started, make the badge number equal the number of the application's push messages received by the current device.
- When the application enters the foreground, set the badge number to 0, clear notification bar messages, and set the badge number in the cloud to 0.

### Implementation method

For such a scenario, the badge number auto increase scheme is recommended. The process is as follows:
**Step 1:** when a push task is created via the [push API](https://intl.cloud.tencent.com/document/product/1024/33764), set `badge_type` to `-2` to enable the application's badge number to automatically increase by 1.
**Step 2:** when the application is started, call the "clearing the application's badge number and notification bar messages" method to clear the local badge number and notification bar messages. The implementation code is as follows:
![](https://main.qcloudimg.com/raw/076ca2d56865d332b0821dca8ffcfdbb.png)
**Step 3:** clear the badge number in the cloud. The implementation code is as follows:
![](https://main.qcloudimg.com/raw/64bd9d0160d2a31bb60f70524c2f3e6e.png)
**Step 4:** if the badge number in the cloud needs to be updated, call the following API to sync the badge value to the TPNS server, and the badge value will be used as the benchmark for the next push. For example, if the current TPNS server badge value is synchronized as N, then the application's badge value will be N+1 when the next push is received.
```
//Sync the badge value to the TPNS server, and the value will be used as the benchmark for the next push
- (void)setBadge:(NSInteger)badgeNumber;
```

>! 
> 1. The `setBadge` method relies on the TPNS channel to implement badge value sync. When the application enters the background, the TPNS channel will be disconnected, and calling the `setBadge` method will fail. In this case, only the custom badge number scheme is applicable.
> 2. When the application enters the foreground, the TPNS channel will try to reconnect, and calling the `setBadge` method will fail before the connection is resumed. In this case, only the custom badge number scheme is applicable.
> 3. When the application is cold started, `setBadge` must be used in the callback of the registration method.
> 4. For more information on how to listen for TPNS network connection status, please see [here](#dayi4).


## Scenario 2: Enabling the Badge Number to Be the Sum of Notification Bar Messages and In-App Messages

### Scenario description
**Application's badge number = Number of notification bar messages + Number of in-app messages.** When a user clicks a notification to start the application, the number of notification bar messages changes, and the application's badge number needs to be updated.
In this scenario, developers need to maintain the device's total number of messages (including the number of notification bar messages and the number of in-app messages).

### Implementation method
1. Obtain the number of notification bar messages. The code is as follows:
```
//Obtain the number of notification bar messages
[[UNUserNotificationCenter currentNotificationCenter] getDeliveredNotificationsWithCompletionHandler:^(NSArray<UNNotification *> *notifications) {
NSLog(@"notifications count:%d.",notifications.count);
}];
```
2. Assume that the number of notification bar messages is a and the number of in-app messages is b. The code for setting the application's badge number is as follows:
```
//Set the application's badge number
[XGPush defaultManager].xgApplicationBadgeNumber = a + b;
```
<span id="zidy"></span>
3. Use the **custom badge number** scheme (recommended). The method is as follows:
When a push task is created via the [push API](https://intl.cloud.tencent.com/document/product/1024/33764), set `badge_type` to the total number of messages (a custom badge number that is greater than or equal to 0). For example, if the total number of messages is 10, set `badge_type` to `10`.


## FAQs
#### How to clear the badge number but retain the push notifications in the notification center?
```
//Do not display the number of pushes in the application icon, but retain the push notifications in the system notification bar
+ (void)resetBageNumber{
    if(APNS_IS_IOS11_LATER){
        //For iOS 11 or later, you only need to set `badgeNumber` to `-1`
        [UIApplication sharedApplication].applicationIconBadgeNumber = -1;
    }else{
        UILocalNotification *clearEpisodeNotification = [[UILocalNotification alloc] init];
        clearEpisodeNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:(0.3)];
        clearEpisodeNotification.timeZone = [NSTimeZone defaultTimeZone];
        clearEpisodeNotification.applicationIconBadgeNumber = -1;
        [[UIApplication sharedApplication] scheduleLocalNotification:clearEpisodeNotification];
    }
}
```

#### How to delete a specific notification from the notification center?

```
//objectID: push ID of the notification to delete
- (void)removeNotificationsForObjectID:(ObjectID *)objectID {
    __weak __typeof(self) weakSelf = self;
    [[UNUserNotificationCenter currentNotificationCenter] getDeliveredNotificationsWithCompletionHandler:^(NSArray<UNNotification *> *notifications) {
        __strong __typeof(weakSelf) self = weakSelf;
        NSMutableArray <NSString *> *identifiersToRemove = [@[] mutableCopy];
        for (UNNotification *notification in notifications) {
            //Filter the notification that meets the deletion criteria
            ObjectID *objectIDFromNotification = [self marshalNotification:notification];
            if ([objectID isEqual:objectIDFromNotification]) {
                [identifiersToRemove addObject:notification.request.identifier];
            }
        }
        [[UNUserNotificationCenter currentNotificationCenter] removeDeliveredNotificationsWithIdentifiers:identifiersToRemove];
    }];
}
```
>! This method applies only to iOS 10 and later.
>

#### How to update only the application's badge number when the application is not started?

Use the [custom badge number scheme](#zidy) to create a push with only a badge number but without content.


<span id="dayi4"></span>
#### How to listen for TPNS network connection status?
For SDK v1.3.1.0 or later, the recommended method is as follows:
```
// TPNS network connected
- (void)xgPushNetworkConnected;
// TPNS network disconnected
- (void)xgPushNetworkDisconnected;
```

#### How to keep the badge number unchanged when I create a push via the [push API](https://intl.cloud.tencent.com/document/product/1024/33764)?
Set `badge_type` to `-1` to make the badge number remain unchanged.

