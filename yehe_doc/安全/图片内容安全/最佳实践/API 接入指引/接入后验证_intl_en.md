After completing the API connection, you can verify whether IMS is connected to successfully as detailed below.

## Connection Success

If the `Response` doesn't have the `Error` field and the business parameters are returned normally, IMS is connected to successfully as shown below:

```
{
  "Response": {
    "RequestId": "a61237dd-c2a0-43e7-a3da-d27022d39ba7",
    "DataId": "a61237dd-c2a0-43e7-a3da-d27022d39ba7",
    "BizType": "test_1001",
    "Suggestion": "Block",
    "FileMD5": "",
    "Label": "Porn",
    "SubLabel": "SexBehavior",
    "Score": 90,
    "LabelResults": [
      {
        "Scene": "Porn",
        "Suggestion": "Block",
        "Label": "Porn",
        "SubLabel": "SexBehavior",
        "Score": 90,
        "Details": []
      }
    ],
    "ObjectResults": [
      {
        "Scene": "QrCode",
        "Suggestion": "Block",
        "Label": "Ad",
        "SubLabel": "",
        "Score": 100,
        "Names": [
          "QRCODE"
        ],
        "Details": [
          {
            "Id": 0,
            "Name": "QRCODE",
            "Score": 100,
            "Location": {
              "X": 155.01746,
              "Y": 396.01746,
              "Width": 769.9824,
              "Height": 769.98254,
              "Rotate": 0
            }
          }
        ]
      }
    ],
    "OcrResults": [],
    "LibResults": [],
    "Extra": ""
  }
}
```



## Connection Failure

If the `Response` contains the `Error` field, the connection failed. The following is an example of failure caused by signature verification :

```
{
    "Response": {
        "Error": {
            "Code": "AuthFailure.SignatureFailure",
            "Message": "The provided credentials could not be validated. Please check your signature is correct."
        },
        "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
    }
}
```

`Code` in `Error` indicates the error code, while `Message` indicates the specific error information. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1122/43829).