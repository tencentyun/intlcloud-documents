## 소개

Go SDK는 클라이언트 암호화를 지원합니다. 업로드 시 파일을 암호화하고 다운로드 시 복호화하여 중요 데이터를 저장하는 클라이언트에 적합합니다.

클라이언트 암호화는 다음 방식만 지원합니다.
KMS 서비스 호스팅 키: KMS 서비스의 사용자 마스터 키 ID(CMK ID)를 SDK에 제공하기만 하면 됩니다. 이 방식을 사용하려면 KMS 서비스를 활성화해야 합니다. KMS 서비스 정보에 대한 자세한 내용은 [Tencent Cloud Key Management Service](https://intl.cloud.tencent.com/document/product/1030)를 참조하십시오.

## 주의 사항


암호화 데이터를 복사하거나 마이그레이션하는 경우 완전하고 정확한 암호화 메타 정보가 필요합니다. 사용자의 잘못된 점검으로 인해 암호화 메타 정보가 틀리거나 누락될 경우 암호화된 데이터를 해독할 수 없으므로 이로 인해 발생하는 모든 손해 및 결과는 사용자가 부담합니다.

## 업로드 암호화 프로세스
1. 파일 객체를 업로드하기 전에 무작위로 대칭 암호화 키를 생성합니다. 무작위로 생성한 키는 KMS 서비스를 통해 암호화되며 암호화된 결과는 객체의 메타데이터에 base64로 인코딩됩니다.
2. 파일 객체를 업로드합니다. 업로드 시 메모리에서 AES256 알고리즘을 사용해 암호화합니다.

## 다운로드 복호화 프로세스

1. 파일 메타데이터에서 암호화에 필요한 정보를 가져와 Base64로 디코딩 후 KMS 서비스(또는 사용자가 제공한 키)로 복호화하여 암호화된 데이터의 키를 얻습니다.
2. 키 쌍을 사용해 입력 스트림을 다운로드하고 AES256을 사용해 복호화하여 복호화된 파일 입력 스트림을 얻습니다.

## 요청 예시
전체 예시는 [클라이언트 암호화 - KMS 암호화 전체 예시](https://github.com/tencentyun/cos-go-sdk-v5/tree/master/example/crypto/crypto_sample.go)를 참조하십시오.


#### 요청 예시1: 간편 업로드 및 다운로드

```go
// 기존 클라이언트 생성
u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
c := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        SecretID: os.Getenv("SECRETID"),
        SecretKey: os.Getenv("SECRETKEY"),
    },
})

// Case1 객체 업로드
name := "test/example"

// 다음은 마스터 암호화 키를 확인할 수 있는 유일한 식별 정보입니다. 복호화할 때 동일한 식별 정보를 입력해야 합니다.
// KMS 암호화 시 이 정보는 EncryptionContext로 설정되며 최대 1024자까지 입력 가능합니다. Encrypt가 해당 매개변수를 지정한 경우 Decrypt 시 동일한 매개변수가 제공되어야 합니다.
materialDesc := make(map[string]string)
//materialDesc["desc"] = "material information of your master encrypt key"

// KMS 클라이언트 생성
kmsclient, _ := coscrypto.NewKMSClient(c.GetCredential(), "ap-guangzhou")
// KMS 마스터 암호화 키 생성, 식별 정보 materialDesc와 마스터 키가 일대일 대응
kmsID := os.Getenv("KMSID")
masterCipher, _ := coscrypto.CreateMasterKMS(kmsclient, kmsID, materialDesc)
// 암호화 클라이언트 생성
client := coscrypto.NewCryptoClient(c, masterCipher)

contentLength := 1024*1024*10 + 1
originData := make([]byte, contentLength)
_, err := rand.Read(originData)
f := bytes.NewReader(originData)
// 암호화 업로드
_, err = client.Object.Put(context.Background(), name, f, nil)
log_status(err)

// 복호화 다운로드
resp, err := client.Object.Get(context.Background(), name, nil)
log_status(err)
defer resp.Body.Close()
decryptedData, _ := ioutil.ReadAll(resp.Body)
if bytes.Compare(decryptedData, originData[rangeStart:rangeEnd+1]) != 0 {
    fmt.Println("Error: encryptedData != originData")
}
```

#### 요청 예시2: 파일 업로드 및 파일에 객체 다운로드

```go
// 기존 클라이언트 생성
u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
c := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        SecretID: os.Getenv("SECRETID"),
        SecretKey: os.Getenv("SECRETKEY"),
    },
})

// Case1 객체 업로드
name := "test/example"

// 다음은 마스터 암호화 키를 확인할 수 있는 유일한 식별 정보입니다. 복호화할 때 동일한 식별 정보를 입력해야 합니다.
// KMS 암호화 시 이 정보는 EncryptionContext로 설정되며 최대 1024자까지 입력 가능합니다. Encrypt가 해당 매개변수를 지정한 경우 Decrypt 시 동일한 매개변수가 제공되어야 합니다.
materialDesc := make(map[string]string)
//materialDesc["desc"] = "material information of your master encrypt key"

// KMS 클라이언트 생성
kmsclient, _ := coscrypto.NewKMSClient(c.GetCredential(), "ap-guangzhou")
// KMS 마스터 암호화 키 생성, 식별 정보 materialDesc와 마스터 키가 일대일 대응
kmsID := os.Getenv("KMSID")
masterCipher, _ := coscrypto.CreateMasterKMS(kmsclient, kmsID, materialDesc)
// 암호화 클라이언트 생성
client := coscrypto.NewCryptoClient(c, masterCipher)

// 암호화 업로드
_, err = client.Object.PutFromFile(context.Background(), name, filepath, nil)
if err! = nil {
    //ERROR
}

// 복호화 다운로드
_, err = client.Object.GetToFile(context.Background(), name, "./test.download", nil)
if err! = nil {
    //ERROR
}
```

#### 요청 예시3: 멀티파트 업로드

```go
// 기존 클라이언트 생성
u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
c := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        SecretID: os.Getenv("SECRETID"),
        SecretKey: os.Getenv("SECRETKEY"),
    },
})

// Case1 객체 업로드
name := "test/example"

// 다음은 마스터 암호화 키를 확인할 수 있는 유일한 식별 정보입니다. 복호화할 때 동일한 식별 정보를 입력해야 합니다.
// KMS 암호화 시 이 정보는 EncryptionContext로 설정되며 최대 1024자까지 입력 가능합니다. Encrypt가 해당 매개변수를 지정한 경우 Decrypt 시 동일한 매개변수가 제공되어야 합니다.
materialDesc := make(map[string]string)
//materialDesc["desc"] = "material information of your master encrypt key"

// KMS 클라이언트 생성
kmsclient, _ := coscrypto.NewKMSClient(c.GetCredential(), "ap-guangzhou")
// KMS 마스터 암호화 키 생성, 식별 정보 materialDesc와 마스터 키가 일대일 대응
kmsID := os.Getenv("KMSID")
masterCipher, _ := coscrypto.CreateMasterKMS(kmsclient, kmsID, materialDesc)
// 암호화 클라이언트 생성
client := coscrypto.NewCryptoClient(c, masterCipher)

filepath := "test"
stat, err := os.Stat(filepath)
if err! - nil {
    // ERROR
}
contentLength := stat.Size()

// 멀티파트 업로드
// 모든 멀티파트는 16바이트를 초과할 수 없으며 1MB 이상이어야 합니다.
partSize := (contentLength / 16 / 3) * 16
if partSize <int64(1024*1024) {
    partSize = int64(1024*1024)
}
cryptoCtx := coscrypto.CryptoContext{
    DataSize: contentLength,
    // 모든 멀티파트는 16바이트를 초과할 수 없습니다.
    PartSize: partSize,
}
// 분할된 데이터
_, chunks, _, err: = cos.SplitFileIntoChunks(filepath, cryptoCtx.PartSize)
if err! - nil {
    // ERROR
}

// init mulitupload
v, _, err := client.Object.InitiateMultipartUpload(context.Background(), name, nil, &cryptoCtx)
if err! - nil {
    // ERROR
}

// part upload
optcom := &cos.CompleteMultipartUploadOptions{}
for _, chunk := range chunks {
    fd, err := os.Open(filepath)
    if err! - nil {
        // ERROR
    }        
    opt := &cos.ObjectUploadPartOptions{
        ContentLength: chunk.Size,
    }
    fd.Seek(chunk.OffSet, os.SEEK_SET)
    resp, err := client.Object.UploadPart(context.Background(), name, v.UploadID, chunk.Number, cos.LimitReadCloser(fd, chunk.Size), opt, &cryptoCtx)
    if err! - nil {
        // ERROR
    }
    optcom.Parts = append(optcom.Parts, cos.Object{
        PartNumber: chunk.Number, ETag: resp.Header.Get("ETag"),
    })
}
// complete upload
_, _, err = client.Object.CompleteMultipartUpload(context.Background(), name, v.UploadID, optcom)
if err! - nil {
    // ERROR
}

_, err = client.Object.GetToFile(context.Background(), name, "test.download", nil)
if err! - nil {
    // ERROR
}
```
