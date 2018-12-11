## Creating a Job

For more information about job, see "Job" in the [Glossary](https://cloud.tencent.com/document/product/599/10396). You can create a job in the [Batch Console]().

1. Log in to the [Batch Console]().   If you have not activated Batch yet, follow on-screen prompts on the Batch Console homepage to activate it.

2. Click "Job" in the left navigation bar, select the target region and click **Create**.
  ![](https://main.qcloudimg.com/raw/7eb9eae8b394d921be0998a67af84218.png)

3. Configure basic job information.
  ![](https://main.qcloudimg.com/raw/4a2d70b65da863db2590f78a43de8dce.png)

4. Select the task template on the left in "Task flow", move the task onto the canvas on the right using the mouse and create a link by dragging and dropping the anchor.
    ![](https://main.qcloudimg.com/raw/1436b756d73f6fffa68eff65741922ee.png)

5. Turn on "Task details" to the right of "Task flow", confirm the everything is correct and click **Finish**.
   + In the job task flow, each task is created based on the customized task template.
   + Turn on "Task information" on the right, select a task and you can edit the configuration of the task. The editing operations have no effect on the task template.
   ![](https://main.qcloudimg.com/raw/8d08a7c2584b666c58277e464f563de3.png)

## Terminating a Job
You can terminate the operation of a job under certain conditions. For more information about termination, see the API documentation for [Terminating a Job](https://intl.cloud.tencent.com/document/product/599/12688).

## Deleting a Job
If the job is in the completed state (either SUCCEED or FAILED), it can be deleted from the job list.
![](https://main.qcloudimg.com/raw/3e5d88069ef36fa1a04688659cd0618d.png)



