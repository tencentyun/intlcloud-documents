
## Suggestions for Dealing with Exceptions

If exceptional errors occur when you call KMS APIs to send requests from your application to the remote KMS server, you can deal with the errors as suggested below:
- **Cancel the call**: if an error shows that the failure is not temporary and persists after several re-executions, you need to terminate or cancel the application call and report the error.
- **Try again immediately**: if an uncommon error is returned, for example, network packets are damaged during transfer but still sent, in this case, you can try again immediately.
- **Increase delays between re-executions**: if an error is generally caused by connections, it indicates that the server is busy and needs to clear the loads first. You can try again in a while in such cases.

The following paragraphs introduce how to increase delays between re-executions. The delay can be gradually increased or scheduled (by implementing exponential backoff). As the frequency of KMS API calls is limited, you can increase delays between re-executions to avoid errors caused by high frequency.


## Exponential Backoff

### Pseudocode
```
// Gradually increase re-execution delays
InitDelayValue = 100
For(Retries = 0; Retries < MAX_RETRIES; Retries = Retries+1)
		wait for (2^Retries * InitDelayValue) milliseconds
		Status = KmsApiRequest()
		IF Status == SUCCESS
	        BREAK // Succeeded, stop calling the API again.
		ELSE IF Status = THROTTLED || Status == SERVER_NOT_READY
		    CONTINUE // Failed due to throttling or server busy, try again.
		ELSE
			BREAK // another error occurs, stop calling the API again.
		END IF
```

### Method
Python: implement exponential backoff for frequency errors in KMS API calls to `Encrypt`
```
# -*- coding: utf-8 -*-
import base64
import math
import time
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.common.profile.client_profile import ClientProfile
from tencentcloud.common.profile.http_profile import HttpProfile
from tencentcloud.kms.v20190118 import kms_client, models


def KmsInit(region="ap-guangzhou", secretId="", secretKey=""):
		  try:
				credProfile = credential.Credential(secretId, secretKey)
				client = kms_client.KmsClient(credProfile, region)
				return client
		  except TencentCloudSDKException as err:
				print(err)
				return None
				
def BackoffFunction(RetryCount):
			InitDelayValue = 100
			DelayTime = math.pow(2, RetryCount) * InitDelayValue
			return DelayTime
			
if __name__ == '__main__':
			# User-defined parameters
			secretId = "replace-with-real-secretId"
			secretKey = "replace-with-real-secretKey"
			region = "ap-guangzhou"
			keyId = "replace-with-realkeyid"
			plaintext = "abcdefg123456789abcdefg123456789abcdefg"
			Retries = 0
			MaxRetries = 10
			client = KmsInit(region, secretId, secretKey)
			req = models.EncryptRequest()
			req.KeyId = keyId
			req.Plaintext = base64.b64encode(plaintext)
			while Retries < MaxRetries:
				try:
					Retries += 1
					rsp = client.Encrypt(req)  # Call the API `Encrypt`
					print 'plaintext: ',plaintext,'CiphertextBlob: ',rsp.CiphertextBlob
					break
				except TencentCloudSDKException as err:
					if err.code == 'InternalError' or err.code == 'RequestLimitExceeded':
						if Retries == MaxRetries: 
							break
						time.sleep(BackoffFunction(Retries + 1))
						continue
					else:
						print(err)
						break
				except Exception as err:
					print(err)
					break
```

>!
> - To deal with other specific errors, you can directly modify the content of the statement `except`.
> - You can customize the schedule policy based on your code logic and business policy to set the optimal initial delay value (InitDelayValue) and the number of retries (Retries), preventing your business from being affected by a too-low or too-high threshold.
