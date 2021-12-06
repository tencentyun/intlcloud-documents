### What should I do if the error “A query error has occurred” is reported during log query?

This issue is usually caused by the incorrect index configuration of the log topic associated with the function. Reconfigure the index as instructed in [Configuring index](https://intl.cloud.tencent.com/document/product/583/39778#configuring-index) and try again.

>! 
>- It generally takes 60 seconds for the log index configuration to take effect.
>- The index configuration update only affects new input data.

### What should I do if the error “server response timeout” is reported during log query?

This API timeout issue is usually caused by the oversized logs of the log topic associated with the function. Please shorten the log query time frame and try again.

