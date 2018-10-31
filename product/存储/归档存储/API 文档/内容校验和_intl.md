## Checksum Overview

Checksums are used to check the consistency of the request contents. There are two types of file checksums: `liner checksum` and `tree checksum`. For CAS, the checksum code of the file content is required for both simple upload and multipart upload. The server checks the consistency of the file using the checksum received. The request fails in case of inconsistency. When you download an archive, a checksum code is also returned by the CAS to check the data consistency.

### Linear checksum

A linear checksum, which is computed based on SHA256 algorithm, is passed as `x-cas-content-sha256` parameter in HTTP header. It is a combination of 64 characters comprised of numbers and lowercase letters.

Here is an example of a linear checksum.

```HTTP
x-cas-content-sha256:24329af4a7cb3276ddf3d6b09d42452ef3cf894a30a61f999909e3c00a5344a7
```

### Tree checksum

A tree checksum is passed as `x-cas-content-sha256` parameter in HTTP header. It is a combination of 64 characters comprised of numbers and lowercase letters.

The following describes how it is computed:

![](https://mc.qcloudimg.com/static/img/cad1e7d0680a508c3b1ac407f5318579/Vector+1.png)

1. Compute the SHA256 hash for each 1MB part of file content. The last part can be smaller than 1MB. For example, to upload a 3.2 MB file, you need to compute the SHA256 hash value for each of the first three 1MB parts, and then compute that for the last 0.2MB. These hash values are the leaf nodes.
2. Compute root nodes for two consecutive leaf nodes. Concatenate the hash values of two consecutive child nodes, and then compute the SHA256 hash of the concatenated hash values as the parent node hash value. When there is only one child node left, the hash value is passed to the next level of the tree.
3. Repeat step 2 until the resulting tree is rooted. The root of the tree is a hash value of the entire file, and the sub-trees are the hash values of the parts in multipart upload.

Here is an example of a tree checksum.

```HTTP
x-cas-sha256-tree-hash:74a1b786020a3c68fbe7bd3048a405bf5ec4b436977d917def4f78e5319d130f
```

## Checksums in Simple Upload

`x-cas-sha256-tree-hash` and `x-cas-content-sha256` of the entire archive is required when using Upload Archive API.

![](https://mc.qcloudimg.com/static/img/cad1e7d0680a508c3b1ac407f5318579/Vector+1.png)

## Checksums in Multipart Upload

The size of each part to be uploaded is a value obtained by multiplying 1MB by 2n.

-  `x-cas-sha256-tree-hash` and `x-cas-content-sha256` of each part is required when using Upload Part API.
-  `X-cas-sha256-tree-hash` of the entire archive is required for data consistency check when using Complete Multipart Upload API.

![](https://mc.qcloudimg.com/static/img/59958d9fc91a90231f235b4d74ed8073/Vector+2.png)

## Checksums in File Download

You can specify the download range with Initiate Job and Get Job Output requests. If the ranges specified in two requests are under the same sub-tree (as shown below), the server will return the tree checksum of the data chunk for data consistency check.

![](https://mc.qcloudimg.com/static/img/ebb31930c571ff7d42ac585bd8d8f0ea/Vector+3.png)

If the consecutive data chunks are not under the same sub-tree, the server will not return the tree checksum.

![](https://mc.qcloudimg.com/static/img/885ad51bfa62b92ec7e062f1c6b42092/Vector+4.png)

