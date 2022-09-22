## Binding an Account

### API Description

This API is used to register an application with a specified account so that the backend can send push messages to the specified account. There are two versions of the API method:

```java
Recommended for applications with an account system. This API will override all accounts previously bound to the device of the current account type, and only the current registered account will take effect.
void clearAndAppendAccount(Context context, String account, int accountType, XGIOperateCallback callback)
Recommended for applications with an account system. This API will override all accounts previously bound to the device of the current account type, and only the current registered account will take effect. There is no registration callback.
void clearAndAppendAccount(Context context, final String account, int accountType)
```

> ?
>
> - As the `appendAccount` API was seldom used and confusing to developers, it has been disused since October 26, 2020. If you have used it before, it will be replaced by the `clearAndAppendAccount` API.
> - Each account can be bound to up to 100 tokens.
> - The account can be email, QQ account number, mobile number, username, etc. For valid values, please see [Account Type Value Table](https://intl.cloud.tencent.com/document/product/1024/40598).
> - If multiple devices are bound to the same account, the backend will push the message to the last bound device by default. If you want to push to all the bound devices, you can view the `account_push_type` parameter settings in [Push API](https://intl.cloud.tencent.com/document/product/1024/33764).



### Parameter description

- context: context object of the current application, which cannot be null.
- account: account.
- accountType: account type of the account. For valid values, please see the enumeration class `XGPushManager.AccountType`.

### Sample code

```java
XGPushManager.clearAndAppendAccount(context, "1369999999", XGPushManager.AccountType.PHONE_NUMBER.getValue());
```
### Getting the binding result

Use the Callback version of the binding API.
The `XGIOperateCallback` class provides an API to process success or failure. Please see the description of the account binding API.

Sample code:

```java
public interface XGIOperateCallback {

    /**
     * Callback when the operation is successful
     * @param data //Business data of a successful operation, such as the token information when registration is successful
     * @param flag //Flag tag
     */
    public void onSuccess(Object data, int flag);
    
    /**
     * Callback when the operation fails
     * @param data //Business data of a failed operation
     * @param errCode //Error code
     * @param msg //Error message
     */
    public void onFail(Object data, int errCode, String msg);
}
```

## Deleting Tags

> ? The `delTag` API is disused in SDK v1.2.3.0. The `delTags` API is recommended.

### API Description

This API is used to delete user tag data.

```java
public static void delTag(Context context, String tagName)
```

### Parameter description

- context: `Context` object.
- tagName: name of the tag to be set, which cannot be null or empty.

### Processing result

The result can be obtained by reloading the `onDeleteTagResult` method of `XGPushBaseReceiver`.

### Sample code

```java
XGPushManager.delTag (this, "male");

```
