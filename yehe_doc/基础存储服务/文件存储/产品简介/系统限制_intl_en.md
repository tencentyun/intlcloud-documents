## Limits and Notes
### Specification limits

<table> 
    <tr align="center">
        <td width="10.5%" rowspan="2" >Product Type</td>
        <td width="10%" colspan="2">Standard</td>
        <td width="10%" colspan="2">High-Performance</td>
        <td width="10%" colspan="2">Standard Turbo</td>
        <td width="10%" colspan="2">High-Performance Turbo</td>
    <tr align="center">
        <td width="10%" >Specification</td>
        <td width="10%" >Recommended Range</td>
        <td width="10%" >Specification</td>
        <td width="10%">Recommended Range</td>
       <td width="10%" >Specification</td>
        <td width="10%">Recommended Range</td>
       <td width="10%">Specification</td>
        <td width="10%">Recommended Range</td>
    </tr>
    <tr align="center">
        <td>Maximum system capacity</td>
        <td>160 TiB</td>
        <td>140 TiB<br></td>
        <td>32 TiB</td>
        <td>24 TiB<br></td>
        <td>100 PiB</td>
        <td>4 PiB<br></td>
        <td>100 PiB</td>
        <td>2 PiB<br></td>
    </tr>
    <tr align="center" >
        <td>Minimum system capacity</td>
        <td colspan="2">Unrestricted</td>
        <td colspan="2">Unrestricted</td>
        <td colspan="2">40 TiB</td>
        <td colspan="2">20 TiB</td>
   </tr>
    <tr align="center" >
        <td>Maximum system bandwidth</td>
        <td>300 MiB/s</td>
        <td>240 MiB/s</td>
        <td>1GiB/s</td>
        <td>800MiB/s</td>
        <td>100 GiB/s</td>
        <td>10 GiB/S</td>
        <td>100 GiB/s</td>
        <td>10 GiB/s</td>
    </tr>
    <tr align="center" >
        <td>Maximum number of system files</td>
        <td>Min[15000 * used capacity (GiB), 1 billion]</td>
        <td>Min[10000 * used capacity (GiB), 0.8 billion]</td>
        <td>Min[20000 * used capacity (GiB), 1.5 billion]</td>
        <td>Min[15000 * used capacity (GiB), 1 billion]</td>
        <td>Min[15000 * deployed capacity (GiB), 1 billion]</td>
        <td>Min[10000 * deployed capacity (GiB), 0.8 billion]</td>
        <td>Min[30000 * deployed capacity (GiB), 1.5 billion]</td>
        <td>Min[20000 * deployed capacity (GiB), 1 billion]</td>
    <tr align="center" >
        <td>Maximum number of system directories</td>
        <td>10 million</td>
        <td>8 million</td>
        <td>15 million</td>
        <td>10 million</td>
        <td>10 million</td>
        <td>8 million</td>
        <td>15 million</td>
        <td>10 million</td>
    <tr align="center" >
        <td>Maximum length of filename</td>
        <td>255 bytes</td>
        <td>255 bytes</td>
        <td>255 bytes</td>
        <td>255 bytes</td>
        <td>255 bytes</td>
        <td>255 bytes</td>
        <td>255 bytes</td>
        <td>255 bytes</td>
    <tr align="center" >
        <td>Maximum length of absolute path</td>
        <td>4,096 bytes</td>
        <td>4,096 bytes</td>
        <td>4,096 bytes</td>
        <td>4,096 bytes</td>
        <td>4,096 bytes</td>
        <td>4,096 bytes</td>
        <td>4,096 bytes</td>
        <td>4,096 bytes</td>
    <tr align="center" >
        <td>Maximum number of directory levels</td>
        <td>1000</td>
        <td>16</td>
        <td>1000</td>
        <td>16</td>
        <td>1000</td>
        <td>16</td>
        <td>1000</td>
        <td>16</td>
    <tr align="center" >
        <td>Maximum number of files/subdirectories per directory</td>
        <td>1 million</td>
        <td>0.8 million</td>
        <td>1 million</td>
        <td>0.8 million</td>
        <td>1 million</td>
        <td>0.8 million</td>
        <td>1 million</td>
        <td>0.8 million</td>
    <tr align="center" >
        <td>Maximum number of concurrently opened files</td>
        <td>65536</td>
        <td>1000</td>
        <td>65536</td>
        <td>1000</td>
        <td>65536</td>
        <td>1000</td>
        <td>65536</td>
        <td>1000</td>
    <tr align="center" >
        <td>Maximum number of locks per file</td>
        <td>512</td>
        <td>512</td>
        <td>512</td>
        <td>512</td>
        <td>512</td>
        <td>512</td>
        <td>512</td>
        <td>512</td>
    <tr align="center" >
        <td>Maximum number of clients</td>
        <td>1000</td>
        <td>100</td>
        <td>1000</td>
        <td>100</td>
        <td>2000</td>
        <td>1000</td>
        <td>2000</td>
        <td>1000</td>
    </tr>
    <tr align="center" >
        <td>Maximum number of mounted file systems per client</td>
        <td>1000</td>
        <td>16</td>
        <td>1000</td>
        <td>16</td>
        <td>16</td>
        <td>8</td>
        <td>16</td>
        <td>8</td>
    </tr>
    <tr align="center" >
        <td>Billing</td>
        <td colspan="2">Billed by the actual usage<br>(excluding prepaid)</td>
        <td colspan="2">Billed by the actual usage<br>(excluding prepaid)</td>
        <td colspan="2">Billed by the purchased capacity</td>
        <td colspan="2">Billed by the purchased capacity</td>
    </tr>
    <tr align="center" >
        <td>Supported protocol</td>
        <td colspan="2">NFS/SMB</td>
        <td colspan="2">NFS</td>
        <td colspan="4">POSIX/MPI</td>
    </tr>
    <tr align="center" >
        <td>Supported OS</td>
        <td colspan="4">Linux/Windows</td>
        <td colspan="4">Linux</td>
    </tr>
</table>


### Notes

#### Turbo series
- The Turbo series is mounted using a client. After you run the `mount` command on the client installed, you can use the file system the same way as a local file system.
- The Turbo series is billed according to the capacity purchased. For example, if you purchased a 40 TiB file system of the Standard Turbo storage class, you will be billed at the 40 TiB rates by hour, no matter how much you actually use. For example, if you use the file system for one hour, the fees will be calculated as follows: 40\*1024*0.09/24/30=5.12 USD. The file system can be terminated anytime.
- To ensure the cloud load balance of the file system after scaling up, we recommend that you scale up when around 80% of the capacity has been used. Online scale-up is supported and will be imperceptible during the whole process.
- The Turbo series cannot be scaled down. Alternatively, you can create a Turbo instance, migrate your data, and then delete the old instance.
- Because the self-deployed cluster needs to be set up again, the initial creation of the Turbo series will take about 20 minutes.
- The Turbo series can be mounted and used only by root accounts by default. If you need to use them with a general account, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category)  to contact us.
- If you need the Turbo series with higher specifications (supporting more files, directories, etc.), you can submit a ticket to contact us.


#### UID and GID

- When the NFS v3.0 protocol is used, if the UID or the GID of the file does not exist in the local account, then the UID and the GID will be displayed directly. Otherwise, the relevant user and group names will be displayed based on the mapping relationship of the local UID and GID.
- When the NFS v4.0 protocol is used, if the Linux version is above 3.0, the UID rules and the GID rules will be the same as those of the NFS v3.0 protocol. Otherwise, the UID and the GID of all files will be displayed as `nobody`.

>! When you mount a file system to a Linux version below 3.0 by using the NFS v4.0 protocol, we recommend that you refrain from performing "change owner" or "change group" on the file or directory. Otherwise, its UID and GID will become `nobody`.
>


#### Supported CIFS/SMB protocol
- Supported protocol versions: CIFS/SMB 1.0 and later are supported. However, we recommend that you refrain from mount file systems using SMB 1.0, because it is inferior in terms of performance and features to SMB 2.0 and later and because Windows has stopped its technical support service for Windows versions supporting SMB 1.0 or earlier.
- You cannot use NFS and SMB to access the same file system at the same time or directly access an SMB file system via WAN.
- Read/write ACL is provided only at the file system level. No ACL is provided at the file/directory level.
- IOCTL/FSCTL operations such as sparse files setting, file compression, ENI status query, and reparse point setting are not supported.
- Alternate Data Streams are not supported.
- Some protocol features in SMB 3.0 or above such as SMB Direct, SMB Multichannel, SMB Directory Leasing, and Persistent File Handle are not supported.
 <!--
 * Attributes not supported by NFS v4.0 include FATTR4_MIMETYPE, FATTR4_QUOTA_AVAIL_HARD, FATTR4_QUOTA_AVAIL_SOFT, FATTR4_QUOTA_USED, FATTR4_TIME_BACKUP, and FATTR4_TIME_CREATE. If these attributes are attempted, an `NFS4ERR_ATTRNOTSUPP` error will be displayed on the client.
 * OPs not supported by NFS v4.0 include OP_DELEGPURGE, OP_DELEGRETURN, and NFS4_OP_OPENATTR. If these OPs are attempted, an `NFS4ERR_NOTSUPP` error will be displayed on the client.
 * Currently, NFS v4 does not support the lock and delegation features.
 -->
