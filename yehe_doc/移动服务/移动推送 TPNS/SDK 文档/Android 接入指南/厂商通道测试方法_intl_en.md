>?This testing method is applicable to phone vendor channels on all versions.

1. Integrate the TPNS SDK v1.0.9 or higher in your application and integrate the required vendor SDK according to the Integration Guide for Vendor Channels.
2. Confirm that the relevant application information has been entered in **[TPNS Console](https://console.cloud.tencent.com/tpns)** > **Configuration Management** > **Basic Configuration** > **Vendor Channel**. Usually, the relevant configuration will take effect after 1 hour. Please wait patiently and proceed to the next step after it takes effect.
3. Install the integrated application (testing version) on a test device and run the application.
4. Keep the application running in the foreground and try to make single/full push to the device.
5. If the application receives the message, switch the application to the background and stop all application processes.
6. Make single/full push again, and if the push is received, the vendor channel integration is successful.
