<div class="tab_list">
<ul>
    <li><a href="#A-J">A-J</a></li>
    <li><a href="#K-T">K-T</a></li>
    <li><a href="#U-Z">U-Z</a></li>
</ul>
</div>


<span id="A-J"></span>
## A-J 
### Standard output 
You can configure the mapping address (COS) of the standard output. The information output to stdout and stderr from the application will be uploaded to the corresponding address after the task is completed, so that the computing process can be backtracked after the task is completed. 
### Compute environment	 
A compute environment is a CVM instance or a cluster of CVM instances. You can submit jobs directly which will automatically create and terminate CVM instances during execution. You can also create a compute environment and then submit jobs to it.
 

<span id="K-T"></span>
## K-T 

### Task 
A task is the information about the application executed on a CVM instance. Batch's scheduling system automatically creates CVM instances and executes applications based on the configuration submitted by the user.
### Task instance 
Task instance is the smallest unit of scheduling and execution in Batch. Each task can specify one or more task instances for execution. You can set the number of instances that need to be executed concurrently in the task configuration.
### Instance 
Instance is the smallest unit of scheduling and execution in Batch and corresponds to a CVM instance. Each task can specify one or more instances for execution.




<span id="U-Z"></span>
## U-Z
### Remote storage mapping 
The remote storage map maps the remote storage address (object storage COS or file storage CFS) to the CVM's local file system so that it can read and write remote storage in the same way as the local file system.
### Job 
A job is the unit in which a user submits a batch processing work and consists of a single or multiple tasks with dependencies. Dependencies among multiple batch tasks can be set through the very easy-to-use DAG syntax.
### Execution environment 
It contains image and command configuration. The image is usually a custom image containing your applications and the environment they depends on, and the command specifies how to launch these applications for computation.

