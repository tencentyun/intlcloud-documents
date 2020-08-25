## CVM Shutdown Analysis

### Shutdown process
>?See [Shutdown Instances](https://intl.cloud.tencent.com/document/product/213/4929) for related operations.
>
The shutdown process of a Tencent Cloud Windows instance is as follows:
1. The host sends the shutdown command via libvirt on the QMP protocol to `qemu` component.
2. The `qemu` component transfers the shutdown command to CVM  by interrupting ACPI (for more information, see technical documents on VMCS).
3. After receiving the shutdown signal, Windows instance exits applications and service processes.
4. Close the core service process.
5. Turn off the power.
>! The sequence of closing applications and services in step 3-4 may vary with the system settings.

Windows is a closed-source system. It provides APIs that allow kernel-mode and user-mode programs to intervene in the shutdown process. And some running Windows services will also affect the shutdown process, increase the shutdown time, and cause shutdown failure.

### Forced shutdown
In a virtualization scenario, in addition to the soft shutdown initialized by system signal and through the message notification, you can force the CVM to shut down, like pulling the plug. This way is called **forced shutdown**.
The forced shutdown may affect Windows and user experience in the following two aspects:
1. A forced shutdown interrupts some services and applications, and causes improper operations, such as unsaved documents, and unfinished WindowsUpdate processes.
2. During the shutdown process, the NTFS system (or the earlier FAT32 system) of Windows writes key data to the disk. A forced shutdown may result in write failure, and then the NTFS file system damage alleged by Windows.

Therefore, we recommend that you **firstly use soft shutdown** on a Windows instance.

## Scenarios of Shutdown Failure
The Windows system may have issues that affect the shutdown process and cause shutdown failure, including but not limited to:
1. A WindowsUpdate process may prolong the shutdown time. The Windows system may perform patch operations during the shutdown process, and give a prompt message like "Please do not power off or unplug your computer".
2. If the Windows system has "Shutdown Event Tracker" mechanism enabled, and needs shutdown due to any system service or driver error, the system will give a prompt box or require an error description based on the configuration. The system will wait for you to complete these operations before shutdown.
3. Windows supports no shutdown without login. Under this configuration, the soft shutdown command sent from the virtual host will be discarded by Windows. So Windows will not shut down.
4. Before the shutdown, Windows will broadcast a message to every service and application. If the applications fail to give affirmative responses, Windows will not initiate the shutdown. In this case, you can configure Windows to ignore this response process.
5. If you configure the power management **When I press the power button** on Windows to ignore it or do nothing, Windows will ignore the shutdown event received from the virtual host.
6. Based on the settings of power management, Windows will go into Sleep and ignore the shutdown event.
7. If the Windows system itself is damaged due to some malicious software installed within it or infection with Trojans or other viruses, Windows may prevent shutdown.

Tencent Cloud has solved most of shutdown failures when releasing Windows public image to ensure soft shutdown. However, if your Windows is infected with viruses or Trojans, the system is damaged, or the Windows settings are adjusted again, the soft shutdown may fail.
**Forced shutdown involves risks. Use it when you really have to.**


