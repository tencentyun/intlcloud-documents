
The Custom Push Speed feature is to solve the problem where TPNS may push messages so fast that some customer servers experience too much connection pressure. TPNS provides API settings to allow you to control the push speed according to your own server conditions.
## Scenarios
- Scenario 1:
You want to push a promotional message to all users, but there is a limit on the number of concurrent visitors on the event page; therefore, you want to control the push speed in order to reduce the connection pressure on your server. In this case, you can set a push speed to limit the number of users allowed to open the event page simultaneously.
- Scenario 2:
You have tagged a group of users as "lost users" and want to push a "benefit claim" message to them, so that they will be attracted to open your app; however, you don't want too many users to concurrently visit the event page. In this case, you can set a push speed to limit the number of users allowed to open the event page simultaneously.

## Directions
### Using the console
1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns).
2. Go to **Push Management** > **Task List**.
3. Click **Create Push**, expand the **Advanced** section, enable **Custom Push Speed**, and set a speed.

After Custom Push Speed is enabled, the message will be pushed to devices that match the push target at the set speed.
>?
> - Only push to all devices and push by tag support Custom Push Speed.
> - The push speed can range from 1,000 to 50,000 pushes per second.
> 

### Using RESTful APIs
When calling the RESTful API, you can set the `push_speed` parameter to push messages at a custom speed. For more information, see the **Optional Parameters** section in [Push API](https://intl.cloud.tencent.com/document/product/1024/33764).
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
        "Title": "Push title",
        "content": "Push content",
        "android": {
        	 "custom_content":"{\"key\":\"value\"}"
        }
    }
}
```
