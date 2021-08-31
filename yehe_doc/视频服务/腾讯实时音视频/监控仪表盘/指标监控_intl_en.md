Log in to the [TRTC Console](https://console.cloud.tencent.com/rav) and click the name of the target application to enter its details page. On the left sidebar, select **Monitoring Dashboard** to view **Call Quality**.
Click **View Details** in the call quality section to view monitoring curves of specific metrics of the current call, which are as detailed below:

## User
This part uses an animation to show the moving direction of audio/video data: the user on the left uploads audio/video data to the cloud, and a CVM instance forwards the data to the user on the right.


## Audio/Video Bitrate
- **Bitrate of Sender**
It is the amount of audio/video data sent per second in Kbps. If the bitrate is 800 Kbps, the data amount generated in one minute will be: 800 KB * 60s / 8 = 6 MB.
- **Bitrate of Receiver**
It is the amount of audio/video data received per second in Kbps. Generally, a lower value indicates a lower definition.



## Video Frame Rate

- **Frame Rate of Sender**
It indicates how many frames are encoded per second. The recommended value is 15 FPS, which can ensure that the video image is smooth enough without reducing the video definition due to too many frames per second.
- **Frame Rate of Receiver**
It indicates how many video frames are received per second. The higher the value, the smoother the image; the lower the value, the more the image lags. Generally, a frame rate below 5 FPS can cause obvious lags.



## LOSS (Network Packet Loss Rate)
The lower the LOSS value, the better; for example, 0% packet loss rate indicates that the network is optimal, and 30% packet loss rate indicates that 3 out of every 10 data packets between the SDK and CVM instance are discarded.



## RTT (Network Delay)
It is the round-trip time between the SDK and server. The smaller the value, the better. Generally, RTT lower than 50 ms is satisfactory, while RTT higher than 100 ms will result in long call delay.



## CPU Utilization
"App CPU" is your application CPU utilization, while "System CPU" is the current total CPU utilization of the system.


## Memory Utilization

It refers to the application memory utilization. As modern real-time operating systems (such as iOS, Android, and Windows) all have a complicated multi-policy virtual memory control mechanism, the actual memory utilization will fluctuate.


