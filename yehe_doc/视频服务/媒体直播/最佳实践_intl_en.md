## Step 1. Apply for an account.

1. Sign up for a DRMtoday account.
   1. Sign up for a DRMtoday account on the [DRMtoday product page](https://castlabs.com/drmtoday/).
      ![](https://main.qcloudimg.com/raw/b1fa760d75f68f27c4470bf52f81b800.png)
   2. After signing up, you will receive a DRMtoday account, along with the password and the dashboard address.
2. Request a FairPlay certificate.
   1. Go to the [Apple FairPlay official website](https://developer.apple.com/streaming/fps/).
   2. Click [Request FPS Deployment Package](https://idmsa.apple.com/IDMSWebAuth/signin.html?path=%2Fcontact%2Ffps%2F&appIdKey=891bd3417a7776362562d2197f89480a8547b108fd934911bcbea0110d07f757), enter and submit the information required.
      ![](https://main.qcloudimg.com/raw/9592e1021494896689ad0d7135f26560.png)
   3. Get the `FPS_Deployment_Package.zip` file.
   4. Decompress the file and create a local password-protected private key and CSR (certificate signing request) as described in the file.
   5. Submit the CSR to Apple as described in the file, and an application secret key (ASK) will be returned. Store it properly.
   6. Download the FairPlay certificate generated.

## Step 2. Upload FairPlay certificate to DRMtoday.

Go to the DRMtoday dashboard, and select **Configuration > DRM Settings**.
![](https://main.qcloudimg.com/raw/352f6e951f0ca3252c5bf346ad19464b.png)
Parameters:
- **Default IV**: leave it empty.

Check **Update certificate and keys**, and set the parameters as described below.

- **ASK**: the ASK obtained in step 1.2.5 in the hexadecimal format.
- **Provider certificate**: the FairPlay certificate downloaded in step 1.2.6. The certificate uploaded must be a PEM file. You can convert your certificate into a PEM file using OpenSSL on Linux. For example, for a certificate named `fairplay.cer`, the command for conversion is:
  	openssl x509 -inform der -in fairplay.cer -out fairplay.pem
- **Provider private key**: the password-protected private key created. The key must be in the PKCS#8 PEM format. You can convert a key into the required format using OpenSSL on Linux. For example, for a key file named `privatekey.pem`, the command for conversion is:
  	openssl rsa -in privatekey.pem -outform PEM -out out.pem

## Step 3. Configure Widevine or FairPlay key via DRMtoday API.

The operations in this step are based on DRMtoday’s official document [DRMtoday Key Ingestion](https://fe.staging.drmtoday.com/frontend/documentation/integration/key_ingestion.html).

1. CAS authentication
   DRMtoday uses CAS (Central Authentication Service) to protect its API from unauthorized access. For details, see [DRMtoday CAS Authentication](https://fe.staging.drmtoday.com/frontend/documentation/integration/cas_authentication.html).
   1. CAS login: send a HTTP POST request to the login address.
      Example:
      	curl -v 'https://auth.staging.drmtoday.com/cas/v1/tickets' -H 'Content-Type: application/x-www-form-urlencoded' -XPOST -d 'username=${username}&password=${password}'
      Parameters:
      - **username and password**: you may use your DRMtoday account and password or the API account and password created at DRMtoday. For details, see DRMtoday’s [document on API account creation](https://fe.staging.drmtoday.com/frontend/documentation/integration/dashboard.html?%20dummy#adding-accounts).
   2. CAS ticket retrieval: send a HTTP POST request to the location in the header of the response of the CAS login request.
      Example:
      	curl -v 'https://auth.staging.drmtoday.com/cas/v1/tickets/xxx' -H 'Content-Type: application/x-www-formurlencoded'-XPOST -d 'service=https://fe.staging.drmtoday.com/frontend/api/keys/v2/ingest/${merchantApiName}'
      Parameters:
      - **service**: the endpoint corresponding to the ingest key in **Dashboard > API **.
        ![](https://main.qcloudimg.com/raw/299f6fdcdfd5016a48c4b41f530e277a.png)

2. Key setting.
   After authentication, use the ingest key API to configure a Widevine or FairPlay key. For how to use the API, see [DRMtoday Key Ingestion](https://fe.staging.drmtoday.com/frontend/documentation/integration/key_ingestion.html).
   Example:
   	curl -v 'https://fe.staging.drmtoday.com/frontend/api/keys/v2/ingest/${merchant}?ticket=${ticket}' -H 'Content-Type: application/json' -H 'Accept: application/json' -XPOST -d '{"assets":[{"type":"CENC","assetId":"assettest","variantId":"varianttest","ingestKeys":[{"streamType":"VIDEO_AUDIO","algorithm":"AES","keyId":"MDAwMDAwMDAwMDAwMDAwMA==","key":"MDAwMDAwMDAwMDAwMDAwMA==","iv":"MDAwMDAwMDAwMDAwMDAwMA=="}]}]}'
   Parameters:
   -  **merchant**: the endpoint corresponding to the ingest key in the dashboard.
   -  **ticket**: the body of the response returned upon CAS ticket retrieval.
   -  **type**: `CENC`, which supports Widevine and FairPlay. Widevine encryption requires a `keyId` and `key`, and FairPlay encryption requires a `key` and `iv`.
   -  **keyId, key and iv**: must be encoded in the Base64 format. For example, `MDAwMDAwMDAwMDAwMDAwMA==` is ‘30303030303030303030303030303030` after converted into the hexadecimal format.

## Step 4. Configure DRM key with StreamLive.

Follow the instructions in the StreamLive [user guide]([Console Guide | Tencent Cloud](https://intl.cloud.tencent.com/document/product/1048/41760#4.-create-a-streamlive-channel)) to configure a StreamLive DRM key. See below for the settings.

- Enable **DRM**.
- For **Scheme**, select **Custom DRM Keys**.

FairPlay key:
![](https://main.qcloudimg.com/raw/d1fd0abc8a2c4b1aa970f74160641731.png)

- For **ContentId**, enter the `assetId` configured in step 3.2, in the hexadecimal format.
- For **Key**, enter the key configured in step 3.2, in the hexadecimal format.
- For **Iv**, enter the `iv` configured in step 3.2, in the hexadecimal format.

Widevine key:
![](https://main.qcloudimg.com/raw/d65d6a93e13b12d8014558a601a21692.png)

- For **ContentId**, enter the `assetId` configured in step 3.2, in the hexadecimal format.
- For **KeyId**, enter the `keyId` configured in step 3.2, in the hexadecimal format.
- For **Key**, enter the `key` configured in step 3.2, in the hexadecimal format.

## Step 5. Run playback test.

After configuring a playback address as instructed in the StreamLive user guide (for example, you can [ingest live streams to the StreamPackage channel](https://intl.cloud.tencent.com/document/product/1048/41760#6.-output-content-to-streampackage-through-streamlive), and [get the playback address via the StreamPackage endpoint](https://intl.cloud.tencent.com/document/product/1063/41787), you can use the [DRMtoday playback page](https://players.castlabs.com/presto/6.1.2/#/player/config) to run a playback test.
![](https://main.qcloudimg.com/raw/5b8b559d838497dd5b75cf9c7cedf363.png)
![](https://main.qcloudimg.com/raw/77249ddf9131bc9578bdb28fc3c37fb4.png)
Parameters:

- **Content URL**: the playback content URL
- **DRM Environment**: the DRM environment you use
- **Merchant**: name of the user at DRMtoday, which is often the same as `merchantApiName`
- **User ID and Session ID**: see the DRMtoday [configuration document](https://fe.staging.drmtoday.com/frontend/documentation/integration/dashboard.html#uisetting-Test_dummy) (when the License Delivery Authorization type is `Test_dummy`)
- **Asset ID**: the `assetId` configured in step 3.2
- **Variant ID**: the `variantId` configured in step 3.2
