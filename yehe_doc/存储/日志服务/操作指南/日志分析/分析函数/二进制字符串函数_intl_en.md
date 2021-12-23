This document introduces the basic syntax and examples of binary string functions.

>? Currently, CLS functions can be used in most regions. If they are required in Beijing, Shanghai, Guangzhou, and Nanjing, please contact [smart customer service](https://intl.cloud.tencent.com/contact-sales).
>

The binary string type varbinary is different from the string type varchar.

| Statement                                    | Description                                  |
| --------------------------------------- | ------------------------------------- |
| Concatenation function \|\|                           | The result of `a || b` is `ab`.                 |
| length(binary) → bigint                 | Returns a binary length.                    |
| concat(binary1, …, binaryN) → varbinary | Concatenates binary strings. This function provides the same functionality as \|\|.        |
| to_base64(binary) → varchar             | Converts a binary string into a base64 string.          |
| from_base64(string) → varbinary         | Converts a base64 string into a binary string.          |
| to_base64url(binary) → varchar          | Converts a binary string into a base64 string with a URL safe alphabet.               |
| from_base64url(string) → varbinary      | Converts a base64 string with a URL safe alphabet into a binary string. |
| to_hex(binary) → varchar                | Converts a binary string into a hexadecimal string.    |
| from_hex(string) → varbinary            | Converts a hexadecimal string into a binary string.              |
| to_big_endian_64(bigint) → varbinary    | Converts a bigint number into a big endian binary string.        |
| from_big_endian_64(binary) → bigint     | Converts a big endian binary string into a number.  |
| md5(binary) → varbinary                 | Computes the MD5 hash of a binary string.               |
| sha1(binary) → varbinary                | Computes the SHA1 hash of a binary string.              |
| sha256(binary) → varbinary              | Computes the SHA256 hash of a binary string.       |
| sha512(binary) → varbinary              | Computes the SHA512 hash of a binary string.            |
| xxhash64(binary) → varbinary            | Computes the xxHash64 hash of a binary string.          |

