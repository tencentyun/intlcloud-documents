## 소개

클라이언트와 서버 간에 데이터가 전송되면서 데이터에 오류가 발생하기도 합니다. COS는 [MD5 검증](https://intl.cloud.tencent.com/document/product/436/32467)으로 데이터 무결성을 검증하며, CRC64 검사 코드를 이용해 데이터 검사를 합니다.

COS는 새로 업로드되는 객체에 CRC64 계산을 실시하고, 그 결과를 객체의 속성으로 보관합니다. 이후 반환되는 응답 헤더에 x-cos-hash-crc64ecma가 포함되는데, 이 헤더는 업로드한 객체의 CRC64 값을 나타내며 [ECMA-182 표준](https://www.ecma-international.org/publications/standards/Ecma-182.htm)에 따라 계산하여 값을 얻습니다. CRC64의 특성상 런칭 이전 시점부터 COS의 객체에 존재하기 때문에 COS에서 객체의 CRC64 값을 계산하지 않습니다. 따라서 해당 유형의 객체를 획득할 때 CRC64 값이 반환되지 않습니다.

## 작업 설명

현재 CRC64를 지원하는 API는 다음과 같습니다.

- 간편 업로드 인터페이스
	- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)와 [POST Object](https://intl.cloud.tencent.com/document/product/436/14690): 반환된 응답 헤더에서 파일의 CRC64 검사 값을 획득할 수 있습니다.
- 멀티파트 업로드 인터페이스
	- [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750): COS에서 반환된 CRC64 값과 로컬에서 계산된 값을 비교 검증합니다.
	- [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742): 멀티파트 각각에 CRC64 속성이 있으면 객체의 CRC64 값이 반환됩니다. 하지만 일부 멀티파트에 CRC64 값이 없는 경우, 반환되지 않습니다.
- [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287)를 실행하면 이와 대응하는 CRC64 값이 반환됩니다.
- [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)를 실행할 때 원본 객체에 CRC64 값이 있으면 CRC64가 반환되고, 그렇지 않으면 반환되지 않습니다.
- [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745)와 [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)를 실행할 때 객체에 CRC64가 있으면 반환됩니다. 사용자는 COS에서 반환된 CRC64 값과 로컬에서 계산된 CRC64 값을 비교 검증할 수 있습니다.

## SDK 예시

#### 기능 설명

객체 업로드 및 다운로드 시 객체 데이터에 대한 CRC64 일관성 검사를 수행하는 데 사용됩니다.

#### 요청 예시

여기서는 단순 업로드 예시만 설명합니다. 다른 인터페이스도 같은 방식으로 사용합니다.

[//]: # (.cssg-snippet-put-object)
```js
cos.putObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: ’COS_REGION’,     /* 버킷이 위치한 리전. 필수 필드 */
    Key: ’exampleobject’,              /* 필수 */
    StorageClass: ’STANDARD’,
    Body: fileObject, // 파일 객체 업로드
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    if (err) {
      console.log(err);
    } else {
      // 올바르게 반환되려면 x-cos-hash-crc64ema 필드를 Expose-Headers에 추가해야 합니다.
      // 참고 문서: https://cloud.tencent.com/document/product/436/13318
      var crc64 = data.headers['x-cos-hash-crc64ecma'];
      console.log(crc64);
    }
});
```

