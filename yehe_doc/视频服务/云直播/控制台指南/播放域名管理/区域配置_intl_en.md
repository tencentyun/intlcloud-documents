To use content delivery, acceleration, and playback services in a different region, you can change the acceleration region for your playback domain in the CSS console.

## Prerequisites
- You have logged in to the [CSS console](https://console.tencentcloud.com/live).
- You have added a **playback domain name**. 
>? You need to select an acceleration region such as **Chinese mainland** when adding a playback domain.

![](https://qcloudimg.tencent-cloud.cn/raw/1915d256b28e4e9a6b997ae464326b8a.png)

## Notes
- **CSS pricing differs inside and outside the Chinese mainland. For details, see [Pricing Overview](https://intl.cloud.tencent.com/document/product/267/2819).**
- A playback domain cannot be used outside its acceleration region.
- If the accelerated region includes the Chinese mainland, you need to apply for ICP filing for your playback domain.
- Changing the acceleration region will reset the bandwidth cap. You need to configure it again.

## Directions
1. Go to [Domain Management](https://console.tencentcloud.com/live/domainmanage). Click the name of your playback domain or **Manage** on the right.
2. Select the **Advanced Configuration** tab and find **Region configuration**.
3. Click **Edit**. In the pop-up window, you can change the acceleration region to **Chinese mainland**, **Global**, or **Outside Chinese mainland**.
4. Click **Save**.
    ![](https://qcloudimg.tencent-cloud.cn/raw/7d6d384588bedb5f51fe54dc5b13dd9e.png)

| Acceleration Region            | ICP Filing Required | Description                                                       |
| ------------------- | ------------ | ---------------------------------------------------------- |
| Chinese mainland    | Yes | Cannot handle requests outside the Chinese mainland.                 |
| Global            | Yes | Acceleration is supported globally, but prices differ inside and outside the Chinese mainland.               |
| Outside Chinese mainland | No | Cannot handle requests inside the Chinese mainland. Prices differ inside and outside the Chinese mainland. |
