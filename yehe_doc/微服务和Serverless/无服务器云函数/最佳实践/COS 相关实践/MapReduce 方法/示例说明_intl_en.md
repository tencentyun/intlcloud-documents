In this tutorial, suppose that:
- You will upload some text files (such as logs) to a specific COS bucket from time to time.
- You need to count the words in these text files.

## Implementation Overview
The implementation process of this function is as follows:
- You create functions and COS buckets.
- You upload an object to the source COS bucket (object creation event).
- The COS bucket detects the object creation event.
- COS invokes the function and passes the event data as parameters to the function, thus publishing the `cos:ObjectCreated:\*` event to the function.
- The SCF platform receives the invocation request and executes the function.
- The function gets the bucket name and filename from the received event data, gets the file from the source bucket, uses the `wordcount` implemented in the code to count the words, and saves the word count in the target bucket.

>!
>- Three COS buckets are used in this example. If you use the same bucket as both source and target buckets, each file uploaded to the source bucket may trigger another object creation event that will invoke the function again and thus cause an infinite loop.
>- Make sure that the function and the COS buckets are in the same region.
>
Note: after going through this tutorial, your account will have the following resources:
- Two SCF functions: Mapper and Reducer.
- Three COS buckets: srcmr, middlestagebucket and destmr.
- The Mapper function will be bound to `srcmr` for triggering, the Reducer function will be bound to `middlestagebucket` for triggering, and `destmr` will be used to receive the final statistics.

