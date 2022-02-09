`aid` is a unique ID assigned by the Aegis SDK to each user device. It is stored in the `localStorage` of the browser and used to distinguish between users for UV calculation. It will be updated only when the user clears the browser cache.

## Prerequisites
Install and initialize the Aegis SDK in any method as detailed in [Installation and Initialization](https://intl.cloud.tencent.com/document/product/1131/44519).

## aid

You can use the following algorithm to customize the `aid` reporting rules:

<dx-codeblock>
:::  js
async getAid(callback: Function) {
// In some cases, an error will occur when `localStorage` is manipulated
  try {
    let aid = await localStorage.getItem('AEGIS_ID');
    if (!aid) {
    aid = 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, (c) => {
      const r = (Math.random() * 16) | 0;
      const v = c === 'x' ? r : (r & 0x3) | 0x8;
      return v.toString(16);
    });
    localStorage.setItem('AEGIS_ID', aid);
    }
    callback?.(aid || '');
  } catch (e) {
    callback?.('');
  }
}
:::
</dx-codeblock>


>?To use the `aid` constructed by yourself as a reporting rule, you need to configure an `aid` verification rule in the format of `/^[@=.0-9a-zA-Z_-]{4,36}$/` on the backend. 
