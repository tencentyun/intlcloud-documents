<span id="que1"></span>
### How do I add a domain name to CSS?

1. Log in to the [CSS Console](https://console.cloud.tencent.com/live) and enter **Domain Management**.
2. Add your own push or playback domain name. For more information, please see [Adding Domain Name](https://intl.cloud.tencent.com/document/product/267/35970).
3. Configure CNAME. For more information, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/267/31057).
4. After successful configuration, you can push and play back with your own domain name.

<span id="que2"></span>
### Why CNAME is still displayed as not configured after configuration?

After you configure CNAME as instructed in [CNAME Configuration](https://intl.cloud.tencent.com/document/product/267/31057), please wait patiently because it takes 15-30 minutes for the configuration to take effect. In addition, you can check whether CNAME configuration is successful by following the steps in [Verifying the Effect of CNAME Record](https://intl.cloud.tencent.com/document/product/267/31057).
>?
> - DNS resolution must be performed over the public network on Linux/macOS/Windows.
> - If the CNAME configuration failure persists, consult your domain name registrar.

<span id="que3"></span>
### What if I don't add my own domain name?
If you activated the CSS service after October 17, 2018, you are required to add your own domain name for playback; otherwise, you cannot play back the live streaming content.

If you activated the service before then, CSS provided a default domain name for you, but we recommend that you replace it with your own domain name. Tencent Cloud has started phasing out the default domain names since December 31, 2018.

> ! Default domain names are system domain names assigned by CSS in the format of `bizid.liveplay.com`` and `bizid.tlivecdn.com`.

<span id="que4"></span>
### I have configured special items for the default domain name. Can my own domain name be resolved to the default one?
To use a new domain name, connect it to CSS from scratch. We recommend that you add and configure your own domain name in the CSS Console.



