## Overview
This document describes how to upload files to the backend service through API Gateway. Based on different backend types and file sizes, there are the following four options, and you should choose the most appropriate one according to your actual business needs:

## Upload Process
![](https://main.qcloudimg.com/raw/b0edfab9807df98ded3d3ffa814b473b.png)

- If the backend is connected to an SCF API to upload a Base64-encoded file below 6 MB in size, we recommend you Base64-encode the file through the client and pass the encoded content to SCF first. Then, SCF will Base64-decode the content to complete the upload.

- If the backend is connected to an SCF API to upload a Base64-encoded file at or above 6 MB in size, we recommend you upload the file to COS through the client and pass the object address to SCF first. Then, SCF will pull the file from COS to complete the upload.

- If the backend is connected to an API of another service to upload a file below 16 MB in size, you only need to leave the parameters empty and keep everything pass-through.

- If the backend is connected to an API of another service to upload a file at or above 16 MB in size, we recommend you upload the file to COS through the client and pass the object address to the backend service first. Then, the backend service will pull the file from COS to complete the upload.
