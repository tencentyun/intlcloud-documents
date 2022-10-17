To help you quickly get started with the VOD console, this document will introduce some frequently used VOD services categorized according to user needs. The VOD console includes four modules: basic services, scenario-specific services, configuration services, and data services.

## Basic Services
The basic services include application creation, enabling, disabling, and termination as well as video uploading, processing, and distribution in application among other basic VOD features. If you only want to use basic VOD services, this is the right module for you.
<table>
<tr><th width="17%">Feature</th><th>Description</th></tr>
<tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/266/2841">Service Overview</a></td>
<td><ul style = "margin-bottom: 0px;"><li>View the billing mode, billable bandwidth, and other information about the current account such as billing mode and billable bandwidth.</li><li>View storage capacity, transcoding duration, traffic usage, bandwidth usage, and data retrieval, and weekly trend information.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/42093">Application Management</a></td>
<td><ul style= "margin: 0"><li>Create, enable, disable, and terminate applications.</li><li>Edit the application name, description, and tags and view the application storage, transcoding, and traffic data.</li></ul></td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/33890">Video Management</a></td>
<td><ul style= "margin: 0"><li>Upload, delete, view, edit, and filter videos, audio, and images. </li><li>Perform audio and video processing operations such as transcoding, adding watermarks, and video moderation.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/39706">Task Management</a></td>
<td>View the progress and details of VOD tasks.</td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/14059">Template Settings</a></td>
<td><ul style= "margin: 0"><li>Set templates for audio/video transcoding, Top Speed Codec, adaptive bitrate streaming, watermarking, screencapture, animated image generating, intelligent recognition and other audio/video processing templates. </li><li>Set task flow templates to process audio and videos.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/33896#editing-basic-info">Playback control</a></td>
<td><ul style= "margin: 0"><li>Get URLs for accelerated video playback. </li><li>Set authentication and access control for video URLs. </li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/7836">Player SDK</a></td>
<td><ul style= "margin: 0"><li>It supports multiple versions of players for multiple clients (iOS, web, Android).</li><li>It offers the player plugin in scenarios where a third-party player is used.</li><li>It provides automatic definition switch, instant first frame broadcasting, gesture control, and many other features. </li><li>It supports playing back videos of multiple codecs.</li></ul></td>
</tr>
</table>

## Scenario-Specific Services
Scenario-specific services are upgraded services for VOD use cases, including cold storage, video production, media moderation, application management, and license management. If you need to use such services, you can configure in this module.
<table>
<tr><th width="17%">Feature</th><th>Description</th></tr>
<tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/266/42092">Cold Storage</a></td>
<td><ul style = "margin-bottom: 0px;"><li>Change the storage classes of media resources and use cold storage and data retrieval capabilities to reduce the storage costs. </li><li>Set custom rule-based policies to automatically trigger cold storage for specified media resources.</li></ul></td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/33897">Audio/Video Moderation</a></td>
<td>Edit audio and videos, including setting volume, transparency, cropping, filters, text, transition effects, and subtitles among others.</td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/33897">Audio/Video Moderation</a></td>
<td><ul style= "margin: 0"><li>View the results of video moderation tasks to confirm whether there is inappropriate content in a video. </li><li>Start new recognition tasks based on the intelligent recognition results.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/42093">Application Management</a></td>
<td><ul style= "margin: 0"><li>You can create subapplications for resource isolation.</li><li>You can edit, disable, terminate, and enable subapplications.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/39429">License Management</a></td>
<td>Manage your UGSV SDK licenses.</td>
</tr>
</table>

## Configuration Services
Configuration services are custom configuration services of VOD, including domain name management, upload and storage settings, callback settings, and player configuration. If you need to use such services, you can configure in this module.
<table>
<tr><th width="17%">Feature</th><th>Description</th></tr>
<tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/266/35572">Domain Management</a></td>
<td><ul style = "margin-bottom: 0px;"><li>You can add domain names and configure CNAME.</li><li>You can perform certificate management, and set hotlink protection and global CDN acceleration for existing domain names.</li><li>You can set default distribution domain names.</li></ul></td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/18874">Upload Storage Settings</a></td>
<td><ul style= "margin: 0"><li>You can manage the categories of uploaded files. </li><li>You can enable media file storage regions and set the default storage regions for uploaded files.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/14055">Callback Settings</a></td>
<td>You can set the event notification method, specific events, and address to receive notifications. </td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/38261">Superplayer Configuration</a></td>
<td>You can configure adaptive bitrate streaming, image sprite, definition settings for the player.</td>
</tr>
</table>


## Data Services
Data services are professional data statistics and data analysis services, which allow you to query usage statistics such as traffic/bandwidth, storage, transcoding, and media moderation by time granularity, the access and playback of VOD files, as well as the log download feature for data monitoring and resource management.
<table>
<tr><th width="17%">Feature</th><th>Description</th></tr>
<tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/266/30421">Usage Statistics</a></td>
<td>You can view bandwidth/traffic, storage capacity, transcoding, and media moderation usage.</td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/30422">Data Analysis</a></td>
<td><ul style= "margin: 0"><li>You can view access data such as total number of access requests from unique IPs, total number of requests, etc.</li><li>You can view playback data such as file playback statistics, top 100 videos by playback times, etc.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/7983">Download Log</a></td>
<td>You can download hourly CDN logs to view the detailed information on access to domain names.</td>
</tr>
</table>
