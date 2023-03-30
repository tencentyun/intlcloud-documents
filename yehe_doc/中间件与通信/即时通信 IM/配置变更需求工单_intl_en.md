> ## How to Submit an IM Configuration Change Ticket
> 1. Go to the [page for submitting an IM ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1).
> 2. Select **Group** under **Problem Types**.
> 3. Enter the information required for the configuration change according to the relevant template under [Templates of IM Configuration Change Ticket](#.E5.8D.B3.E6.97.B6.E9.80.9A.E4.BF.A1-im-.E9.85.8D.E7.BD.AE.E5.8F.98.E6.9B.B4.E9.9C.80.E6.B1.82.E5.B7.A5.E5.8D.95.E6.A8.A1.E7.89.88) , and fill in contact information such as mobile number.
> 4. Click **Submit Ticket**.
> >? After the ticket is submitted, we will process it within one business day.
>
> ## Templates of IM Configuration Change Ticket
>
> ### Frequency control of group messages with different priorities
> > Change type: Frequency control of group messages with different priorities
> > SDKAppID: // SDKAppID of your app in IM
> > Group type: // Group type to be modified, such as Private, ChatRoom, etc.
> > Frequency control of chat messages: // Up to N per second
> > Frequency control of like messages: // Up to M per second
> > Frequency control of member change notifications: // Up to K per second
>
> ### Group downstream messages with custom fields
> > Change type: Group downstream messages with custom fields
> > SDKAppID: // SDKAppID of your app in IM
> > Group type: // Group type to be modified, such as Private, ChatRoom, etc
> > Custom field type: // Custom group member fields or user profile fields
> > The custom field that needs to be carried: // The custom field that has been added in the console. It can carry multiple fields and needs to match with the custom field type.
>
>
> ### Modify group type
> > Change type: Modify group type
> > SDKAppID: // SDKAppID of your app in IM
> > Group type: // Group type, such as Private, ChatRoom, etc.
> > Features to be modified: // Describe the features that need to be changed in detail.
>
>
> ### Periodically kick out offline members in the group
> > Change type: Periodically kick out offline members in the group.
> > SDKAppID: // SDKAppID of your app in IM
> > Group type: // Group type, such as Private, ChatRoom, etc.
> > Whether to allow periodically kicking out offline members: // Yes/No
>
> 
>
> ### Auto repossess group
> > Change type: Auto repossess group
> > SDKAppID: // SDKAppID of your app in IM
> > Group type: // Group type, such as Private, ChatRoom, etc.
> > Group repossessing time (in seconds): // Groups that are inactive during the time will be repossessed. An inactive group is a group in which no messages are sent and no member changes occur.
>
> ### Modify daily group creation quota
> > Change type: Modify daily group creation quota
> > SDKAppID: // SDKAppID of your app in IM
> > The maximum number of newly created groups per day: // Only the newly created groups are included, while deleted groups do not count against the quota.
>
> ### Adjust RESTful API calling frequency
> > Change type: Adjust RESTful API calling frequency
> > SDKAppID: // SDKAppID of your app in IM
> > ServiceName/Command: // The RESTful API called, such as group_svc/get_group_list.
> > Expected maximum frequency: // Up to XXX times per minute. By default, it can be called 6000 times per minute.
>
> ### Enable pushing to all users
> > Change type: Enable the feature of pushing to all users
> > SDKAppID: // SDKAppID of your app in IM, including the official and test SDKAppID
> > Main push types: // Push to all users, push by attribute, or push by tag
> > Application scenario: // Describe in detail. Otherwise, we cannot evaluate whether the requirement is reasonable.
> > Expected call frequency and interval: // By default, it can be called up to 100 times per day, and the interval between two calls must be greater than 1s. If you need to raise the frequency limit, describe your expected call frequency and interval.
> > Whether to store unread messages: // If the account is offline during the push of a message, whether you need to pull this unread message upon next login.
> > [](id:community)
> ### Enable community creation feature
> > Change type: Enable community creation feature
> > SDKAppID: // SDKAppID of your app in IM, including the official and test SDKAppID
> > Application scenario: // Describe in detail. Otherwise, we cannot evaluate whether the requirement is reasonable.
