### What is a CAR concurrency pack? How do I determine the max number of concurrent users?
To use CAR services for your application, you need to purchase a concurrency pack. When you configure a pack, you can select the max number of concurrencies (i.e. the max number of concurrent users). Each concurrency supports access by only one user at a time. You can select the number and region of concurrencies based on the average and peak numbers of concurrent users you expect to access your application as well as the users’ region.

### When a user directly exits the client or webpage, how long does it take to release a concurrency?
If the user directly closes the page to close the connection to CAR, because [DestroySession](https://intl.cloud.tencent.com/document/product/1158/49967) is not called, CAR will wait 90 seconds for the user to reconnect, after which the concurrency will be released.

### How do I know that a user closes the CAR connection?
We recommend you directly maintain a heartbeat between the business backend and the client to detect whether the user is connected.

### How do I immediately release a CAR concurrency?
The backend actively calls the [DestroySession](https://intl.cloud.tencent.com/document/product/1158/49967) API.

### What should I do if a message indicating that there are no idle concurrencies is prompted when CAR calls the API for applying for a concurrency?
You can troubleshoot as follows:
- Concurrencies cannot be scheduled if there are no concurrency packs in the console. Check whether you have purchased a CAR concurrency pack.
- Check whether the requested project is bound to a concurrency pack in the console. If not, bind it to a concurrency pack with the same concurrency scale.
- Check whether there are any idle concurrencies (i.e., concurrencies that are not currently being occupied by a user) under the requested project in the console. After the last user exits the application, it will take some time for the concurrency to be cleared and released. A user can access the application only after a concurrency becomes idle.

### Can I call `ApplyConcurrent` and `CreateSession` repeatedly? Will a new concurrency or the original one be connected to in a repeated call?
`ApplyConcurrent` and `CreateSession` can be called repeatedly. If the original concurrency hasn’t been repossessed, it will be connected to, and the original client connection will close. If the original concurrency has already been repossessed, a new concurrency will be connected to.
![](https://qcloudimg.tencent-cloud.cn/raw/291399f70ba46fb36457dfb7835cf469.jpg)

### Will the connection close if the user performs no operations for a long time?
CAR doesn't actively close the user connection, so you need to actively close the connection based on the SDK callback. To set the duration after which the concurrency will become considered idle (i.e., the duration a user is idle and performs no operations), you can customize the `idleThreshold` parameter in the [init](https://intl.cloud.tencent.com/document/product/1158/49627#tcgsdk.init(params)) API. After you receive the callback, you can call [DestroySession](https://intl.cloud.tencent.com/document/product/1158/49967) to release the concurrency.
