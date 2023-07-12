This document describes CLS LogListener updates.

>?
> - The \_\_HOSTNAME\_\_ collection feature is available starting from LogListener v2.7.4.
> - The combined parsing feature is available starting from LogListener v2.6.4.
> - Full/Incremental collection policies are available starting from LogListener v2.6.2.
> - CVM batch deployment is available starting from LogListener v2.6.0.
> - Multi-line - full regular expression collection mode is available starting from LogListener v2.4.5.
> - LogListener auto upgrade is available starting from LogListener v2.5.0.
> - Uploading parsing-failed logs is available starting from LogListener v2.5.2.
> - You are advised to [install or upgrade to the latest version](https://intl.cloud.tencent.com/document/product/614/17414) for a better user experience.
> 

<table>
	<tr><th style="width: 10%;">Version</th><th style="width: 11%;">Change Type</th><th>Description</th></tr>
	<tr><td><b>v2.7.9</b></td><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Added LogListener file lock verification, so only one agent instance can be started by default.</li><li>Fixed the empty row processing exception in `containerd stdout`.</li><li>Fixed full disk and business exceptions caused by file handle leaks.</li><li>Fixed the failure in parsing the second half of the log content when there were too many lines of logs.</li></ul></td></tr>
	<tr><td><b>v2.7.8</b></td><td>Experience optimization</td><td>Fixed the issue where logs didn't have tag metadata due to metadata file generation delay in container scenarios.</td></tr>
	<tr><td><b>v2.7.7</b></td><td>Experience optimization</td><td>Fixed the issue where the collection program's network connection couldn't be reconnected after a DNS exception was fixed.</td></tr>
	<tr><td><b>v2.7.6</b></td><td>Experience optimization</td><td>Optimized the line break processing during `hostname` extraction.</td></tr>
	<tr><td><b>v2.7.5</b></td><td>Experience optimization</td><td>Fixed the processing exception in file rotation when the actual file and soft link in the same directory were collected at the same time with different collection configurations.</td></tr>
	<tr><td rowspan=2><b>v2.7.4</b></td><td>New feature</td><td><ul  style="margin: 0;"><li>Supported collecting `hostname` as the metadata.</li><li>Added `meta_processor` for combined parsing and supported parsing custom metadata (path).</li></ul></td></tr>
	<tr><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Fixed the missing collection problem in file deletion scenarios.</li><li>Fixed the issue where a file was collected repeatedly as the file size calculated by the system was incorrect due to the lace of a line break at the end of the file.</li></ul></td></tr>
	<tr><td><b>v2.7.3</b></td><td>New feature	</td><td>Supported log upload from multiple endpoints by a single agent instance.</td></tr>
	<tr><td><b>v2.7.2</b></td><td>Experience optimization</td><td>Fixed the issue where the memory leaked as the corresponding configuration cache couldn't be cleared when a rotation file was removed.</td></tr>
	<tr><td><b>v2.7.1</b></td><td>Experience optimization</td><td>Fixed the issue where a large number of empty service logs were printed.</td></tr>
	<tr><td><b>v2.7.0</b></td><td>Experience optimization</td><td>Fixed the issue where collection was blocked due to possible exceptions when an empty string was uploaded.</td></tr>
	<tr><td><b>v2.6.9</b></td><td>Experience optimization</td><td>Fixed the issue where excessive invalid logs were printed when multi-line log parsing failed.</td></tr>
	<tr><td><b>v2.6.8</b></td><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Added a limit on the LogListener collection specification, so the protection mechanism will be enabled after the limit is exceeded.</li><li>Fixed the Ubuntu startup failure.</li><li>Optimized the blocklist feature to reduce the memory usage.</li><li>Optimized the combined parsing mode and fixed processing exceptions when the root processor was a regular expression parsing plugin.</li><li>Optimized the printing of certain logs.</li></ul></td></tr>
	<tr><td><b>v2.6.7</b></td><td>New feature</td><td>Supported the multi-tenancy collection capabilities under a single agent.</td></tr>
	<tr><td><b>v2.6.6</b></td><td>Experience optimization</td><td>Fixed the issue where files with a small amount of written data might be missing or delayed during collection in soft link scenarios.</td></tr>
	<tr><td rowspan=2><b>v2.6.5</b></td><td>New feature</td><td>Supported parsing the time zone information in the log time.</td></tr>
	<tr><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Fixed the empty pointer processing exception in advanced data processing.</li><li>Fixed the exception when multiple files were rotated at the same time.</li></ul></td></tr>
	<tr><td rowspan=2><b>v2.6.4</b></td><td>New feature</td><td>Supported customizing log parsing rules through a plugin.</td></tr>
	<tr><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Optimized the log parsing format pipeline.</li><li>Fixed the exception of parsing the millisecond timestamp (`%F`).</li></ul></td></tr>
	<tr><td><b>v2.6.3</b></td><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Fixed the issue where LogListener couldn't be started if the checkpoint file is corrupted.</li><li>Fixed the issue where the blocklist didn't take effect for new files in special scenarios.</li></ul></td></tr>
	<tr><td rowspan=2><b>v2.6.2</b></td><td>New feature</td><td>Added support for incremental collection.</td></tr>
	<tr><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Optimized the issue where collection is ignored in the period from file scanning to processing.</li><li>Optimized abnormal overriding during automatic upgrade.</li></ul></td></tr>
	<tr><td><b>v2.6.1</b></td><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Optimized the issue where backtracking collection may occur during log rotation in some scenarios.</li><li>Adjusted the timeout duration for log upload on the collection end to avoid data duplication caused by timeout.</li></ul></td></tr>
	<tr><td rowspan=2><b>v2.6.0</b></td><td>New feature</td><td><ul  style="margin: 0;"><li>Added support for CVM batch deployment.</li><li>Added support for ciphertext storage of secret IDs/KEYs.</li></ul></td></tr>
	<tr><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Optimized the LogListener installation and stop logic.</li><li>Optimized the retry policy upon upload failures.</li><li>Added a tool for detecting and rectifying dead locks caused by Glibc libraries of earlier versions.</li><li>Optimized collection performance.</li></ul></td></tr>
	<tr><td><b>v2.5.9</b></td><td>Experience optimization</td><td>Optimized the resource limit policy.</td></tr>
	<tr><td><b>v2.5.8</b></td><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Fixed the issue that removing a directory soft link affects the collection of other directory soft links that point to the same target.</li><li>Fixed the issue that files in a directory cannot be collected if a soft link of the directory is removed and the same soft link is created again.</li></ul></td></tr>
	<tr><td><b>v2.5.7</b></td><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Fixed the (new) issue that logs will be collected again when the log file size is greater than 2 GB.</li><li>Fixed the issue where renaming too many files will cause the program to malfunction.</li><li>Fixed the issue where specified fields cannot be updated under log collection monitoring.</li></ul></td></tr>
	<tr><td><b>v2.5.6</b></td><td>Experience optimization</td><td>Optimized the issue that under specific use cases, the collection program cannot be triggered.</td></tr>
	<tr><td><b>v2.5.5</b></td><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Optimized metadata checkpoints for collection to guarantee no data will lose due to restart.</li><li>Supports resource limit configuration and overrun handling for memory, CPU, and bandwidth. </li></ul></td></tr>
	<tr><td rowspan=2><b>v2.5.4</b></td><td>New feature</td><td>Added support for log collection monitoring.</td></tr>
	<tr><td>Experience optimization</td><td>Enhanced memory overrun handling: LogListener will be automatically loaded when memory overrun lasts for a period of time. </td></tr>
	<tr><td><b>v2.5.3</b></td><td>Experience optimization</td><td>Optimized LogListener exceptions caused by memory issues.</td></tr>
	<tr><td rowspan=2><b>v2.5.2</b></td><td>New feature</td><td>Added support for uploading parsing-failed logs.</td></tr>
	<tr><td>Experience optimization</td><td>Optimized the blocklist feature. Now, the blocklist FILE mode supports wildcard filtering.</td></tr>
	<tr><td><b>v2.5.1</b></td><td>Experience optimization</td><td>Enhanced the handling when breakpoint metadata could not be found in the collection file.</td></tr>
	<tr><td><b>v2.5.0</b></td><td>New feature</td><td><ul  style="margin: 0;"><li>Added support for automatic LogListener upgrade. </li><li>Added support for automatic LogListener start in Ubuntu operating system.</li></ul></td></tr>
	<tr><td><b>v2.4.6</b></td><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Cleared residual configuration data in the cache after the collection configuration was changed. </li><li>Optimized the issue where file collection with a soft link pointing to the `realpath` file was affected when an `IN_DELETE` event that deleted the soft link was being processed. </li><li>Optimized the feature of collecting the same source file via the file's soft link and the directory's soft link at the same time.</li></ul></td></tr>
	<tr><td><b>v2.4.5</b></td><td>New feature</td><td>Added support for `multiline_fullregex_log` log collection.</td></tr>
	<tr><td><b>v2.4.4</b></td><td>Experience optimization</td><td>Optimized the issue of inaccurate log time caused by the msec feature.</td></tr>
	<tr><td><b>v2.4.3</b></td><td>New feature</td><td>Added support for automatically checking the log format (logFormat).</td></tr>
	<tr><td><b>v2.4.2</b></td><td>Experience optimization</td><td>Optimized the issue of cache eviction during configuration pulling in Tencent Cloud container scenarios.</td></tr>
	<tr><td rowspan=2><b>v2.4.1</b></td><td>New feature</td><td>Added support for collecting logs in milliseconds.</td></tr>
	<tr><td>Experience optimization</td><td>Optimized exceptions due to no line break data in user logs.</td></tr>
	<tr><td><b>v2.4.0</td><td>New feature</td><td>Added support for instance-level process monitoring by LogListener.</td></tr>
	<tr><td rowspan=2><b>v2.3.9</b></td><td>New feature</td><td>Added support for blocklisting collection paths.</td></tr>
	<tr><td>Experience optimization</td><td>Optimized the memory leak issue due to outdated Boost library.</td></tr>
	<tr><td><b>v2.3.8</b></td><td>New feature</td><td>Added support for multi-path log collection.</td></tr>
	<tr><td><b>v2.3.6</b></td><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Fixed the issue where collection stopped due to invalid key value. </li><li>Fixed the memory leak issue due to request failures with the error code 502 returned.</li></ul></td></tr>
	<tr><td rowspan=2><b>v2.3.5</b></td><td>New feature</td><td>Added support for log context search.</td></tr>
	<tr><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Fixed the issue where log collection stopped when logs were uploaded but authentication failed in the static configuration mode. </li><li>Fixed the issue where dynamic configurations were no longer read after the memory exceeded the threshold in the dynamic configuration mode. </li><li>Fixed the issue where sometimes log collection repeated when the log production speed was too high during log rotation. </li><li>Fixed the memory leak issue caused by multiple failures to upload logs.</li></ul></td></tr>
	<tr><td><b>v2.3.1</b></td><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Optimized memory limit. </li><li>When the memory limit was reached, requests lasting over 3s were considered as timed out.</li></ul></td></tr>
	<tr><td rowspan=2><b>v2.2.6</b></td><td>New feature</td><td>Added support for configuring private domain names and public domain names separately.</td></tr>
	<tr><td>Experience optimization</td><td>Fixed LogListener exceptions caused by `getip`.</td></tr>
	<tr><td rowspan=2><b>v2.2.5</b></td><td>New feature</td><td>Added support for Tencent Cloud COC environment deployment.</td></tr>
	<tr><td>Experience optimization</td><td>Fixed the core issue caused by `getip`.</td></tr>
	<tr><td><b>v2.2.4</b></td><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Changed the commands for installation and initialization to the subcommands `install` and `init` of `tools/loglistener.sh` respectively. </li><li>Changed the command for restart to `/etc/init.d/loglistenerd start|stop|restart`.</li></ul></td></tr>
	<tr><td><b>v2.2.3</b></td><td>Experience optimization</td><td>Renaming or creating logs during log rotation will not cause log loss.</td></tr>
	<tr><td><b>v2.2.2</b></td><td>Experience optimization</td><td>A log greater than 512 KB will be automatically truncated.</td></tr>
	<tr><td><b>Earlier versions</b></td><td>-</td><td><ul  style="margin: 0;"><li>v2.2.2 added support for collection by full regular expression. </li><li>v2.1.4 added support for full text in multi lines. </li><li>v2.1.1 added support for log structuring.</li></ul></td></tr>
</table>


