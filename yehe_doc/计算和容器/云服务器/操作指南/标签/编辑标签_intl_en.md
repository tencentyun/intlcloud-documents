## Operation Scenario
This document describes how to edit tags of resources.

## Use Limits

There are several limitations on editing tags:
- Quantity: each resource can have at most 50 tags.
- Tag key limitations:
  - You cannot create tag keys that start with `qcloud`, `tencent`, and `project` as they are reserved for the system.
  - Tag keys can only contain `numbers`, `alphabet characters`, `+=.@-`, and must be less than 255 characters.
- Tag value: tag values can only contain `empty strings or numbers`, `alphabet characters`, `+=.@-`, and must be less than 127 characters.


## Prerequisites
Log in to the [CVM Console](https://console.cloud.tencent.com/cvm).

## Directions
### Editing the tag of a single instance
1. On the Instance management page, select the instance of which the tags need to be edited and click **More** > **Instance Settings** > **Edit Tags**, as shown below.
![](https://main.qcloudimg.com/raw/29ad45e372fc78e28ab0ed69e73ec997.png)
2. Add, modify, or delete tags in the “1 cloud resource(s) selected” pop-up window based on your needs.

### Editing the tags of multiple instances
> You can batch edit tags of up to 20 resources at one time.
>
1. On the Instance management page, select the instances of which the tags need to be edited and click **More Actions** > **Instance Settings** > **Edit Tags** on the top, as shown below:
![](https://main.qcloudimg.com/raw/d0e1965a2e256cae7b4dbdb7881ca9de.png)
2. Add, modify, and delete tags in the “n cloud resource(s) selected” pop-up window based on your needs.

## Operation Examples

For information on how to use tags, please see [User Guide on Tags](https://intl.cloud.tencent.com/document/product/213/19548).
