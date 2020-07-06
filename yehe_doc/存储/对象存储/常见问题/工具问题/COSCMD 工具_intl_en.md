### Does COSCMD support regular expressions?

No.

### I can successfully create a bucket with a name containing uppercase letters using COSCMD, but when I perform other operations with a bucket name containing uppercase letters, an error occurs. What is the reason for this?

COSCMD automatically converts uppercase letters to lowercase ones. A bucket name can only contain lowercase letters, numbers, and hyphens (-), with a length not greater than 40 characters. For more information, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).

### Can the files in a sub-directory be excluded when I download the files in the root directory with COSCMD?

Yes. You can filter files using `coscmd download --ignore /folder/*`. If you need to ignore a folder with a certain suffix, be sure to append `,` to the "*" character, or enclose it with `""`.


### How can I transfer a large number of files with quicker speed?
You can do so by configuring an appropriate value for `MAX_THREAD`, which defaults to 5. The number of threads depends on the server performance, and generally, setting its value to 30 can easily take up full bandwidth. For example, you can set the number of concurrent threads to 30 by running the following command:
```plaintext
coscmd config -m 30
```
