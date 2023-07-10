## Job APIs

Job is an abstract concept. Smart voice has many types of jobs, such as text to speech and audio noise cancellation.
A job contains three key pieces of information: input, output, and parameters. Input and output control the input file when the job is executed and the target file after the job is executed, and parameters control the detailed configurations for executing specific features.


<table>
<thead>
<tr>
<th colspan=2>Features</th>
<th>Job API</th>
</tr>
</thead>
<tbody><tr>
<tr>
<td rowspan=4>Smart voice</td>
<td>Audio noise cancellation</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/48933">Submitting Audio Noise Cancellation Job</a></td>
</tr>
<tr>
<td>Voice/Sound separation</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/48946">Submitting Voice/Sound Separation Job</a></td>
</tr>
<tr>
<td>Text to speech</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/48942">Submitting Text-to-Speech Job</a></td>
</tr>
<tr>
<td>Speech recognition</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1045/49789">Submitting Speech Recognition Job</a></td>
</tr>


## Workflow APIs

A workflow in smart voice refers to the process of automatically processing the specified uploaded file by configuring multiple job operations. For more information on calls, see [Workflow APIs](https://www.tencentcloud.com/document/product/1045/43618).

## Batch Operation APIs

A batch operation is to execute a single job or automatically perform operations configured in a workflow on the specified existing file. For more information on calls, see [Triggering Batch Data Processing Job](https://www.tencentcloud.com/document/product/1045/48921).
