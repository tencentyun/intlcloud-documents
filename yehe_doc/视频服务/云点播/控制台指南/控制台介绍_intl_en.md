To help you quickly get started with the VOD console, this document will introduce some frequently used VOD services categorized according to user needs. The VOD console comes with four modules: basic services, scenario-specific services, configuration services, and data services.

## Basic Services
The basic services include video uploading, processing, and distribution among other VOD basic features. If you only want to use basic VOD services, this is the right module for you.
<table>
<tr><th width="17%">Feature</th><th>Description</th></tr>
<tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/266/2841">Service Overview</a></td>
<td><ul style = "margin-bottom: 0px;"><li>View the billing mode, billable bandwidth, and other information about the current account.</li><li>View storage capacity, transcoding duration, traffic usage, bandwidth usage, and moderation duration.</li></ul></td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/33890">Video Management</a></td>
<td><ul style= "margin: 0"><li>Upload, delete, view, edit, and filter videos, audio, and images. </li><li>Perform audio and video processing operations such as transcoding, watermarking, and video moderation.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/39706">Task Management</td>
<td>View the progress and details of VOD tasks.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/266/14059">Template Settings</a></td>
<td><ul style= "margin: 0"><li>Set templates for audio/video transcoding, Top Speed Codec, adaptive bitrate streaming, watermarking, screencapture, animated image generating, intelligent recognition and other audio/video processing templates. </li><li>Set task flow templates to process audio and videos.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/33896#editing-basic-info">Playback control</a></td>
<td><ul style= "margin: 0"><li>Get URLs for accelerated video playback. </li><li>Set authentication and access control for video URLs.
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/7836">Player SDK</a></td>
<td><ul style= "margin: 0"><li>Supports multiple versions of players for multiple clients (iOS, Web, Android). </li><li>Provides an adapter-version player for third-party players to access cloud PaaS resources.</li><li>Provides automatic definition switching, first frame broadcasting, gesture control, and many other features. </li><li>Supports playing back videos of multiple codecs.</li></ul></td>
</tr>
</table>

## Scenario-Specific Services
Scenario-specific services are upgraded services for VOD use cases, including cold storage, intelligent video recognition, application management, license management, etc. If you need to use such services, you can configure in this module.
<table>
<tr><th width="17%">Feature</th><th>Description</th></tr>
<tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/266/42092">Cold Storage</a></td>
<td><ul style = "margin-bottom: 0px;"><li>Change the storage classes of media resources and use cold storage and data retrieval capabilities to reduce storage costs. </li><li>Set custom rule-based policies to automatically trigger cold storage for specified media resources.</li></ul></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/266/33897">Intelligent Video Recognition</a></td>
<td><ul style= "margin: 0"><li>View the results of intelligent video recognition tasks to confirm whether there is inappropriate content in a video. </li><li>Start new recognition tasks based on the intelligent recognition results.</li></ul></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/266/42093">Application Management</td>
<td><ul style= "margin: 0"><li>Create subapplications for resource isolation.</li><li>Edit, disable, terminate, and enable subapplications.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/39429">License Management</a></td>
<td>Manage the UGSV SDK license.</td>
</tr>
</table>



## Configuration Services
Configuration services are custom configuration services of VOD, including domain name management, upload storage settings, callback settings, superplayer configuration, etc. If you need to use such services, you can configure in this module.
<table>
<tr><th width="17%">Feature</th><th>Description</th></tr>
<tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/266/35572">Domain Management</a></td>
<td><ul style = "margin-bottom: 0px;"><li>Add domain names and configure CNAME.</li><li>Perform certificate management, and set hotlink protection and global CDN acceleration for existing domain names.</li><li>Set default distribution domain names.</li></ul></td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/18874">Upload Storage Settings</a></td>
<td><ul style= "margin: 0"><li>Manage the categories of uploaded files. </li><li>Enable media file storage regions and set the default storage regions for uploaded files.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/14055">Callback Settings</a></td>
<td>Set the event notification method, specific events, and address to receive notifications. </td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/38261">Superplayer Configuration</a></td>
<td>Configure adaptive bitrate streaming, image sprite, definition settings for the superplayer.</td>
</tr>
</table>


## Data Services
Data services are professional data statistics and data analysis services, which allow you to query usage statistics such as traffic/bandwidth, storage, transcoding, and intelligent video recognition by time granularity, the access and playback of VOD files, as well as the log download feature for data monitoring and resource management.
<table>
<tr><th width="17%">Feature</th><th>Description</th></tr>
<tr>
<td ><a href="https://intl.cloud.tencent.com/document/product/266/30421">Usage Statistics</a></td>
<td>View bandwidth/traffic, storage capacity, transcoding, and intelligent video recognition usage.</td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/30422">Data Analysis</a></td>
<td><ul style= "margin: 0"><li>View access data such as total number of access requests from unique IPs, total number of requests, etc.</li><li>View playback data such as file playback statistics, top 100 videos by playback times, etc.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/7983">Download Log</a></td>
<td>Download hourly CDN logs to view the detailed information on access to domain names.</td>
</tr>
</table>



