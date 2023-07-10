This document introduces the basic syntax and examples of binary string functions.


The binary string type varbinary is different from the string type varchar.

| Statement                                    | Description                                  |
| --------------------------------------- | ------------------------------------- |
|Concatenation function \|\|   |The result of `a || b` is `ab`.              |
| length(binary) → bigint [](id:length)                | Returns a binary length.                    |
| concat(binary1, …, binaryN) → varbinary [](id:concat)| Concatenates binary strings. This function provides the same functionality as \|\|.        |
| to_base64(binary) → varchar  [](id:to_base64)           | Converts a binary string into a base64 string.          |
| from_base64(string) → varbinary [](id:from_base64)        | Converts a base64 string into a binary string.          |
| to_base64url(binary) → varchar   [](id:to_base64url)       | Converts a binary string into a base64 string with a URL safe alphabet.               |
| from_base64url(string) → varbinary   [](id:from_base64url)   | Converts a base64 string with a URL safe alphabet into a binary string. |
| to_hex(binary) → varchar [](id:to_hex)               | Converts a binary string into a hexadecimal string.    |
| from_hex(string) → varbinary[](id:from_hex)            | Converts a hexadecimal string into a binary string.              |
| to_big_endian_64(bigint) → varbinary[](id:to_big_endian_64)    | Converts a bigint number into a big endian binary string.        |
| from_big_endian_64(binary) → bigint [](id:from_big_endian_64)    | Converts a big endian binary string into a number.  |
| md5(binary) → varbinary  [](id:md5)               | Computes the MD5 hash of a binary string.               |
| sha1(binary) → varbinary[](id:sha1)                | Computes the SHA1 hash of a binary string.              |
| sha256(binary) → varbinary   [](id:sha256)           | Computes the SHA256 hash of a binary string.       |
| sha512(binary) → varbinary  [](id:sha512)            | Computes the SHA512 hash of a binary string.            |
| xxhash64(binary) → varbinary[](id:xxhash64)            | Computes the xxHash64 hash of a binary string.          |

