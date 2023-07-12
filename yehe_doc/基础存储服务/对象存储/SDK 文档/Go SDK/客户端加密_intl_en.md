## Overview

The Go SDK supports client-side encryption. Files can be encrypted before the upload and decrypted during the download. Client-side encryption is suitable for users who store sensitive data.

Client-side encryption supports:
KMS managed keys: You can provide the ID of your KMS CMK to the SDK. To use this type of keys, the KMS service needs to be activated. For more information, please see [Key Management Service](https://intl.cloud.tencent.com/document/product/1030).

## Notes


When you copy or migrate encrypted data, note that you should ensure the integrity and accuracy of the cryptographic metadata. If any encrypted data cannot be decoded due to cryptographic metadata loss/corruption caused by your inappropriate maintenance, you shall bear all losses and consequences arising from it.

## Encryption upon Upload
1. Before each upload, a random symmetric key will be generated, which will be encrypted using the KMS service. KMS will then Base64-encode the key and store it in the object metadata.
2. During the upload, the file is encrypted in memory using the AES256 algorithm.

## Decryption upon Download

1. Get the necessary encryption information from the metadata of the file, Base64-decode it, and then decrypt it using the KMS or customer managed key to get the encryption key at upload.
2. Use the resulting key to decrypt the downloaded input stream using AES256.

## Sample Request
For the complete sample, please see [Client-Side Encryption - Full Demo of KMS Encryption]( https://github.com/tencentyun/cos-go-sdk-v5/tree/master/example/crypto/crypto_sample.go).


#### Sample 1. Simple upload and download

```go
// Create the original client.
u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
c := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
    SecretID:  os.Getenv("SECRETID"),
    SecretKey: os.Getenv("SECRETKEY"),
    },
})

// Sample 1. Upload an object.
name := "test/example"

// An identifier that determines a unique master encryption key, which also needs to be passed in during decryption.
// During KMS encryption, set it to EncryptionContext. Up to 1,024 characters are supported. If a value is specified in Encrypt, the same value should be passed to Decrypt.
materialDesc := make(map[string]string)
//materialDesc["desc"] = "material information of your master encrypt key"

// Create a KMS client.
kmsclient, _ := coscrypto.NewKMSClient(c.GetCredential(), "ap-guangzhou")
// Create the KMS master encryption key, whose identifier, materialDesc, should correspond to the master encryption key one to one.
kmsID := os.Getenv("KMSID")
masterCipher, _ := coscrypto.CreateMasterKMS(kmsclient, kmsID, materialDesc)
// Create an encryption client.
client := coscrypto.NewCryptoClient(c, masterCipher)

contentLength := 1024*1024*10 + 1
originData := make([]byte, contentLength)
_, err := rand.Read(originData)
f := bytes.NewReader(originData)
// Encrypt data upon upload.
_, err = client.Object.Put(context.Background(), name, f, nil)
log_status(err)

// Decrypt data upon download.
resp, err := client.Object.Get(context.Background(), name, nil)
log_status(err)
defer resp.Body.Close()
decryptedData, _ := ioutil.ReadAll(resp.Body)
if bytes.Compare(decryptedData, originData[rangeStart:rangeEnd+1]) != 0 {
    fmt.Println("Error: encryptedData != originData")
}
```

#### Sample 2. Uploading and downloading an object

```go
// Create the original client.
u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
c := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
    SecretID:  os.Getenv("SECRETID"),
    SecretKey: os.Getenv("SECRETKEY"),
    },
})

// Sample 1. Upload an object.
name := "test/example"

// An identifier that determines a unique master encryption key, which also needs to be passed in during decryption.
// During KMS encryption, set it to EncryptionContext. Up to 1,024 characters are supported. If a value is specified in Encrypt, the same value should be passed to Decrypt.
materialDesc := make(map[string]string)
//materialDesc["desc"] = "material information of your master encrypt key"

// Create a KMS client.
kmsclient, _ := coscrypto.NewKMSClient(c.GetCredential(), "ap-guangzhou")
// Create the KMS master encryption key, whose identifier, materialDesc, should correspond to the master encryption key one to one.
kmsID := os.Getenv("KMSID")
masterCipher, _ := coscrypto.CreateMasterKMS(kmsclient, kmsID, materialDesc)
// Create an encryption client.
client := coscrypto.NewCryptoClient(c, masterCipher)

// Encrypt data upon upload.
_, err = client.Object.PutFromFile(context.Background(), name, filepath, nil)
if err != nil {
    //ERROR
}

// Decrypt data upon download.
_, err = client.Object.GetToFile(context.Background(), name, "./test.download", nil)
if err != nil {
    //ERROR
}
```

#### Sample 3. Multipart upload

```go
// Create the original client.
u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
c := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
    SecretID:  os.Getenv("SECRETID"),
    SecretKey: os.Getenv("SECRETKEY"),
    },
})

// Sample 1. Upload an object.
name := "test/example"

// An identifier that determines a unique master encryption key, which also needs to be passed in during decryption.
// During KMS encryption, set it to EncryptionContext. Up to 1,024 characters are supported. If a value is specified in Encrypt, the same value should be passed to Decrypt.
materialDesc := make(map[string]string)
//materialDesc["desc"] = "material information of your master encrypt key"

// Create a KMS client.
kmsclient, _ := coscrypto.NewKMSClient(c.GetCredential(), "ap-guangzhou")
// Create the KMS master encryption key, whose identifier, materialDesc, should correspond to the master encryption key one to one.
kmsID := os.Getenv("KMSID")
masterCipher, _ := coscrypto.CreateMasterKMS(kmsclient, kmsID, materialDesc)
// Create an encryption client.
client := coscrypto.NewCryptoClient(c, masterCipher)

filepath := "test"
stat, err := os.Stat(filepath)
if err !- nil {
    // ERROR
}
contentLength := stat.Size()

// Upload parts.
// Each part should be aligned to 16 bytes and not smaller than 1 MB.
partSize := (contentLength / 16 / 3) * 16
if partSize < int64(1024*1024) {
    partSize = int64(1024*1024)
}
cryptoCtx := coscrypto.CryptoContext{
    DataSize: contentLength,
    // Each part should be aligned to 16 bytes.
    PartSize: partSize,
}
// Split the data.
_, chunks, _, err := cos.SplitFileIntoChunks(filepath, cryptoCtx.PartSize)
if err !- nil {
    // ERROR
}

// init mulitupload
v, _, err := client.Object.InitiateMultipartUpload(context.Background(), name, nil, &cryptoCtx)
if err !- nil {
    // ERROR
}

// part upload
optcom := &cos.CompleteMultipartUploadOptions{}
for _, chunk := range chunks {
    fd, err := os.Open(filepath)
    if err !- nil {
        // ERROR
    }        
    opt := &cos.ObjectUploadPartOptions{
        ContentLength: chunk.Size,
    }
    fd.Seek(chunk.OffSet, os.SEEK_SET)
    resp, err := client.Object.UploadPart(context.Background(), name, v.UploadID, chunk.Number, cos.LimitReadCloser(fd, chunk.Size), opt, &cryptoCtx)
    if err !- nil {
        // ERROR
    }
    optcom.Parts = append(optcom.Parts, cos.Object{
        PartNumber: chunk.Number, ETag: resp.Header.Get("ETag"),
    })
}
// complete upload
_, _, err = client.Object.CompleteMultipartUpload(context.Background(), name, v.UploadID, optcom)
if err !- nil {
    // ERROR
}

_, err = client.Object.GetToFile(context.Background(), name, "test.download", nil)
if err !- nil {
    // ERROR
}
```
