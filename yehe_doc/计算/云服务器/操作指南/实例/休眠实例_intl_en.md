### Overview

When an instance is hibernated, the MEM data is retained in the system disk. When it is restarted, the applications are restored to the previous status automatically according to the retained MEM data.

Different to hibernation, when an instance is restarted after shutdown, backend services and applications are restarted from scratch. 

Hibernation is recommended if you do not want to run the instance or implement operations on it (such as adjusting configurations and reinstalling the system) for a short period.


### Requirements

1. Region: Silicon Valley.

2. Specification: Standard S3, MEM ＜ 150 GiB.

3. Image: Ubuntu20 or CentOS 8.x custom images.

4. System disk: Cloud disk.

5. Hibernation Agent: Installed.

### Considerations

1. Instance hibernation cannot be disabled when it is enabled at the time of instance creation.

2. The hibernation feature cannot be toggled off after creation.

3. **No charges during hibernation** and **Retain the instance and continue billing** are only available for pay-as-you-go instances. 

4. When the hibernation feature is toggled on, the following operations are NOT SUPPORTED: 

  - Adjusting configurations
    
  - Reinstalling the system
    
  - Creating snapshots
    
  - Adjusting disk media
    
  - Creating custom images
    

5. Hibernation is not available for instances added to an auto-scaling group.

>!
>1. If you enable hibernation on an instance, the instance is charged during hibernation.
>2. The instance status is changed to **Running** automatically after it is failed to enable hibernation.


### Directions

1. In the process of creating an instance, select Hibernation.

You need to enable hibernation at the time of instance creation. Otherwise, the instance cannot be hibernated.

2. Install the hibernation Agent.

  - Log in to the CVM instance.

  - Download the Agent script: `wget https://store-1252113659.cos.na-siliconvalley.myqcloud.com/suspend.py` 

  - Install the Agent   

    - For a CentOS instance: `python3 suspend.py`

    - For an Ubuntu instance: `sudo python3 suspend.py`


3. Hibernate the instance.

A running CVM instance can be hibernated if you enabled instance hibernation and installed the hibernation Agent for it.

  - Log in to the CVM console. Click **Instances** in the left sidebar. Select the desired instance. Click **More actions - Instance settings - Hibernate** on the right.

  - **No charges during hibernation** and **Retain the instance and continue billing** are available for a pay-as-you-go instance. Only **Charged during hibernation** is available for a spot instance.

  - Click **OK**. The instance goes into **Stopped** status. You can click **Start up** to restart it.