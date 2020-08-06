You can log in to the [IM Console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app, where you can **upgrade**, **downgrade**, or **disable** it. For a comparison of basic billing plans of IM, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1047/34349).


## Upgrading Your App
Upgrade is only available when the service version of your app is **IM**. The upgrade operation allows you to upgrade the service version, enable an unlimited number of audio-video chat rooms, enable content filtering, increase the maximum number of groups a single user can join, and increase the maximum number of members in a single group. The upgraded features may incur corresponding fees, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) to learn more.

1. Log in to the [IM Console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
2. In the **Service Version** area, click **Upgrade**. The **Upgrade Reminder** dialog appears.
3. Set the following value-added items as needed and click **OK**.
  <table>
     <tr>
         <th nowrap="nowrap">Value-added Item</th>  
         <th>Pro Edition</th>  
         <th>Flagship Edition</th>  
     </tr>
	 <tr>      
         <td>Service Version</td>
	 <td colspan="2">Select **Pro Edition** or **Flagship Edition**. The upgraded plan takes effect immediately and is pay-as-you-go on a monthly basis. No fees will be incurred until the first day of the next month after the plan is activated. Standard billing plan fees are recorded in the bill generated on the third day of every month.</td>   
     </tr> 
	 <tr>      
         <td nowrap="nowrap">Unlimited number of audio-video chat rooms</td>   
	 <td><ul><li>Enabled: this feature allows a single Pro Edition app to create an unlimited number of audio-video chat rooms and incurs value-added service fees once enabled.</li><li>Disabled: a single Pro Edition app can create up to 50 audio-video chat rooms.</li></ul></td>   
	     <td>Not supported</td>   
     </tr> 
	 <tr>      
         <td nowrap="nowrap">Enabling content filtering</td>   
	 <td colspan="2"><ul><li>Enabled: custom words libraries in Chinese and English are supported. The number of filter operations is not limited. This feature incurs value-added service fees once enabled.</li><li>Disabled: the feature is disabled by default.</li></ul></td>      
     </tr> 
	 <tr> 
	     <td nowrap="nowrap">Increasing the maximum number of groups a single user can join</td>   
	     <td>By default, the maximum number of groups a single user can create and join is 500. A larger number can be set if needed, and you will incur value-added service fees when the number is over 500.</td>   			    
	     <td>The default maximum number of groups a single user can create and join is 1,000. A larger number can be set if needed, and you will incur value-added service fees when the number is over 1,000.</td>   
     </tr> 
	 <tr> 
	     <td>Increasing the maximum number of members in a single group</td>   
	     <td>The default maximum number of members in a single group is 200, which only applies to private groups, public groups, and chat rooms and is subject to the limitations of the <a href="https://intl.cloud.tencent.com/document/product/1047/33515">features</a> of each group type. A larger number can be specified if needed, and you will incur value-added service fees when the number is over 200 per group.</td>
	     <td>The default maximum number of members in a single group is 2,000, which only applies to private groups, public groups, and chat rooms and is subject to the limitations of the <a href="https://intl.cloud.tencent.com/document/product/1047/33515">features</a> of each group type. A larger number can be specified if needed, and you will incur value-added service fees when the number is over 2,000 per group.</td>
   </tr> 
</table>

3. Click **OK** to complete the upgrade.
 When the upgrade succeeds, the **service version** of the app becomes **Pro Edition-Postpaid** or **Flagship Edition-Postpaid**. To adjust the configuration, you can go to the console and perform the **change configuration** or **disable** operation.

>If you have only upgraded the service version without adjusting other value-added service plans, the existing audio-video chat rooms, ordinary groups, and the groups created or joined by users will not be affected. However, the new audio-video chat rooms, groups, or the groups your users subsequently create or join will be subject to the limitations of the relevant service version. You will receive [error code](https://intl.cloud.tencent.com/document/product/1047/34348) messages once any of the limitations are exceeded.

## Changing Configuration
You can change the configuration when the service version of your app is **Pro Edition-Postpaid** or **Flagship Edition-Postpaid**. The change configuration operation allows you to change the service version, enable an unlimited number of audio-video chat rooms, enable content filtering, increase the maximum number of groups a single user can join, and increase the maximum number of members in a single group. The changed features may incur corresponding fees, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) to learn more.
>
>- You can change the service version and each value-added service plan of your app once every calendar month.
>- A change configuration operation that is performed in the same month in which the service version is adjusted takes effect immediately and does not incurs fees until the first day of the next month. A change configuration operation that is performed in the month after service version adjustment or later takes effect and incurs fees immediately.
For example, assume you changed the service version of your app to **Pro Edition-Postpaid** on February 10, 2019.
Scenario 1: if you upgraded the configuration to enable audio-video chat rooms on February 15, 2019 and then disabled it on February 25, 2019, no fees related to audio-video chat rooms are incurred.
Scenario 2: if you upgraded the configuration to enable audio-video chat rooms on February 15, 2019 and keep it enabled, you will be charged for audio-video chat rooms from March 2019 and receive the bill on April 1, 2019.
Scenario 3: you did not change the configuration in February 2019 or you changed the configuration in February 2019 but restored it in the same month. If you then upgrade the configuration to enable audio-video chat rooms on April 1, 2019, you will be charged for audio-video chat rooms from April 2019 and receive the bill on May 1, 2019.

1. Log in to the [IM Console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
2. In the **Service Version** area, click **Change Configuration**. The **Change Configuration Reminder** dialog appears.
3. Set value-added items such as **service version**, **enabling content filtering**, **increasing the maximum number of groups a single user can join**, and **increasing the maximum number of members in a single group** as needed and click **OK**.
4. Click **OK** to complete the change configuration operation.



>After your app changes to Trial Edition, the existing audio-video chat rooms, ordinary groups, and the groups created or joined by users will not be affected. However, the new audio-video chat rooms, groups, or the groups your users subsequently create or join will be subject to the limitations of the Trial Edition. You will receive [error code](https://intl.cloud.tencent.com/document/product/1047/34348) messages once any of the limitations are exceeded.

## Disabling Your App
**Once your app is disabled, all the services under the app become inactive immediately and cannot be restored, so proceed with caution.**

1. Log in to the [IM Console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
2. In the **Service Version** area, click **Disable**. The **Disable Reminder** dialog appears.
3. Click **OK**, and your app is disabled immediately and cannot be restored.
