## Implementation Scenario
>
>1. Two COS buckets must be used. If you use the same bucket as both source and target buckets, each thumbnail uploaded to the source bucket may trigger another object creation event that will invoke the function again and thus cause an infinite loop.
>2. Make sure that the function and the COS bucket are in the same region.
>
In this tutorial, suppose that:
- A user is going to upload a photo to a specific COS bucket.
- You need to create a thumbnail for every image uploaded by the user.
- The created thumbnails need to be stored in another COS bucket.


## Implementation Overview

The implementation process of this function is as follows:
- You create the event source mapping between the function and the COS buckets.
- The user uploads an object to the source COS bucket (object creation event).
- The COS bucket detects the object creation event.
- COS invokes the function and passes the event data as parameters to the function, thus publishing the `cos:ObjectCreated:\*` event to the function.
- The SCF platform receives the invocation request and executes the function.
- The function gets the bucket name and filename from the received event data, gets the file from the source bucket, uses the graphic database to create a thumbnail, and saves the thumbnail in the target bucket.

Note: after going through this tutorial, your account will have the following resources:
- A SCF function used to create thumbnails.
- Two COS buckets: the source bucket for storing uploaded original images and the target bucket for storing cropped images.
