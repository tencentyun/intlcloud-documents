 `aid` is a unique ID assigned by the Aegis SDK to each user device. It is stored in the mini program storage and used to distinguish between users for UV calculation. It will be updated only when the user clears the mini program cache.

## Prerequisites
Install and initialize the Aegis SDK in any method as detailed in [Installation and Initialization](https://intl.cloud.tencent.com/document/product/1131/44531).

## aid

You can use the following algorithm to customize the `aid` reporting rules:

<dx-codeblock>
:::  js
aid = 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, (c) => {
const r = (Math.random() * 16) | 0;
const v = c === 'x' ? r : (r & 0x3) | 0x8;
return v.toString(16);
:::
</dx-codeblock>
