## Overview
Many causes can lead to CVM login failure. Causes that can be monitored by Cloud Monitor include overly high CVM bandwidth usage and overly high CVM CPU/memory usage. This document describes how to troubleshoot these two causes.

## Problem Analysis
The following causes of CVM login failure can be detected by Cloud Monitor:
- [CVM bandwidth utilization is too high](#BandwidthUtilization)
- [CVM CPU/memory usage is too high](#HighServerLoad)


> Before troubleshooting, check whether the login attempt failed because the entered password was incorrect, you forgot the password, or the password failed to reset.
If yes, [reset the password](https://intl.cloud.tencent.com/document/product/213/16566).

<span id="BandwidthUtilization"></span>

## Solutions
### CVM bandwidth utilization is too high

**Problem**: the self-diagnosis tool shows that bandwidth utilization is too high.
**Solutions**:

1. Log in to the CVM instance via VNC.
 - [Log in to a Windows instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496).
 - [Log in to a Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Check the bandwidth utilization of the instance and troubleshoot accordingly. For more information, see [CVM Bandwidth Utilization Is Too High](https://intl.cloud.tencent.com/document/product/248/36207).

<span id="HighServerLoad"></span>

### CVM CPU/memory usage is too high

**Problem**: the self-diagnosis tool or Cloud Monitor shows that the CPU/memory usage of the CVM instance is too high, and therefore the system cannot establish a remote connection or the connectivity is poor.
**Possible causes**: viruses, trojans, third-party anti-virus software, application exceptions, driver exceptions, and automatic software backend updates may lead to high CPU usage, resulting in CVM login failure or slow access.
**Solutions**:

1. Log in to the CVM instance via VNC.
 - [Log in to a Windows instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496).
 - [Log in to a Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Refer to [CVM CPU/Memory Usage Is Too High](https://intl.cloud.tencent.com/document/product/248/36204) to identify the process with a high load on the **Task Manager** page.

> Many causes may lead to CVM login failure. For more information on other causes, see [Windows Instance Login Failures](https://intl.cloud.tencent.com/document/product/213/10339) or [Linux Instance Login Failures](https://intl.cloud.tencent.com/document/product/213/32500).

