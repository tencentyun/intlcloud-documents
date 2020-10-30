
MediaLive supports quick channel creation through exporting/importing channel configuration files or cloning a channel.
## Operation Method
### Step 1: Export a channel
All created channels and their states will be displayed in “Channel Management” of MediaLive. Click “Export” under the “Operation” column to quickly export the json file of the channel configuration.
 ![](https://main.qcloudimg.com/raw/a594a0763bbadf85dcc5df7fb44d6309.jpg)

### Step 2: Import a channel
Go to “Channel Management” and click “Create Channel”. Click “Import Configuration”, select the modified json file of the channel configuration, and import the file.
You will enter the channel editing state after submitting the json file. Then, complete the other channel configuration.
 ![](https://main.qcloudimg.com/raw/a9c515f9a211a36c621d32674b605d01.jpg)

>!
>- Channel importing is actually used for quickly entering contents. Based on the json file you imported, it will quickly help you fill in the “Basic Information” and “Output Group Setting,” but the “Input Setting” will not be filled in automatically. You need to select an input. Therefore, please create a new input in advance if you want to create a channel through channel importing.
>- If you import a new configuration file when editing the channel, the earlier channel configurations will be overwritten.

### Step 3: Clone a channel
Channel cloning is essentially a fast and special channel exporting/importing operation. Go to “Channel Management”. Click “Clone” under the “Operation” column to configure the channel cloning.
At this time, the channel’s “Basic Information” will be automatically filled in according to the cloned channel (except the “Input Setting”). Then, complete the other channel configurations.
![](https://main.qcloudimg.com/raw/2a8e3bc4beecc3be1f67de8aed62512f.jpg)
