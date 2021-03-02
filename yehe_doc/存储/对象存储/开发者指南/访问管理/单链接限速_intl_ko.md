## 단일 링크 속도 제한

COS는 다른 애플리케이션의 네트워크 대역폭을 고려해 파일을 업로드 및 다운로드할 때 발생하는 트래픽을 제어합니다. [PutObject](https://intl.cloud.tencent.com/document/product/436/7749), [PostObject](https://intl.cloud.tencent.com/document/product/436/14690), [GetObject](https://intl.cloud.tencent.com/document/product/436/7753), [UploadPart](https://intl.cloud.tencent.com/document/product/436/7750)에서 요청 시, x-cos-traffic-limit 매개변수를 포함하고, 속도값을 제한하면 COS는 설정한 속도 제한값에 따라 요청한 네트워크 대역폭을 제어합니다.

## 사용 설명

- 사용자는 PUT Object, POST Object, GET Object, Upload Part 요청을 실행할 때, x-cos-traffic-limit 요청 헤더(POST Object 요청 시, 테이블 필드 요청)를 포함해 해당 요청의 속도 제한값을 설정합니다. 해당 매개변수는 header와 요청 매개변수에 설정하거나 form 업로드 인터페이스를 사용할 경우, form field에서 설정할 수 있습니다.
- x-cos-traffic-limit 매개변수값은 숫자여야 하며, 기본 단위는 bit/s입니다.
- 속도 제한값은 819200 ~ 838860800, 즉 100KB/s ~ 100MB/s 범위에서 설정할 수 있으며, 이 범위를 넘으면 400 오류가 반환됩니다.
>?단위 환산법: 1MByte=1024KByte=1048576Byte=8388608bit

## API 사용 예시

다음은 API의 간편 업로드 예시입니다. 속도 제한값은 1048576 bit/s으로 128KB/s입니다.

```sh
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Content-Length: 13
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109068;1561116268&q-key-time=1561109068;1561116268&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=998bfc8836fc205d09e455c14e3d7e623bd2****
x-cos-traffic-limit: 1048576
```

