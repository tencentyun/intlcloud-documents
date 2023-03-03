## Overview

The basic image processing feature of CI enables you to add an [image](https://intl.cloud.tencent.com/document/product/1045/33720) or [text watermark](https://intl.cloud.tencent.com/document/product/1045/33721) to images. However, in actual business scenarios, an image may contain both a fixed logo watermark and a dynamically changing text watermark (username). For such scenarios, the following integration methods are provided. You can select an appropriate one based on your actual business scenario.

## Method Comparison

| Method | Pros | Cons |
|---------|---------|---------|
| 1 | It is easy to integrate and implement. | The watermark size cannot change dynamically with the image size or tiled. |
| 2 | It can better fit the image when the image size changes frequently. | It is difficult to integrate and is charged processing fees twice. |


## How to Use

### Method 1. Using a pipeline operator to add two types of watermarks with only one URL

The basic image processing feature of CI allows you to use [pipeline operators](https://intl.cloud.tencent.com/document/product/1045/33727) "|" to process an image multiple times with only one request at a one-time charge of processing and traffic fees. This method greatly reduces the latency and additional fees caused by repeated requests.

#### Directions

1. Define the image watermark parameters as instructed in [Image Watermarking](https://intl.cloud.tencent.com/document/product/1045/33720).
If you are unfamiliar with API parameters, you can add a style in the console to generate parameters as instructed in [Basic Processing](https://intl.cloud.tencent.com/document/product/1045/33443).

Below are the processing parameters:
```
watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTgxMjU2MzguY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vbG9nby5wbmc/dissolve/60/dx/10/dy/50/gravity/southeast
```
>? Here, `aHR0cDovL2V4YW1wbGVzLTEyNTgxMjU2MzguY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vbG9nby5wbmc` is the URL-safe Base64-encoded URL of the image watermark (image stored in the COS bucket).
>
2. Define the text watermark parameters as instructed in [Text Watermarking](https://intl.cloud.tencent.com/document/product/1045/33721).
If you are unfamiliar with API parameters, you can add a style in the console to generate parameters as instructed in [Basic Processing](https://intl.cloud.tencent.com/document/product/1045/33443).

```
watermark/2/text/VUlOOiAxMjM0NTY3OA/font/SGVsdmV0aWNhLmRmb250/fontsize/36/fill/IzAwMDAwMA/dissolve/50/gravity/southeast/dx/10/dy/10
```
>? Here, `VUlOOiAxMjM0NTY3OA` is the URL-safe Base64-encoded text of `UIN: 12345678`.
>
3. Use a pipeline operator to concatenate image and text watermark parameters:
```
watermark/2/text/VUlOOiAxMjM0NTY3OA/font/SGVsdmV0aWNhLmRmb250/fontsize/36/fill/IzAwMDAwMA/dissolve/50/gravity/southeast/dx/10/dy/10|watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTgxMjU2MzguY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vbG9nby5wbmc/gravity/southeast/dx/10/dy/50/dissolve/60 
```
4. Add the concatenated parameters to the end of the image download URL:
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/preview.png?watermark/2/text/VUlOOiAxMjM0NTY3OA/font/SGVsdmV0aWNhLmRmb250/fontsize/36/fill/IzAwMDAwMA/dissolve/50/gravity/southeast/dx/10/dy/10|watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTgxMjU2MzguY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vbG9nby5wbmc/gravity/southeast/dx/10/dy/50/dissolve/60 
```

To shorten the URL, you can add the part of the image watermark (unchanged) as the `watermark1` style in the console as instructed in [Basic Processing](https://intl.cloud.tencent.com/document/product/1045/33443).

In this way, the URL can be shortened to:
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/preview.png/watermark1?watermark/2/text/VUlOOiAxMjM0NTY3OA/font/SGVsdmV0aWNhLmRmb250/fontsize/36/fill/IzAwMDAwMA/dissolve/50/gravity/southeast/dx/10/dy/10
```
If you need to change the text content later, you only need to replace `VUlOOiAxMjM0NTY3OA` in the URL with the updated Base64 code; for example, `UIN: 88888888` is encoded into `VUlOOiA4ODg4ODg4OA`, so you only need to change the URL to the following content to replace the text:
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/preview.png/watermark1?watermark/2/text/VUlOOiA4ODg4ODg4OA/font/SGVsdmV0aWNhLmRmb250/fontsize/36/fill/IzAwMDAwMA/dissolve/50/gravity/southeast/dx/10/dy/10
```



### Method 2. Printing the text and image watermarks onto a transparent image and using the output image as the final image watermark

1. Upload a 400x400 px transparent PNG image to the bucket as instructed in [File Management](https://intl.cloud.tencent.com/document/product/1045/37766).
For example: `https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/transparent.png`
2. Generate and concatenate image and text watermark parameters as instructed in **steps 1–3 of method 1**.
3. Add the concatenated parameters at the end of the download URL of the transparent PNG image:
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/transparent.png?watermark/2/text/VUlOOiAxMjM0NTY/font/SGVsdmV0aWNhLmRmb250/fontsize/48/fill/IzAwMDAwMA/dissolve/60/gravity/south/dx/0/dy/60|watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTgxMjU2MzguY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vbG9nby5wbmc/gravity/center/dx/0/dy/0/dissolve/71
```

4. Use the transparent image as the image watermark and add the watermark to the original image:
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/preview.png?watermark/1/image/aHR0cDovL2V0ZXJuYXV4LTEzMDE0NTM1NTAuY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vdHJhbnNwYXJlbnQucG5nP3dhdGVybWFyay8yL3RleHQvVlVsT09pQXhNak0wTlRZL2ZvbnQvU0dWc2RtVjBhV05oTG1SbWIyNTAvZm9udHNpemUvNDgvZmlsbC9JekF3TURBd01BL2Rpc3NvbHZlLzYwL2dyYXZpdHkvc291dGgvZHgvMC9keS82MHx3YXRlcm1hcmsvMS9pbWFnZS9hSFIwY0RvdkwyVjBaWEp1WVhWNExURXpNREUwTlRNMU5UQXVZMjl6TG1Gd0xXZDFZVzVuZW1odmRTNXRlWEZqYkc5MVpDNWpiMjB2Ykc5bmJ5NXdibWMvZ3Jhdml0eS9jZW50ZXIvZHgvMC9keS8wL2Rpc3NvbHZlLzcx/gravity/southeast/dx/0/dy/0/dissolve/90
```

You can also use the `scatype` parameter to scale the image watermark proportionally to the image size and use the `batch` parameter to tile the image watermark.
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/preview.png?watermark/1/image/aHR0cDovL2V0ZXJuYXV4LTEzMDE0NTM1NTAuY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vdHJhbnNwYXJlbnQucG5nP3dhdGVybWFyay8yL3RleHQvVlVsT09pQXhNak0wTlRZL2ZvbnQvU0dWc2RtVjBhV05oTG1SbWIyNTAvZm9udHNpemUvNDgvZmlsbC9JekF3TURBd01BL2Rpc3NvbHZlLzYwL2dyYXZpdHkvc291dGgvZHgvMC9keS82MHx3YXRlcm1hcmsvMS9pbWFnZS9hSFIwY0RvdkwyVjBaWEp1WVhWNExURXpNREUwTlRNMU5UQXVZMjl6TG1Gd0xXZDFZVzVuZW1odmRTNXRlWEZqYkc5MVpDNWpiMjB2Ykc5bmJ5NXdibWMvZ3Jhdml0eS9jZW50ZXIvZHgvMC9keS8wL2Rpc3NvbHZlLzcx/scatype/3/spcent/30/gravity/southeast/dx/0/dy/0/dissolve/90/batch/1/degree/45
```


