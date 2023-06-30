## Issue Description
The multi-queue configuration of the CVM ENI is incorrect.

## Common Causes
By default, the CVM is configured with multiple queues for its ENI. This method distributes ENI terminals to different CPUs and improves the network processing performance. There may be manual modifications that result in the incorrect multi-queue ENI configuration.

## Solution
Correct the number of ENI queues as instructed in [Steps](#ProcessingSteps).


## Steps[](id:ProcessingSteps)
In the following steps, the default main ENI of the CVM is `eth0`, and the number of ENI queues is 2.
1. Run the following command to check the current number of ENI queues.
```
ethtool -l eth0
```
If the following result is returned, the currently set number of queues is less than the maximum number of ENI queues, which is unreasonable and needs to be fixed.
```
Channel parameters for eth0:
Pre-set maximums:
RX:             0
TX:             0
Other:          0
Combined:       2         ### Maximum number of ENI queues supported by the server
Current hardware settings:
RX:             0
TX:             0
Other:          0
Combined:       1        ### Currently set number of ENI queues
```
2. Run the following command to adjust the current number of ENI queues.
```
ethtool -L eth0  combined 2
```
The number of queues in the command is set to 2, which can be adjusted as needed, up to the maximum number of ENI queues supported by the server.
2. Run the following command to check the current configuration of the number of ENI queues.
```
ethtool -l eth
```
If the maximum number of ENI queues supported by the server is equal to the currently set number of ENI queues, the configuration is successful.
