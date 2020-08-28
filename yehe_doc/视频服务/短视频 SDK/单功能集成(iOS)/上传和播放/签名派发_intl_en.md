Video upload from client refers to uploading local videos to the VOD platform by an end user of the application. For more information, please see [Guide](https://intl.cloud.tencent.com/document/product/266/33921). This document describes how to generate a signature for upload from client.

## Overview
The overall process for upload from client is as follows:
![](https://main.qcloudimg.com/raw/dda5e1c01863e801e65d9635cedb4ca2.png)
To support upload from client, you need to build two backend services: signature distribution service and event notification receipt service.

* The client first requests an upload signature from the signature distribution service.
* The signature distribution service verifies whether the client user has the upload permission. If the verification passes, a signature will be generated and distributed; otherwise, an error code will be returned, and the upload process will end.
* After receiving the signature, the client will use the upload feature integrated in the UGSV SDK to upload the video.
* After the upload is completed, the VOD backend will send an [upload completion event notification](https://intl.cloud.tencent.com/document/product/266/33950) to your event notification receipt service.
* If the signature distribution service specifies a video processing [task flow](https://intl.cloud.tencent.com/document/product/266/33931) in the signature, the VOD service will automatically process the video accordingly after the video is uploaded. Video processing in UGSV scenarios is generally [AI-based porn detection](https://intl.cloud.tencent.com/document/product/1069/38040#.E4.BD.BF.E7.94.A8-ai-.E9.89.B4.E9.BB.84).
* After the video is processed, the VOD backend will send a [task flow status change event notification](https://intl.cloud.tencent.com/document/product/266/33953) to your event notification receipt service.

At this point, the entire video upload and processing flow ends.

## Signature Generation
For more information on the signature for upload from client, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).

## Signature Distribution Service Implementation Sample

``` 
/**
 * Calculate a signature
 */
function createFileUploadSignature({ timeStamp = 86400, procedure = '', classId = 0, oneTimeValid = 0, sourceContext = '' }) {
    // Determine the current time and expiration time of the signature
    let current = parseInt((new Date()).getTime() / 1000)
    let expired = current + timeStamp;  // Signature validity period: 1 day
    // Enter the parameters into the parameter list
    let arg_list = {
        //required
        secretId: this.conf.SecretId,
        currentTimeStamp: current,
        expireTime: expired,
        random: Math.round(Math.random() * Math.pow(2, 32)),
        //opts
        procedure,
        classId,
        oneTimeValid,
        sourceContext
    }
    // Calculate the signature
    let orignal = querystring.stringify(arg_list);
    let orignal_buffer = new Buffer(orignal, "utf8");
    let hmac = crypto.createHmac("sha1", this.conf.SecretKey);
    let hmac_buffer = hmac.update(orignal_buffer).digest();
    let signature = Buffer.concat([hmac_buffer, orignal_buffer]).toString("base64");
    return signature;
}
/**
 * Respond to a signature request
 */
function getUploadSignature(req, res) {
    res.json({
        code: 0,
        message: 'ok',
        data: {
            signature: gVodHelper.createFileUploadSignature({})
        }
    });
}
``` 
