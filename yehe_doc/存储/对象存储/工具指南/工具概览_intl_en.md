<style>
table th:nth-of-type(1) {
width:200px;	
}
table th:nth-of-type(3) {
width: 200px;	
}
</style>


| Tool | Features |
|---------|---------|
| [COS Browser](https://www.tencentcloud.com/document/product/436/11366) | This tool makes it easy for users to perform data upload/download, access link generation, and other operations in a visualized manner. |
|   [COSCLI](https://intl.cloud.tencent.com/document/product/436/43249)    |   COS provides the command-line client COSCLI to allow you to upload, download, delete, and perform other operations on COS objects by using simple commands.     |
| [COSCMD](/doc/product/436/10976) | Enables users to perform operations (such as upload, download, and delete) in batches with simple commands. |
| [COS Migration](https://www.tencentcloud.com/document/product/436/15392) | This tool is used to migrate data from multiple data sources (such as on-premises server, and other cloud storage services) to COS. |
| [FTP Server](/doc/product/436/7214) | Enables users to upload/download files to/from COS by using an FTP client. |
| [COSFS](/doc/product/436/6883) | In Linux, this tool is used to mount buckets to a local file system and to perform operations on objects in COS via the local file system. |
|[Hadoop Tool](/doc/product/436/6884) | Helps integrate COS with big data computing frameworks such as Hadoop, Spark, and Tez, so that they can read and write COS data. |
| [COSDistCp](https://intl.cloud.tencent.com/document/product/436/38863)  |  COSDistCp is a MapReduce-based distributed file copy tool mainly used for data copy between HDFS and COS. |
| [Hadoop-cos-DistChecker](https://www.tencentcloud.com/document/product/436/34687) | Verifies the directory integrity after you use the `hadoop distcp` command to migrate data from HDFS to COS. |
| [HDFS TO COS](/doc/product/436/7212) | Copies data from HDFS to COS. |
| [Diagnostic Tool](https://www.tencentcloud.com/document/product/436/41623)  | COS's web-based diagnostic tool that allows you to troubleshoot error requests. |



## Upload Capabilities

The upload capabilities of different tools are detailed as below:

<table>
        <tr>
                <th width="22%">Tool</th>
                <th width="5%">Simple Upload</td>
								<th width="5%">Multipart Upload</th>
								<th width="20%">Checkpoint Restart</th>
								<th width="15%">Advanced Upload</th>
								<th width="15%">Consistency Check</th>
								<th width="12%">Pre-Signed URL Generation</th>
        </tr>
        <tr>
                <td>COSBrowser</td>
                <td>Supported</td>
								<td>Supported</td>
								<td>Supported</td>
								<td>Supported. By default, multipart upload will be triggered for files of 8 MB or above.</td>
								<td>Supported for MD5 check</td>
								<td>Supported for file download</td>
        </tr>
        <tr>
                <td>COSCLI</td>
                <td>Supported</td>
								<td>Supported</td>
								<td>Supported</td>
								<td>Supported. The trigger threshold for multipart upload can be customized.</td>
								<td>Supported for CRC64 check</td>
								<td>Supported</td>
        </tr>
        <tr>
                <td>COSCMD</td>
                <td>Supported</td>
								<td>Supported</td>
								<td>Supported</td>
								<td>Supported. By default, multipart upload will be triggered for files of 10 MB or above.</td>
								<td>Supported for MD5 check</td>
								<td>Supported</td>
        </tr>
        <tr>
                <td>COS Migration</td>
                <td>Supported</td>
								<td>Supported</td>
								<td>Supported</td>
								<td>Supported. The trigger threshold for multipart upload can be customized.</td>
								<td>Supported for MD5 check</td>
								<td>N/A</td>
        </tr>
        <tr>
                <td>FTP Server</td>
                <td>Supported</td>
								<td>Supported</td>
								<td>Supported</td>
								<td>Supported. The trigger threshold for multipart upload can be customized.</td>
								<td>Not supported</td>
								<td>N/A</td>
        </tr>
        <tr>
                <td>COSFS</td>
                <td>Supported</td>
								<td>Supported</td>
								<td>Supported</td>
								<td>Supported. The trigger threshold for multipart upload can be customized.</td>
								<td>Supported for MD5 check</td>
								<td>N/A</td>
        </tr>
        <tr>
                <td>Hadoop</td>
                <td>Supported</td>
								<td>Supported</td>
								<td>Not supported. There is an HDFS protocol conflict.</td>
								<td>Supported. The trigger threshold for multipart upload can be customized.</td>
								<td>Supported for CRC64 or CRC32 check</td>
								<td>N/A</td>
        </tr>
        <tr>
                <td>COSDistCp</td>
                <td>Supported</td>
								<td>Supported</td>
								<td>Not supported. There is an HDFS protocol conflict.</td>
								<td>Supported. The trigger threshold for multipart upload can be customized.</td>
								<td>Supported for file size, CRC64, or CRC32 check</td>
								<td>N/A</td>
        </tr>
        <tr>
                <td>HDFS TO COS</td>
                <td>Supported</td>
								<td>Supported</td>
								<td>Not supported. There is an HDFS protocol conflict.</td>
								<td>Supported. The trigger threshold for multipart upload can be customized.</td>
								<td>Supported for file name or size check</td>
								<td>N/A</td>
        </tr>
</table>

> ? Advanced upload encapsulates simple upload and multipart upload and can intelligently select the upload method based on file size.

