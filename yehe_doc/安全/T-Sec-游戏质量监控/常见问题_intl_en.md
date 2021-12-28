### Remote Debugging

**1. If the debugging interface is closed inadvertently halfway, how to return to it？**
 If the page is inadvertently closed halfway, you can re-enter the remote debugging model list page, enter the “My Device List” module, check the occupied models, and click the “Continue Debugging” button to enter the debugging interface.No charge is calculated during the period of closing the page, but if you do not do anything in the debugging interface for a long time, the system will automatically end the debugging page.

**2. Why does it prompt that debugging is over when I didn’t click to end the test?**
 In order to avoid waste of resources, if you stay in the cloud mobile phone debugging interface for 30 minutes without any operation, the system will automatically and forcibly end the debugging.

**3. What should I do if there is a lag, black screen, or connection failure when I use a cloud mobile phone.**
 You can contact the online customer service, describe your problem clearly, and we will help you solve it as soon as possible.

**4. Is there an upper limit on the duration of a single use of device？**
 The maximum duration of single use of device is 5 hours, and it will be forced to end if it exceeds 5 hours.

**5. Failed to install app when using an iOS device.**
 At present, iOS devices support the installation of installation packages containing the enterprise signature of the inhouse profile file. Installation packages without the enterprise signature are not currently supported for installation.



### PerfDog

**1. PerfDog cannot detect the phone?**

- Android platform:

  a. Please turn on the Debug mode (for Huawei devices, you need to enable the ADB debugging option in the "Charge Only" mode of the developer options, and then turn on the USB debugging).

  b. The above does not work. Please re-open the PerfDog software and restart the phone.

  c. The above does not work, please confirm that ADB on the PC may be monopolized (automated testing framework, Android Studio tools, etc.), please close the tool and ADB.exe.

  d. The above does not work, please check with mobile phone butler or mobile assistant.

**Guide for Special Phones**: https://bbs.perfdog.qq.com/detail-133.html

- iOS platform:

  - Windows and before Mac 10.15

    a. Requires mobile phone trust.

    b. The above does not work, please use the latest version of itunes software to check whether the mobile phone can be detected.

    c. The above does not work, please restart the phone and change the USB cable (the USB cable may be aging).

    d. None of the above, please restart your phone.
    
  -  Mac10.15 and later systems

    a. The location device on the left of the finder determines the trust request.

    b. Terminal equipment confirmation.

  - Please download and use the latest itunes in advance (if you have installed iTools, please close iToos first).

2.  PerfDog's Windows & Mac OS X desktop app support users testing on iOS and Android devices.PerfDog can test multiple mobile devices at the same time on a single PC.

3.  PerfDog supports all applications on the mobile platform (games, apps, browsers, mini programs, mini-games, H5, background system processes, etc.) and Android Emulator, Cloud Real Machine performance tests.

4.  Support APP multi-process testing, such as Android multi-child process and iOS extension process APP Extension.

5. iOS platform: iPhone AssistiveTouch and Guided Access affect PerfDog to collect data accuracy, please close.

>?  Close the Guided Access method:
>- Click [Settings] - [General] - [Accessibility] - [Guided Access]
>- Turn on [Guided Access]. After entering the app, press the power button three times to completely hide the home button.
>- If you want to restore the home button, press the power button three times to restore.

6. Screen capture affects performance (overall FPS impact <=1). MI 5: CPU = about 1%. iPhone 7P: CPU < 2%. If not needed, please don't open the screenshot function.

7. Prompt network connection failure.

It may be that the network proxy is set on the PC network or the capture software is enabled. Please close it.

8. The memory collection of iOS mobile phone is always 0. Please restart the phone. The Energy collection is always 0. Please restart the tested APP application or game.

9. How to collect more performance parameters?

Customize the performance parameters by pressing the + button on the bottom right of the client. Check the box to indicate the collection, and select the corresponding box to indicate the display.

10. Why can't I see the GPU information?

The Android platform currently only supports some Qualcomm GPU phones, which will be completed later.

11. Why can't my phone test power?

The power can only be tested in WIFI mode, and the USB mode has a charging test meaningless. Under the iOS platform, there is a wireless charging function that is temporarily not supported.

12. Android phone WIFI mode connection failed?

For some Huawei and OPPO phones, please connect in WIFI mode in charging only mode.

13. Why can't I take a screenshot?

Only available in USB mode.

14. Why can't I see performance information on my phone?

Please open the phone floating window display permission.

15. Why does the WIFI test mode prompt connection failure?

   a. Make sure the computer and mobile phone are connected to the same WIFI.

   b. If not, it is possible that WIFI has set network security policy restrictions. Please change to another WIFI test.

16. Android cloud real machine test process：

Mobile cloud real machine platform ADB remote debugging-> Copy remote debug ADB command information-> Local cmd command window enter the ADB command just copied-> return to the mobile cloud real machine platform to confirm authorization-> PerfDog select cloud real machine test.

17. The Android emulator test process is similar to the Android cloud real machine test process.

18. For Mac systems, if you are prompted with a security question, you need to make security settings, otherwise PerfDog will be falsely reported as malicious software. The specific setting method is: Open System Settings-> Security and Privacy-> General-> Click Still Open.

19. Unable to delete PerfDog folder, please task manager close Adb.exe process.

20. Various tips, anyway can not be used

Please restart your phone or change the USB cable. Restarting is universal.

21. Incompatibility with automated test platform

Start the automation platform before starting PerfDog.

22. How to test multiple phones at the same time

- Windows: Double-click once to open it again. Can open multiple PerfDog

- Mac: Just like other programs, open one more PerfDog

Or use the command line: open -n /Applications/PerfDog.app.

23. Unable to start PerfDog on Windows platform

Don’t put the PerfDog file directory in the system disk or the Chinese directory.

