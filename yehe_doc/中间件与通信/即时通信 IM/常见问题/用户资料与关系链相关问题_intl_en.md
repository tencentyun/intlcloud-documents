### Why do I encounter error code 30001?

There are several possible reasons for the occurrence of error code 30001:
1. A request parameter is invalid.
2. User A initiates a friend request to user B, but user B is already in user A’s friend list.
3. User A initiates a friend deletion request to user B, but user B is not in user A’s friend list.
4. User A initiates a friend update request to update friend B’s relationship chain data, but friend B is not in user A’s friend list.
5. User A initiates a request to fetch the relationship chain data of friend B, but friend B is not in user A’s friend list.
6. User A initiates a blocklist request to user B, but user B is already in user A’s blocklist.
7. User A initiates a request to remove user B from the blocklist, but user B is not in user A’s blocklist.

When the IM backend returns an error code, it also returns the detailed error information, and users can identify the cause of the error based on the error information.

### What should I do if error code 30004/40004 is returned when the RESTful API of the profile/relationship chain system is called?

The request packet of the profile/relationship chain system contains a From_Account field, which is used to indicate the request sender. If the value of the From_Account field in the request packet is inconsistent with the actual sender, the IM backend considers that the request was initiated by the app backend. In this case, the backend checks whether the request sender has app admin permissions. If the actual sender is not an admin, error 30004/40004 is returned.

### How can I configure settings for messages sent by non-friend users?

To allow non-friend users to send messages, disable the relationship chain for one-to-one chat message verification in the [IM console](https://console.cloud.tencent.com/im). To forbid non-friend users to send messages, enable the verification. It takes 5 minutes for the setting to take effect.
