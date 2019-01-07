## Overview
EXIF is short for "Exchangeable Image File", which records shooting parameters, thumbnails and other attributes of digital photos. Currently, this supports processing images with a size of less than 20 MB and a length x width of less than 9,999 pixels.
## API Form
download_url?exif
## Parameter Descriptions
| Parameter                                      | Meaning                                       |
| --------------------------------------- | ---------------------------------------- |
| download_url | Access link of the file which is structured as <bucket id>-<appid>.<picture region>.<domain>.com/<picture name>, for example, examples-1251000004.picsh.myqcloud.com/sample.jpeg |

## Example

```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?exif

```
