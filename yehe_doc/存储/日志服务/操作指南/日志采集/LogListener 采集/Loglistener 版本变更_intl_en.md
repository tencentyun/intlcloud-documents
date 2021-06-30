This document describes CLS LogListener versions.

>?
> - Multi-line - full regular expression collection mode is available starting from LogListener v2.4.5.
> - LogListener auto upgrade is available starting from LogListener v2.5.0.
> - Uploading parsing-failed logs is available starting from LogListener v2.5.2.
> - You are advised to [install or upgrade to the latest version](https://intl.cloud.tencent.com/document/product/614/17414) for a better user experience.
> 

<table>
	<tr><th style="width: 10%;">Version</th><th style="width: 11%;">Change Type</th><th>Description</th></tr>
	<tr><td><b>v2.5.9</b></td><td>Bug fix</td><td>Fixed the issue in the resource limit policy.</td></tr>
	<tr><td><b>v2.5.8</b></td><td>Bug fix</td><td><ul  style="margin: 0;"><li>Fixed the issue that removing a directory soft link affects the collection of other directory soft links that point to the same target.</li><li>Fixed the issue that files in a directory cannot be collected if a soft link of the directory is removed and the same soft link is created again.</li></ul></td></tr>
	<tr><td><b>v2.5.7</b></td><td>Bug fix</td><td><ul  style="margin: 0;"><li>Fixed the (new) issue that logs will be collected again when the log file size is larger than 2 GB.</li><li>Fixed the issue where renaming too many files will cause the program to malfunction.</li><li>Fixed the issue where specified fields cannot be updated under log collection monitoring.</li></ul></td></tr>
	<tr><td><b>v2.5.6</b></td><td>Bug fix</td><td>Fixed the issue that under specific use cases, the collected program cannot be triggered.</td></tr>
	<tr><td><b>v2.5.5</b></td><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Optimized metadata checkpoints for collection to guarantee no data will lose due to restart.</li><li>Supports resource limit configuration and overrun handling for memory, CPU, and bandwidth. </li></ul></td></tr>
	<tr><td rowspan=3><b>v2.5.4</b></td><td>New feature</td><td>Added support for log collection monitoring.</td></tr>
	<tr><td>Experience optimization</td><td>Enhanced memory overrun handling: LogListener will be automatically loaded when memory overrun lasts for a period of time. </td></tr>
	<tr><td>Bug fix</td><td><ul  style="margin: 0;"><li>Fixed the issue where the collection configuration cannot be pulled and the collection operation is blocked when the regular expression processing malfunctions.</li><li>Fixed the issue where some logs cannot be collected when the "inotify" event queue overflows.</li><li>Fixed the issue where some files will be recollected when multiple files are renamed at the same time.</li><li>Fixed the issue where logs are shipped to an incorrect log topic during log rotation.</li></ul></td></tr>
	<tr><td><b>v2.5.3</b></td><td>Bug fix</td><td>Fixed LogListener exceptions caused by memory issues.</td></tr>
	<tr><td rowspan=2><b>v2.5.2</b></td><td>New feature</td><td>Added support for uploading parsing-failed logs.</td></tr>
	<tr><td>Bug fix</td><td>Fixed a blocklist bug. Now the blocklist FILE mode supports wildcard filtering.</td></tr>
	<tr><td><b>v2.5.1</b></td><td>Experience optimization</td><td>Enhanced the handling when breakpoint metadata could not be found in the collection file.</td></tr>
	<tr><td><b>v2.5.0</b></td><td>New feature</td><td><ul  style="margin: 0;"><li>Added support for automatic LogListener upgrade. </li><li>Added support for automatic LogListener start in Ubuntu operating system.</li></ul></td></tr>
	<tr><td><b>v2.4.6</b></td><td>Bug fix</td><td><ul  style="margin: 0;"><li>Fixed the issue where there was residual data in the cache after the collection configuration was changed. </li><li>Fixed the issue where file collection with a soft link pointing to the `realpath` file was affected when an `IN_DELETE` event that deletes the soft link was being processed. </li><li>Fixed LogListener crashes when collecting the same source file via the file’s soft link and the directory’s soft link at the same time.</li></ul></td></tr>
	<tr><td><b>v2.4.5</b></td><td>New feature</td><td>Added support for `multiline_fullregex_log` log collection.</td></tr>
	<tr><td><b>v2.4.4</b></td><td>Bug fix</td><td>Fixed the issue of inaccurate log time caused by the msec feature.</td></tr>
	<tr><td><b>v2.4.3</b></td><td>New feature</td><td>Added support for automatically checking the log format (logFormat).</td></tr>
	<tr><td><b>v2.4.2</b></td><td>Bug fix</td><td>Fixed the issue of cache eviction of related configurations when pulling configurations under Tencent Cloud container scenarios.</td></tr>
	<tr><td rowspan=2><b>v2.4.1</b></td><td>New feature</td><td>Added support for collecting logs in milliseconds.</td></tr>
	<tr><td>Bug fix</td><td>Fixed exceptions due to no line break data in user logs.</td></tr>
	<tr><td><b>v2.4.0</td><td>New feature</td><td>Added support for instance-level process monitoring.</td></tr>
	<tr><td rowspan=2><b>v2.3.9</b></td><td>New feature</td><td>Added support for blocklisting collection paths.</td></tr>
	<tr><td>Bug fix</td><td>Fixed the memory leak issue due to outdated Boost library.</td></tr>
	<tr><td><b>v2.3.8</b></td><td>New feature</td><td>Added support for multi-path log collection.</td></tr>
	<tr><td><b>v2.3.6</b></td><td>Bug fix</td><td><ul  style="margin: 0;"><li>Fixed the issue where collection stopped due to invalid key value. </li><li>Fixed the memory leak issue due to request failures with the error code 502 returned.</li></ul></td></tr>
	<tr><td rowspan=2><b>v2.3.5</b></td><td>New feature</td><td>Added support for log context search.</td></tr>
	<tr><td>Bug fix</td><td><ul  style="margin: 0;"><li>Fixed the issue where log collection stopped when logs were uploaded but authentication failed in the static configuration mode. </li><li>Fixed the issue where dynamic configurations were no longer read after the memory exceeded the threshold in the dynamic configuration mode. </li><li>Fixed the issue where sometimes log collection repeated when the log production speed was too high during log rotation. </li><li>Fixed the memory leak issue caused by multiple failures to upload logs.</li></ul></td></tr>
	<tr><td><b>v2.3.1</b></td><td>Bug fix</td><td><ul  style="margin: 0;"><li>Optimized memory limit. </li><li>When the memory limit was reached, requests lasting over 3s were considered as timed out.</li></ul></td></tr>
	<tr><td rowspan=2><b>v2.2.6</b></td><td>New feature</td><td>Added support for configuring private domain names and public domain names separately.</td></tr>
	<tr><td>Bug fix</td><td>Fixed LogListener exceptions caused by `getip`.</td></tr>
	<tr><td rowspan=2><b>v2.2.5</b></td><td>New feature</td><td>Added support for Tencent Cloud COC environment deployment.</td></tr>
	<tr><td>Bug fix</td><td>Fixed the issue of core loss or corruption caused by `getip`.</td></tr>
	<tr><td><b>v2.2.4</b></td><td>Experience optimization</td><td><ul  style="margin: 0;"><li>Changed the commands for installation and initialization to the subcommands `install` and `init` of `tools/loglistener.sh` respectively. </li><li>Changed the command for restart to `/etc/init.d/loglistenerd start|stop|restart`.</li></ul></td></tr>
	<tr><td><b>v2.2.3</b></td><td>Experience optimization</td><td>Renaming or creating logs during log rotation will not cause log loss.</td></tr>
	<tr><td><b>v2.2.2</b></td><td>Experience optimization</td><td>A log greater than 512 KB will be automatically truncated.</td></tr>
	<tr><td><b>Earlier versions</b></td><td>-</td><td><ul  style="margin: 0;"><li>v2.2.2 added support for collection by full regular expression. </li><li>v2.1.4 added support for full text in multi lines. </li><li>v2.1.1 added support for log structuring.</li></ul></td></tr>
</table>


