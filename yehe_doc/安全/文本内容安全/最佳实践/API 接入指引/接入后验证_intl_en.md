After completing the API connection, you can verify whether TMS is connected to successfully as detailed below.

## Connection Success

If the `Response` doesn't have the `Error` field and the business parameters are returned normally, TMS is connected to successfully as shown below:

```
{
  "Response": {
    "DataId": "123",
    "Extra": "xx",
    "BizType": "0",
    "RiskDetails": [
      {
        "Level": 2,
        "Label": "RiskAccount"
      }
    ],
    "DetailResults": [
      {
        "LibName": "Porn",
        "Score": 72,
        "Label": "Porn",
        "LibId": "12",
        "Suggestion": "Review",
        "Keywords": [
          "Porn"
        ],
        "LibType": 0
      },
      {
        "LibName": "Porn",
        "Score": 0,
        "Label": "",
        "LibId": "1",
        "Suggestion": "Block",
        "Keywords": [
          "Porn"
        ],
        "LibType": 2
      }
    ],
    "Label": "Ad",
    "Score": 87,
    "RequestId": "x2123-123123-123",
    "Suggestion": "Block",
    "Keywords": [
      "Friend me for coupons"
    ]
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

`Code` in `Error` indicates the error code, while `Message` indicates the specific error information. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1121/43771). If you cannot identify the cause of the connection error, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance on a 24/7 basis.