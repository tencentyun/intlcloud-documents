### Does COSCMD support regular expressions?

No.

### I successfully created a bucket with a name containing uppercase letters using COSCMD tool, but when I performed other operations with a bucket name containing uppercase letters, an error occurred. What is the cause of it?

COSCMD automatically converts uppercase letters to lowercase ones. A bucket name can be up to 50 characters, containing only lowercase letters, numbers, hyphens (-), and a combination of them. For more information, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).

### Can the files in a sub-directory be excluded when I download the files in the root directory with COSCMD tool?

Yes. You can filter our files using `coscmd download --ignore /folder/*`. If you need to ignore the folder with a certain suffix, be sure to append `,` to the "*" character, or enclose it with `""`.


### How can I transfer a massive number of files faster?
You may do so by configuring an appropriate value for MAX_THREAD, which defaults to 5. The number of threads depends on the server performance, and generally, setting its value to 30 can easily take up full bandwidth. For example, you may set the number of concurrent threads to 30 by running
```plaintext
coscmd config -m 30
```


### Does COSCMD support using \* to determine objects with specified prefix to download?

No, it doesn’t. Instead, you have to download by running
```plaintext
coscmd download prefix/ localpath/ -r
```
