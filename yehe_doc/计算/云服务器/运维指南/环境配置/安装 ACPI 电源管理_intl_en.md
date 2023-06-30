## Introduction

x86 machines use two power management methods, **APM** (Advanced Power Management) and **ACPI** (Advanced Configuration and Power Interface). ACPI is a power management standard jointly developed by Intel, Microsoft, and Toshiba, which provides a more flexible interface for computer and device management, whereas APM is the old power management standard.
Linux supports APM and ACPI, but the two standards cannot run simultaneously. Linux runs ACPI by default. Tencent Cloud also recommends ACPI. 
If ACPI is not installed in a Linux system, the soft shutdown will fail. This document describes how to check whether ACPI has been installed and if not, how to install it.

## Notes

For CoreOS, there is no need to install ACPI.

## Directions
 
1. Execute the following command to see if ACPI has been installed.
```
ps -ef|grep -w "acpid"|grep -v "grep"
```
 - If there is no process running, it means ACPI has not been installed. Please go to the next step.
 - If there is a process running, it means ACPI has been installed.
2. Execute the following command to install ACPI.
 - For Ubuntu or Debian:
```
sudo apt-get install acpid
```
 - For Redhat or CentOS:
```
yum install acpid
```
 - For SUSE:
```
in apcid
```
