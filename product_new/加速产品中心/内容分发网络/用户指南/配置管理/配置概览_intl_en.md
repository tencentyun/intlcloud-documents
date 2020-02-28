CDN supports various custom configurations, you can optimize your CDN acceleration based on your business needs.

## Basic Configuration
| Configuration Name | Feature Description |
| ------------------------------------------------------------ | -------------------------------------- |
| [Basic Information](https://intl.cloud.tencent.com/doc/product/228/7864) | Modifies the domain¡¯s project and service type |
| [Origin Server Configuration](https://intl.cloud.tencent.com/doc/product/228/6289) | Configures hot backup origin server and modifies the origin server to ensure the success of origin-pull |
| [Host Header Configuration](https://intl.cloud.tencent.com/doc/product/228/6293) | Specifies the domain name accessed by CDN during origin-pull |

## Access Control
| Configuration Name | Feature Description |
| ---------------------------------------- | ------------------------- |
| [Ignore Query String Configuration](https://intl.cloud.tencent.com/doc/product/228/6291) | Specifies whether a node will ignore the parameters after "?" in a user request URL |
| [Hotlink Protection Configuration](https://intl.cloud.tencent.com/doc/product/228/6292) | Configures HTTP referer blacklist/whitelist |
| [IP Blacklist/Whitelist Configuration](https://intl.cloud.tencent.com/doc/product/228/6298) | Configures IP blacklist/whitelist for access control |
| [IP Access Limit Configuration](https://intl.cloud.tencent.com/doc/product/228/6420) | Configures access limit of an IP to a single node |
| [Video Dragging Configuration](https://intl.cloud.tencent.com/doc/product/228/8111) | Enables video dragging configuration |


## Cache Expiration Configuration
| Configuration Name | Feature Description |
| ---------------------------------------- | ----------------- |
| [Cache Expiration Configuration](https://intl.cloud.tencent.com/doc/product/228/6290) | Configures cache expiration rules for the specified resources |
| [Status Code Cache Configuration](https://intl.cloud.tencent.com/doc/product/228/6290) | Configures 404 status code cache period |
| [HTTP Header Cache Configuration](https://intl.cloud.tencent.com/doc/product/228/6290) | Configures the header cache policy |

## Origin Configuration
| Configuration Name | Feature Description |
| ---------------------------------------- | -------------------- |
| [Intermediate Node Configuration](https://intl.cloud.tencent.com/doc/product/228/6294) | Specifies whether to use intermediate nodes |
| [Range GETs Configuration](https://intl.cloud.tencent.com/doc/product/228/7184) | Enables/disables range GETs |
| [Follow 302 Configuration](https://intl.cloud.tencent.com/doc/product/228/7183) | Configures whether requests should be redirected when the origin server returns the 302 status code |

## Security Configuration

| Configuration Name | Feature Description |
| ------------------------------------------------------------ | ------------- |
| Authentication Configuration | Configures URL authentication |

## Advanced Configuration

| Configuration Name | Feature Description |
| ---------------------------------------- | -------------------------------- |
| [Bandwidth Cap Configuration](https://intl.cloud.tencent.com/doc/product/228/7541) | Configures bandwidth cap for domain names. When the cap is reached, the CDN service will be disabled and the access request will be forwarded to the origin server |
| [HTTPS Configuration](https://intl.cloud.tencent.com/doc/product/228/6295) | Configures HTTPS to implement secure acceleration where forced HTTPS redirection is supported |
| [SEO Optimization Configuration](https://intl.cloud.tencent.com/doc/product/228/6297) | Enables SEO optimization configuration to ensure stability of the search engine weights |
| [HTTP Header Configuration](https://intl.cloud.tencent.com/doc/product/228/6296) | Adds an HTTP header configuration |

## Cross-border Direct Connect Configuration
| Configuration Name | Feature Description |
| ---------------------- | ------------------------------------------------ |
| Cross-border Direct Connect Configuration (in beta) | Enables/disables cross-border direct connect lines during global CDN acceleration to ensure origin-pull quality |

