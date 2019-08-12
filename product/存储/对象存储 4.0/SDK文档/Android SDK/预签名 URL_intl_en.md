## Overview
The SDK for Android provides APIs to get object URLs and pre-signed request URLs.

## Getting an Object URL
```java
string getAccessUrl(CosXmlRequest cosXmlRequest);
```

## Getting a Pre-signed Request URL 
```java
String getPresignedURL(CosXmlRequest cosXmlRequest) throws CosXmlClientException;
```
### Parameter Descriptions
| Parameter Name | Type | Description |
|-----|-----|----|
|cosXmlRequest|CosXmlRequest| Request object |
|presignedUrlRequest |PresignedUrlRequest | Pre-signed URL instance |
|checkParameterListForSing |`Set<String>`| Request parameter to be verified in the signature |
|checkHeaderListForSign |`Set<String>`| Request header to be verified in the signature |

### PresignedUrlRequest Structure Description
The corresponding pre-signed request URL is obtained through the PresignedUrlRequest object for sending the request.

| Parameter Name | Type | Description |
|-----|-----|----|
|bucket|string| Bucket name for the COS XML API in the format of `<BucketName-APPID>`, such as examplebucket-1250000000 |
|requestMethod|string| HTTP request method, such as GET (for download) |
|cosPath |string| Object key, i.e. position identifier of the object in the bucket |
|checkParameterListForSing |`Set<String>`| Request parameter to be verified in the signature |
|checkHeaderListForSign |`Set<String>`| Request header to be verified in the signature |

## Example of Getting a Pre-signed Request

```java
Method 1. Construct a pre-request using PresignedUrlRequest
try{
String bucket = "examplebucket-1250000000"; // Bucket name
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, such as cosPath = "text.txt";
String method = "GET"; // HTTP method of the request, such as GET for download and PUT for upload
PresignedUrlRequest presignedUrlRequest = new PresignedUrlRequest(bucket, cosPath);
presignedUrlRequest.setRequestMethod(method);

//Set<String> checkParameterListForSing = new HashSet<String>();
//Set<String> checkHeaderListForSign = new HashSet<String>();
//presignedUrlRequest.setSignParamsAndHeaders(checkParameterListForSing, checkHeaderListForSign);

String urlWithSign = cosXmlService.getPresignedURL(presignedUrlRequest);
}catch(Exception ex){
Log.d("TEST", ex.getMessage());
}


Method 2. Directly use the corresponding request such as PutObjectRequest and GetObjectRequest
try{
PutObjectRequest putObjectRequest;
String urlWithSign = cosXmlService.getPresignedURL(putObjectRequest);
}catch(Exception ex){
Log.d("TEST", ex.getMessage());
}
```
## Example of Pre-signing a Request Using a Permanent Key

### Sample Request for Upload
```java
try {
	// Initialize CosXmlService with a permanent key
	Context context = getApplicationContext(); // application context
	String bucket = "examplebucket-1250000000"; // Bucket name
	String region = Region.AP_Guangzhou.getRegion();
	String appid = "1250000000";
	String secretId = "COS_SECRETID"; // "TencentCloud API key's SecretId";
	String secretKey = "COS_SECRETKEY"; //"TencentCloud API key's SecretKey";
	long durationSecond = 600;  // Validity period of the secretKey in seconds
	// Initialize config
	CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
					.isHttps(true)  // Set HTTPS request. The default value is HTTP request
					.setRegion(region)
					.setDebuggable(true)
					.builder();
	// Initialize QCloudCredentialProvider with a permanent key
	QCloudCredentialProvider qCloudCredentialProvider = new ShortTimeCredentialProvider(secretId, secretKey, durationSecond);
	// Initialize CosXmlService
	CosXmlService cosXmlService = new CosXmlService(context, serviceConfig, qCloudCredentialProvider);

	String cosPath = "exampleobject"; // Position identifier of the object in the bucket, such as cosPath = "text.txt";
	String method = "PUT"; // HTTP method of the request
	PresignedUrlRequest presignedUrlRequest = new PresignedUrlRequest(bucket, cosPath);
	presignedUrlRequest.setRequestMethod(method);

	String urlWithSign = cosXmlService.getPresignedURL(presignedUrlRequest); // Upload the pre-signed URL (signed URL calculated using the permanent key method)

	//String urlWithSign = cosXmlService.getPresignedURL(putObjectRequest)； // Use PutObjectRequest directly

	String srcPath = Environment.getExternalStorageDirectory().getPath() + "/exampleobject";
	PutObjectRequest putObjectRequest = new PutObjectRequest(null, null, srcPath);
	// Set the pre-signed upload request URL
	putObjectRequest.setRequestURL(urlWithSign);
	// Set progress callback
	putObjectRequest.setProgressListener(new CosXmlProgressListener() {
			@Override
			public void onProgress(long progress, long max) {
					// todo Do something to update progress...
			}
	});
	// Use the sync method to upload
	PutObjectResult putObjectResult = cosXmlService.putObject(putObjectRequest);
	} catch (CosXmlClientException e) {
	e.printStackTrace();
	} catch (CosXmlServiceException e) {
	e.printStackTrace();
}
```

### Sample Download Request
```java
try
{
	// Initialize CosXmlService with a permanent key
	Context context = getApplicationContext(); // application context
	String bucket = "examplebucket-1250000000"; // Bucket name
	String region = Region.AP_Guangzhou.getRegion();
	String appid = "1250000000";
	String secretId = "COS_SECRETID"; // "TencentCloud API key's SecretId";
	String secretKey = "COS_SECRETKEY"; //"TencentCloud API key's SecretKey";
	long durationSecond = 600;  // Validity period of the secretKey in seconds
	// Initialize config
	CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
					.isHttps(true)  // Set HTTPS request. The default value is HTTP request
					.setRegion(region)
					.setDebuggable(true)
					.builder();
	// Initialize QCloudCredentialProvider with a permanent key
	QCloudCredentialProvider  qCloudCredentialProvider = new ShortTimeCredentialProvider(secretId, secretKey, durationSecond);
	// Initialize CosXmlService
	CosXmlService cosXmlService = new CosXmlService(context, serviceConfig, qCloudCredentialProvider);

	String cosPath = "exampleobject"; // Position identifier of the object in the bucket, such as cosPath = "text.txt";
	String method = "GET"; // HTTP method of the request
	PresignedUrlRequest presignedUrlRequest = new PresignedUrlRequest(bucket, cosPath);
	presignedUrlRequest.setRequestMethod(method);

	String urlWithSign = cosXmlService.getPresignedURL(presignedUrlRequest); // Upload the pre-signed URL (signed URL calculated using the permanent key method)

	//String urlWithSign = cosXmlService.getPresignedURL(getObjectRequest)； // Use GetObjectRequest directly

	String savePath = Environment.getExternalStorageDirectory().getPath(); // Local path
	String saveFileName = "exampleobject"; // Local filename
	GetObjectRequest getObjectRequest = new GetObjectRequest(null, null, savePath, saveFileName);

	// Set the pre-signed upload request URL
	getObjectRequest.setRequestURL(urlWithSign);
	// Set progress callback
	getObjectRequest.setProgressListener(new CosXmlProgressListener() {
			@Override
			public void onProgress(long progress, long max) {
					// todo Do something to update progress...
			}
	});
	// Use the sync method to download
	GetObjectResult getObjectResult =cosXmlService.getObject(getObjectRequest);
	} catch (CosXmlClientException e) {
	e.printStackTrace();
	} catch (CosXmlServiceException e) {
	e.printStackTrace();
}
```


## Example of Pre-signing a Request Using a Temporary Key

### Sample Request for Upload
```java
try
{
	// Initialize CosXmlService with a temporary key
	Context context = getApplicationContext(); // application context
	String bucket = "examplebucket-1250000000"; // Bucket name
	String region = Region.AP_Guangzhou.getRegion();
	String appid = "1250000000";
	string secretId = "COS_SECRETID"; // Temporary key's SecretId
	string secretKey = "COS_SECRETKEY"; // Temporary key's SecretKey
	String sessionToken = "TOKEN"; // Temporary key's Token
	long startTime = 1555054436;  // Start timestamp of validity of the temporary key
	long expiredTime = 1555055036;// End timestamp of validity of the temporary key
	// Initialize config
	CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
		.isHttps(true)  // Set HTTPS request. The default value is HTTP request
		.setAppid(appid)
		.setRegion(region)
		.setDebuggable(true)
		.builder();
	// Initialize QCloudCredentialProvider with a temporary key
	QCloudCredentialProvider  qCloudCredentialProvider = = new BasicLifecycleCredentialProvider() {
          @Override
          protected QCloudLifecycleCredentials fetchNewCredentials() throws QCloudClientException {
              return new SessionQCloudCredentials(secretId, secretKey, sessionToken, startTime, expiredTime);
          }
      };
	// Initialize CosXmlService
	CosXmlService cosXmlService = new CosXmlService(context, serviceConfig, qCloudCredentialProvider);

	String cosPath = "exampleobject"; // Position identifier of the object in the bucket, such as cosPath = "text.txt";
	String method = "PUT"; // HTTP method of the request
	PresignedUrlRequest presignedUrlRequest = new PresignedUrlRequest(bucket, cosPath);
	presignedUrlRequest.setRequestMethod(method);
	
	String urlWithSign = cosXmlService.getPresignedURL(presignedUrlRequest); // Upload the pre-signed URL (signed URL calculated using the permanent key method)

	//String urlWithSign = cosXmlService.getPresignedURL(putObjectRequest)； // Use PutObjectRequest directly

	string srcPath = Environment.getExternalStorageDirectory().getPath() + "/exampleobject";
	PutObjectRequest putObjectRequest = new PutObjectRequest(null, null, srcPath);
	// Set the pre-signed upload request URL
	putObjectRequest.setRequestURL(urlWithSign);
	// Set progress callback
	putObjectRequest.setProgressListener(new CosXmlProgressListener() {
	    @Override
	    public void onProgress(long progress, long max) {
	        // todo Do something to update progress...
	    }
	});
	// Use the sync method to upload
	PutObjectResult putObjectResult = cosXmlService.putObject(putObjectRequest);
} catch (CosXmlClientException e) {
	e.printStackTrace();
} catch (CosXmlServiceException e) {
	e.printStackTrace();
}
```

### Sample Download Request
```java
try
{
	// Initialize CosXmlService with a temporary key
	Context context = getApplicationContext(); // application context
	String bucket = "examplebucket-1250000000"; // Bucket name
	String region = Region.AP_Guangzhou.getRegion();
	String appid = "1250000000";
	String secretId = "COS_SECRETID"; // Temporary key's SecretId
	string secretKey = "COS_SECRETKEY"; // Temporary key's SecretKey
	String sessionToken = "TOKEN"; // Temporary key's Token
	long startTime = 1555054436;  // Start timestamp of validity of the temporary key
	long expiredTime = 1555055036;// End timestamp of validity of the temporary key
	// Initialize config
	CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
					.isHttps(true)  // Set HTTPS request. The default value is HTTP request
					.setRegion(region)
					.setDebuggable(true)
					.builder();
	// Initialize QCloudCredentialProvider with a temporary key
	QCloudCredentialProvider  qCloudCredentialProvider = new BasicLifecycleCredentialProvider() {
	@Override
	protected QCloudLifecycleCredentials fetchNewCredentials() throws QCloudClientException {
			return new SessionQCloudCredentials(secretId, secretKey, sessionToken, startTime, expiredTime);
	}
	};
	// Initialize CosXmlService
	CosXmlService cosXmlService = new CosXmlService(context, serviceConfig, qCloudCredentialProvider);

	String cosPath = "exampleobject"; // Position identifier of the object in the bucket, such as cosPath = "text.txt";
	String method = "PUT"; // HTTP method of the request
	PresignedUrlRequest presignedUrlRequest = new PresignedUrlRequest(bucket, cosPath);
	presignedUrlRequest.setRequestMethod(method);

	String urlWithSign = cosXmlService.getPresignedURL(presignedUrlRequest); // Upload the pre-signed URL (signed URL calculated using the permanent key method)

	//String urlWithSign = cosXmlService.getPresignedURL(putObjectRequest)； // Use PutObjectRequest directly

	String srcPath = Environment.getExternalStorageDirectory().getPath() + "/exampleobject";
	PutObjectRequest putObjectRequest = new PutObjectRequest(null, null, srcPath);
	// Set the pre-signed upload request URL
	putObjectRequest.setRequestURL(urlWithSign);
	// Set progress callback
	putObjectRequest.setProgressListener(new CosXmlProgressListener() {
			@Override
			public void onProgress(long progress, long max) {
					// todo Do something to update progress...
			}
	});
	// Use the sync method to upload
	PutObjectResult putObjectResult = cosXmlService.putObject(putObjectRequest);
	} catch (CosXmlClientException e) {
	e.printStackTrace();
	} catch (CosXmlServiceException e) {
	e.printStackTrace();
}
```
