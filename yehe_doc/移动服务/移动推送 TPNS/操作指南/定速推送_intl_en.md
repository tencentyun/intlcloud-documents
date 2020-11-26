
The fixed-speed push feature is to solve the problem where TPNS may push messages so fast that some customer servers experience too much connection pressure. TPNS provides API settings to allow you to control the push speed according to your own server conditions.
## Scenarios
- Scenario 1:
You want to push a promotional message to all users, but there is a limit on the number of concurrent visitors on the event page; therefore, you want to control the push speed in order to reduce the connection pressure on your server. In this case, you can set fixed-speed push to limit the number of users allowed to open the event page simultaneously.
- Scenario 2:
You have tagged a group of users as "lost users" and want to push a "benefit claim" message to them, so that they will be attracted to open your app; however, you don't want too many users to visit the event page at the same time. In this case, you can set fixed-speed push to limit the number of users allowed to open the event page simultaneously.

## Directions
### Console
Go to **Message Push** > **Create Push** > **Advanced Settings** in the [console](https://console.cloud.tencent.com/tpns), enable fixed-speed push, and select a push speed.

After fixed-speed push is enabled, the message will be pushed to devices that match the push target at the selected speed.
>
>- Only push to all devices and push by tag support fixed-speed push.
>- The push speed can range from 1,000 to 50,000 pushes per second.

### RESTful API
Set the optional `push_speed` parameter for the RESTful API to implement fixed-speed push. For more information, please see [Push API Parameter Description](https://intl.cloud.tencent.com/document/product/1024/33764).
Below is a sample push:
```
{
   "audience_type": "tag",
    "tag_list": {
        "tags": [
            "tag1",
            "tag2"
        ],
        "op": "AND"
    },
	"push_speed":50000,
    "message_type": "notify",
    "message": {
        "title": "Push title",
        "content": "Push content",
        "android": {
        	 "custom_content":"{\"key\":\"value\"}"
        }
    }
}
```
