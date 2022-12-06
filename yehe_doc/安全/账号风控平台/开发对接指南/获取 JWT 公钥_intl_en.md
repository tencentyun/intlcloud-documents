## API Description
This API is used to use the JSON Web Token (JWT) public key to verify the ID Token and Access Token in JWT format.
>? The JWT key is automatically generated when the user directory is created, and the key is different for different user directories.

## Supported Applications
Web applications, single-page applications (SPA), mobile applications, and machine-to-machine (M2M) applications.

## Request Method
```
GET
```

## Request Path
```
/oauth2/jwks
```

## Sample Requests
```
GET /oauth2/jwks HTTP/1.1
Host: sample.portal.tencentciam.com
```

## Sample Success Responses
```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "Keys" : [ {
    "kty" : "RSA",
    "e" : "AQAB",
    "kid" : "f9694d93-d541-4985-88dc-42229873008e",
    "n" : "wYmf-IL7_pXqEjtfHme7KqS06hRQ0BzhTzORjgwnsJD_CPexMHQAd82vZfOQioW9oaMXTiSAtkXslxNIxKVjiYMVzTLHQ9nqCARHOAONiftvcOyMiDGwI_ZV2u2ltHCbQ1w8sMpREMxLiW46TYHANSQwgzg9gLojhzPEUmAS0ksTx3UURmQGLnFBEh6Ydbj8tPNnNxfZHRLtqTD0FwLpPrn3wJvQRxNk_fcrJexM5v96XdQ1SLhhcIAMyqU-_-3IkyWIcS-Z-EvZCiKNJPCfVIEpWdz0oQdGXdADSRU8cV_sl-YmUWSE355PSzK1UmbvNJWLMsO67ZsgZyetcvkaIw"
  } ]
}
```

## Response Parameters

| Parameter | Data Type | Description |
| :--------- | :------- | :----------------- |
| keys | Array | An array of public keys.   |
| keys[].kty | String | Key type, such as RSA. |
| keys[].kid | String | Key identifier.         |
| keys[].e | String | RSA public key.         |
| keys[].n | String | RSA public key.         |