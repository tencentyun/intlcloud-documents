
## Overview

This document uses Java as an example to describe how to integrate the data reporting SDK for Java with the client to quickly report data to DataHub.

## Directions

### Step 1. Create an HTTP access point

Create an HTTP access point in the DataHub console as instructed in [Reporting over HTTP](https://intl.cloud.tencent.com/document/product/597/46807) and get the `DatahubId` identifying the reporting endpoint.

### Step 2. Import the SDK for Java

Import the data reporting SDK through Maven or Gradle into the Java project.

### Step 3. Report the data

After importing the SDK, you can call the `SendMessage` API of the SDK to report a single data entry or batch report data entries as follows:

1. Instantiate the authentication object.
2. Instantiate the client object.
3. Call `SendMessage` to request to report data.
4. Process the returned result.
<dx-codeblock>
:::  java
import com.tencentcloudapi.common.Credential;
import com.tencentcloudapi.common.profile.ClientProfile;
import com.tencentcloudapi.common.profile.HttpProfile;
import com.tencentcloudapi.common.exception.TencentCloudSDKException;
import com.tencentcloudapi.ckafka.v20190819.CkafkaClient;
import com.tencentcloudapi.ckafka.v20190819.models.*;

public class SendMessage
{
    public static void main(String [] args) {
        try{
            // Instantiate an authentication object. Pass in `secretID` and `secretKey` of your Tencent Cloud account as the input parameters and keep them confidential.
            // You can get them at https://console.intl.cloud.tencent.com/cam/capi
            Credential cred = new Credential("SecretId", "SecretKey");
            // (Optional) Instantiate an HTTP option
            HttpProfile httpProfile = new HttpProfile();
            httpProfile.setEndpoint("ckafka.tencentcloudapi.com");
            // (Optional) Instantiate a client option
            ClientProfile clientProfile = new ClientProfile();
            clientProfile.setHttpProfile(httpProfile);
            // Instantiate the client object of the requested product. `clientProfile` is optional
            CkafkaClient client = new CkafkaClient(cred, "ap-beijing", clientProfile);
            // Instantiate a request object. Each API corresponds to a request object
            SendMessageRequest req = new SendMessageRequest();
            req.setDataHubId("datahub-r6gkngy3");

            BatchContent[] batchContents1 = new BatchContent[2];
            BatchContent batchContent1 = new BatchContent();
            batchContent1.setBody("test1");
            batchContents1[0] = batchContent1;
    
            BatchContent batchContent2 = new BatchContent();
            batchContent2.setBody("test2");
            batchContents1[1] = batchContent2;
    
            req.setMessage(batchContents1);
    
            // The returned `resp` is an instance of `SendMessageResponse` which corresponds to the request object
            SendMessageResponse resp = client.SendMessage(req);
            // A string response packet in JSON format is output
            System.out.println(SendMessageResponse.toJsonString(resp));
        } catch (TencentCloudSDKException e) {
            System.out.println(e.toString());
        }
    }
}
:::
</dx-codeblock>


### Step 4. Query the message

After the data is sent, you can check whether it is sent successfully on the message query page. For more information, see [Querying Message](https://intl.cloud.tencent.com/document/product/597/39719).



## Source Code Demo
<dx-codeblock>
:::  Java
import com.tencentcloudapi.common.Credential;
import com.tencentcloudapi.common.profile.ClientProfile;
import com.tencentcloudapi.common.profile.HttpProfile;
import com.tencentcloudapi.common.exception.TencentCloudSDKException;
import com.tencentcloudapi.ckafka.v20190819.CkafkaClient;
import com.tencentcloudapi.ckafka.v20190819.models.*;

public class SendMessage
{
    public static void main(String [] args) {
        try{
            // Instantiate an authentication object. Pass in `secretID` and `secretKey` of your Tencent Cloud account as the input parameters and keep them confidential.
            // You can get them at https://console.intl.cloud.tencent.com/cam/capi
            Credential cred = new Credential("SecretId", "SecretKey");
            // (Optional) Instantiate an HTTP option
            HttpProfile httpProfile = new HttpProfile();
            httpProfile.setEndpoint("ckafka.tencentcloudapi.com");
            // (Optional) Instantiate a client option
            ClientProfile clientProfile = new ClientProfile();
            clientProfile.setHttpProfile(httpProfile);
            // Instantiate the client object of the requested product. `clientProfile` is optional
            CkafkaClient client = new CkafkaClient(cred, "ap-beijing", clientProfile);
            // Instantiate a request object. Each API corresponds to a request object
            SendMessageRequest req = new SendMessageRequest();
            req.setDataHubId("datahub-r6gkngy3");

            BatchContent[] batchContents1 = new BatchContent[2];
            BatchContent batchContent1 = new BatchContent();
            batchContent1.setBody("test1");
            batchContents1[0] = batchContent1;
    
            BatchContent batchContent2 = new BatchContent();
            batchContent2.setBody("test2");
            batchContents1[1] = batchContent2;
    
            req.setMessage(batchContents1);
    
            // The returned `resp` is an instance of `SendMessageResponse` which corresponds to the request object
            SendMessageResponse resp = client.SendMessage(req);
            // A string response packet in JSON format is output
            System.out.println(SendMessageResponse.toJsonString(resp));
        } catch (TencentCloudSDKException e) {
            System.out.println(e.toString());
        }
    }
}
:::
::: Python
import json
from tencentcloud.common import credential
from tencentcloud.common.profile.client_profile import ClientProfile
from tencentcloud.common.profile.http_profile import HttpProfile
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.ckafka.v20190819 import ckafka_client, models
try:
    cred = credential.Credential("SecretId", "SecretKey")
    httpProfile = HttpProfile()
    httpProfile.endpoint = "ckafka.tencentcloudapi.com"

    clientProfile = ClientProfile()
    clientProfile.httpProfile = httpProfile
    client = ckafka_client.CkafkaClient(cred, "ap-beijing", clientProfile)
    
    req = models.SendMessageRequest()
    params = {
        "DataHubId": "datahub-r6gkngy3",
        "Message": [
            {
                "Body": "test1"
            },
            {
                "Body": "test2"
            }
        ]
    }
    req.from_json_string(json.dumps(params))
    
    resp = client.SendMessage(req)
    print(resp.to_json_string())

except TencentCloudSDKException as err:
    print(err)
:::
::: Node.JS
// Depends on tencentcloud-sdk-nodejs version 4.0.3 or higher
const tencentcloud = require("tencentcloud-sdk-nodejs");

const CkafkaClient = tencentcloud.ckafka.v20190819.Client;

const clientConfig = {
  credential: {
    secretId: "SecretId",
    secretKey: "SecretKey",
  },
  region: "ap-beijing",
  profile: {
    httpProfile: {
      endpoint: "ckafka.tencentcloudapi.com",
    },
  },
};

const client = new CkafkaClient(clientConfig);
const params = {
    "DataHubId": "datahub-r6gkngy3",
    "Message": [
        {
            "Body": "test1"
        },
        {
            "Body": "test2"
        }
    ]
};
client.SendMessage(params).then(
  (data) => {
    console.log(data);
  },
  (err) => {
    console.error("error", err);
  }
);
:::
::: PHP
<?php
require_once 'vendor/autoload.php';
use TencentCloud\Common\Credential;
use TencentCloud\Common\Profile\ClientProfile;
use TencentCloud\Common\Profile\HttpProfile;
use TencentCloud\Common\Exception\TencentCloudSDKException;
use TencentCloud\Ckafka\V20190819\CkafkaClient;
use TencentCloud\Ckafka\V20190819\Models\SendMessageRequest;
try {

    $cred = new Credential("SecretId", "SecretKey");
    $httpProfile = new HttpProfile();
    $httpProfile->setEndpoint("ckafka.tencentcloudapi.com");
      
    $clientProfile = new ClientProfile();
    $clientProfile->setHttpProfile($httpProfile);
    $client = new CkafkaClient($cred, "ap-beijing", $clientProfile);
    
    $req = new SendMessageRequest();
    
    $params = array(
        "DataHubId" => "datahub-r6gkngy3",
        "Message" => array(
            array(
                "Body" => "test1"
            ),
            array(
                "Body" => "test2"
            )
        )
    );
    $req->fromJsonString(json_encode($params));
    
    $resp = $client->SendMessage($req);
    
    print_r($resp->toJsonString());
}
catch(TencentCloudSDKException $e) {
    echo $e;
}
:::
::: GoLang
package main

import (
        "fmt"

        "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
        "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/errors"
        "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/profile"
        ckafka "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/ckafka/v20190819"
)

func main() {

        credential := common.NewCredential(
                "SecretId",
                "SecretKey",
        )
        cpf := profile.NewClientProfile()
        cpf.HttpProfile.Endpoint = "ckafka.tencentcloudapi.com"
        client, _ := ckafka.NewClient(credential, "ap-beijing", cpf)
    
        request := ckafka.NewSendMessageRequest()
        
        request.DataHubId = common.StringPtr("datahub-r6gkngy3")
        request.Message = []*ckafka.BatchContent {
                &ckafka.BatchContent {
                        Body: common.StringPtr("test1"),
                },
                &ckafka.BatchContent {
                        Body: common.StringPtr("test2"),
                },
        }
    
        response, err := client.SendMessage(request)
        if _, ok := err.(*errors.TencentCloudSDKError); ok {
                fmt.Printf("An API error has returned: %s", err)
                return
        }
        if err != nil {
                panic(err)
        }
        fmt.Printf("%s", response.ToJsonString())
} 
:::
:::  .Net
using System;
using System.Threading.Tasks;
using TencentCloud.Common;
using TencentCloud.Common.Profile;
using TencentCloud.Ckafka.V20190819;
using TencentCloud.Ckafka.V20190819.Models;

namespace TencentCloudExamples
{
    class SendMessage
    {
        static void Main(string[] args)
        {
            try
            {
                Credential cred = new Credential {
                    SecretId = "SecretId",
                    SecretKey = "SecretKey"
                };

                ClientProfile clientProfile = new ClientProfile();
                HttpProfile httpProfile = new HttpProfile();
                httpProfile.Endpoint = ("ckafka.tencentcloudapi.com");
                clientProfile.HttpProfile = httpProfile;
    
                CkafkaClient client = new CkafkaClient(cred, "ap-beijing", clientProfile);
                SendMessageRequest req = new SendMessageRequest();
                req.DataHubId = "datahub-r6gkngy3";
                BatchContent batchContent1 = new BatchContent();
                batchContent1.Body = "test1";
    
                BatchContent batchContent2 = new BatchContent();
                batchContent2.Body = "test2";
                req.Message = new BatchContent[] { batchContent1, batchContent2 };
    
                SendMessageResponse resp = client.SendMessageSync(req);
                Console.WriteLine(AbstractModel.ToJsonString(resp));
            }
            catch (Exception e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.Read();
        }
    }
}
:::
::: C++
#include <tencentcloud/core/Credential.h>
#include <tencentcloud/core/profile/ClientProfile.h>
#include <tencentcloud/core/profile/HttpProfile.h>
#include <tencentcloud/ckafka/v20190819/CkafkaClient.h>
#include <tencentcloud/ckafka/v20190819/model/SendMessageRequest.h>
#include <tencentcloud/ckafka/v20190819/model/SendMessageResponse.h>
#include <iostream>
#include <string>
#include <vector>

using namespace TencentCloud;
using namespace TencentCloud::Ckafka::V20190819;
using namespace TencentCloud::Ckafka::V20190819::Model;
using namespace std;

int main() {

        Credential cred = Credential("SecretId", "SecretKey");
    
        HttpProfile httpProfile = HttpProfile();
        httpProfile.SetEndpoint("ckafka.tencentcloudapi.com");
    
        ClientProfile clientProfile = ClientProfile();
        clientProfile.SetHttpProfile(httpProfile);
        CkafkaClient client = CkafkaClient(cred, "ap-beijing", clientProfile);
    
        SendMessageRequest req = SendMessageRequest();
        
        req.SetDataHubId("datahub-r6gkngy3");
        BatchContent batchContent1;
        batchContent1.SetBody("test1");
        BatchContent batchContent2;
        batchContent2.SetBody("test2");
    
        vector<BatchContent> batchContents1 = {batchContent1, batchContent2};
        req.SetMessage(batchContents1);
    
        auto outcome = client.SendMessage(req);
        if (!outcome.IsSuccess())
        {
            cout << outcome.GetError().PrintAll() << endl;
            return -1;
        }
        SendMessageResponse resp = outcome.GetResult();
        cout << resp.ToJsonString() << endl;
    
    return 0;
}
:::
</dx-codeblock>



