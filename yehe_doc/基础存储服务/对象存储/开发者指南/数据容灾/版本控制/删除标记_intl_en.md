## Overview

A delete marker is used to mark a versioned object as “deleted” in COS. It has an object key and version ID just like an object, but with the following differences:

- Its content is empty.
- It is not associated with an ACL value.
- A GET request on a delete marker will return a 404 error.
- The only operation you can use on a delete marker is DELETE, and only the root account can make such a request.

## Deleting a Delete Marker

To permanently delete a delete marker, specify its version ID in a DELETE Object versionId request. If you use a DELETE request to delete a delete marker without specifying its version ID, COS will not delete the delete marker, but instead, insert another delete marker.

The following figure shows how a simple DELETE on a delete marker removes nothing, but adds a new delete marker to the bucket.
![](https://main.qcloudimg.com/raw/cfce300a0a08889ef385e9140f771ccc.jpg)

In a versioning-enabled bucket, a new delete marker has a unique version ID. Therefore, one object may have multiple delete markers in the same bucket. To delete a delete marker permanently, you must include its version ID in a DELETE Object versionId request.

The following figure shows how you can permanently delete a delete marker with a DELETE Object versionId request.
![](https://main.qcloudimg.com/raw/89e0cb4d6fdbcd089d3f7e0bde6d90ec.jpg)

>You can delete a delete marker only after the root account grants the `DeleteObject` permission.

To permanently delete a delete marker:

1. Set versionId to the ID of the version of the delete marker you want to delete.
2. Send a DELETE Object versionId request.
