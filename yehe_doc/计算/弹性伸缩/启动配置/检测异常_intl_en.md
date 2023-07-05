Auto Scaling (AS) can detect exceptions in advance.

In some cases, such as when you have an insufficient balance or accidentally delete an image, it is impossible to create the CVMs needed for scale-out. AS can detect these exceptions in advance and send an alarm. This allows you to identify risks before scaling fails, so as to prevent losses. You can view the causes of exceptions as described below: 

In the launch configuration list, if **Invalid** appears in the **Validity** column, it indicates that your launch configuration has become unavailable due to an improper operation. Hover the cursor over the status to view the detailed reason.
