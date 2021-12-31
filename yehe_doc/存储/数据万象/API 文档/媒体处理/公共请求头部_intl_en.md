## Overview


This document describes common request headers that may be used in API requests. The headers mentioned below will not be addressed again in related API documents.

## Request Headers


<table>
<thead>
<tr>
<th>Header</th>
<th>Description</th>
<th>Type</th>
<th>Required</th>
</tr>
</thead>
<tbody><tr>
<td>Authorization</td>
<td>Carries the authentication information, i.e., signing information, used to verify the validity of a request </td>
<td>string</td>
<td>Yes</td>
</tr>
<tr>
<td nowrap="nowrap">Content-Length</td>
<td>Length in bytes of the content of an HTTP request defined in RFC 2616</td>
<td>integer</td>
<td>No<br>Required for PUT and POST requests</td>
</tr>
<tr>
<td>Content-Type</td>
<td>Content type (MIME) of an HTTP request as defined in RFC 2616, such as <code>application/xml</code></td>
<td>string</td>
<td>No<br>Required for PUT and POST requests with a request body</td>
</tr>
<tr>
<td>Content-MD5</td>
<td>Base64-encoded MD5 hash value of the request body content as defined in RFC 1864, such as <code>ZzD3iDJdrMAAb00lgLLeig==</code>. The value is used to verify whether the request body experienced any changes during transfer.</td>
<td>string</td>
<td>No</td>
</tr>
<tr>
<td>Date</td>
<td>Current time in GMT as defined in RFC 1123, such as <code>Wed, 29 May 2019 04:10:12 GMT</code></td>
<td>string</td>
<td>No</td>
</tr>
<tr>
<td>Host</td>
<td>Requested host in the format of <code>&lt;BucketName-APPID&gt;.ci.&lt;Region&gt;.myqcloud.com</code></td>
<td>string</td>
<td>Yes</td>
</tr>
<tr>
<td nowrap="nowrap">x-ci-security-token</td>
<td>Security token field required when using temporary security credentials</td>
<td>string</td>
<td>No<br>Required when a temporary key is used and the authentication information is carried through <code>Authorization</code></td>
</tr>
</tbody></table>




