## Symptoms

When POST requests are initiated via COS APIs, the following error messages are returned:
- [Condition key q-ak doesn&apos;t match the value XXXXXX](#AccessDenied_q-ak)
- [You post object request has been expired, expiration time: 1621188104 but the time now : 1621245817](#AccessDenied_Expiration)
- [The Signature you specified is invalid.](#SignatureDoesNotMatch_POSTSignature)
- [You must provide condition if you specify a policy in post object request.](#InvalidPolicyDocument_JSONFormat)
- [Condition key bucket doesn&apos;t match the value [bucket-appid]](#AccessDenied_BucketNotConsistent)
- [Condition key key doesn&apos;t match the value XXXXX](#AccessDenied_Condition)
- [The body of your POST request is not well-formed multipart/form-data.](#MalformedPOSTRequest_POSTBody)



## Troubleshooting

<span id="AccessDenied_q-ak"></span>
### Error message "Condition key q-ak doesn&apos;t match the value XXXXXX"

When POST requests are initiated via COS APIs, the following information is displayed:

```
<Code>AccessDenied</Code>
<Message>Condition key q-ak doesn&apos;t match the value XXXXXX</Message>
```

#### Possible cause

`q-ak` parameter input error.

#### Solution

1. Log in to the CAM console and go to the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page to view the key information.
2. Check whether the `q-ak` parameter is incorrectly set based on the key information:
 - Yes: change the value of the `q-ak` parameter to the correct SecretId.
 - No: [contact us](https://intl.cloud.tencent.com/contact-sales).

<span id="AccessDenied_Expiration"></span>
### Error message "You post object request has been expired, expiration time: 1621188104 but the time now : 1621245817"

When POST requests are initiated via COS APIs, the following information is displayed:

```
<Code>AccessDenied</Code>
<Message>You post object request has been expired, expiration time: 1621188104 but the time now : 1621245817</Message>
```


#### Possible cause

The value of `expiration` in the policy has expired.

#### Solution

Change the value of `expiration` in the policy.
>! The value of `expiration` must be later than the current time. The recommended value is a time 30 minutes later than the current time (UTC time).
>


<span id="SignatureDoesNotMatch_POSTSignature"></span>
### Error message "The Signature you specified is invalid."

When POST requests are initiated via COS APIs, the following information is displayed:

```
<Code>SignatureDoesNotMatch</Code>
<Message>The Signature you specified is invalid.</Message>
```

#### Possible cause

Signature calculation error.

#### Solution

Check whether the POST signature string generation rule is correct by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) :


<span id="InvalidPolicyDocument_JSONFormat"></span>
### Error message "You must provide condition if you specify a policy in post object request."

When POST requests are initiated via COS APIs, the following information is displayed:

```
<Code>InvalidPolicyDocument</Code>
<Message>You must provide condition if you specify a policy in post object request.</Message>
```


#### Possible cause

Policy format error.

#### Solution

Change the policy format to the standard JSON format by referring to [POST Object](https://intl.cloud.tencent.com/document/product/436/14690).


<span id="AccessDenied_BucketNotConsistent"></span>
### Error message "Condition key bucket doesn&apos;t match the value [bucket-appid]"

When POST requests are initiated via COS APIs, the following information is displayed:

```
<Code>AccessDenied</Code>
<Message>Condition key bucket doesn&apos;t match the value [bucket-appid]</Message>
```


#### Possible cause

The bucket in the policy is inconsistent with that in the request.

#### Solution

Use the bucket specified in the policy to initiate the request.


<span id="AccessDenied_Condition"></span>
### Error message "Condition key key doesn&apos;t match the value XXXXX"

When POST requests are initiated via COS APIs, the following information is displayed:

```
<Code>AccessDenied</Code>
<Message>Condition key key doesn&apos;t match the value XXXXX</Message>
```


#### Possible cause

The uploaded content does not comply with the policy.

#### Solution

Upload content that meets the conditions specified in the policy.


<span id="MalformedPOSTRequest_POSTBody"></span>
### Error message "The body of your POST request is not well-formed multipart/form-data."

When POST requests are initiated via COS APIs, the following information is displayed:

```
<Code>MalformedPOSTRequest</Code>
<Message>The body of your POST request is not well-formed multipart/form-data.</Message>
```

#### Possible cause

The POST body format is invalid.

#### Solution

Correct the body format by referring to [POST Object](https://intl.cloud.tencent.com/document/product/436/14690).




