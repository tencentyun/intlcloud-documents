### Does the COSCMD tool support regular expressions?

No.

### I can successfully create a bucket with a name containing uppercase letters using COSCMD tool, but when I perform other operations with a bucket name containing uppercase letters, an error occurs. What is the reason for this?

The COSCMD tool automatically converts uppercase letters to lowercase ones. A bucket name can only contain lowercase letters, numbers, and hyphen (-), with a length not greater than 40 characters. For more information, see [Use Limits](https://cloud.tencent.com/document/product/436/14518).

### Can the files in a sub-directory be excluded when I download the files in the root directory with COSCMD tool?

Yes. You can filter our files using `coscmd download --ignore /folder/*`. If you need to ignore the folder with a certain suffix, be sure to append `,` to the "*" character, or enclose it with `""`.

