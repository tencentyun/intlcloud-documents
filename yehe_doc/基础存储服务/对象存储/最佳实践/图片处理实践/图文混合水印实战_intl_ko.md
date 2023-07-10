## 작업 시나리오

CI의 기본 이미지 처리 기능으로 이미지에 [이미지 워터마크](https://intl.cloud.tencent.com/document/product/1045/33720) 또는 [텍스트 워터마크](https://intl.cloud.tencent.com/document/product/1045/33721)를 추가할 수 있습니다. 그러나 실제 비즈니스 시나리오에서는 이미지에 고정 Logo 워터마크와 동적으로 변경되는 텍스트 워터마크(사용자 이름)가 모두 포함될 수 있습니다. 이러한 시나리오를 위해 다음과 같은 통합 방법이 제공됩니다. 실제 비즈니스 시나리오에 따라 적절한 것을 선택할 수 있습니다.

## 메소드 비교

| 메소드 | 장점 | 단점 |
|---------|---------|---------|
| 1 | 통합 및 구현이 쉽습니다. | 워터마크 크기는 이미지 크기에 따라 동적으로 변경될 수 없으며, 채우기할 수 없습니다. |
| 2 | 이미지 크기가 자주 변경될 때 이미지에 더 잘 맞을 수 있습니다. | 통합이 어렵고 처리 요금이 두 번 청구됩니다. |


## 사용 방법

### 방법1: 파이프라인 연산자를 사용하여 URL 하나만으로 두 가지 유형의 워터마크 추가

CI(Cloud Infinite)의 기본 이미지 처리 기능을 통해 [파이프라인 연산자](https://intl.cloud.tencent.com/document/product/1045/33727) "|"를 사용할 수 있습니다. 처리 및 트래픽 요금의 일회성 요금으로, 단 한 번의 요청으로 이미지를 여러 번 처리합니다. 이 방법은 반복 요청으로 인한 대기 시간과 추가 요금을 크게 줄입니다.

#### 작업 순서

1. [이미지 워터마크](https://intl.cloud.tencent.com/document/product/1045/33720)에 설명된 대로 이미지 워터마크 매개변수를 정의합니다.
API 매개변수에 익숙하지 않은 경우 콘솔에서 스타일을 추가하여 [기본 처리](https://intl.cloud.tencent.com/document/product/1045/33443)에 설명된 대로 매개변수를 생성할 수 있습니다.

다음은 처리 매개변수입니다.
```
watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTgxMjU2MzguY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vbG9nby5wbmc/dissolve/60/dx/10/dy/50/gravity/southeast
```
>? 여기서 `aHR0cDovL2V4YW1wbGVzLTEyNTgxMjU2MzguY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vbG9nby5wbmc`는 이미지 워터마크(COS bucket에 저장된 이미지)의 URL 보안 base64 인코딩 URL입니다.
>
2. [텍스트 워터마크](https://intl.cloud.tencent.com/document/product/1045/33721)에 설명된 대로 텍스트 워터마크 매개변수를 정의합니다.
API 매개변수에 익숙하지 않은 경우 콘솔에서 스타일을 추가하여 [기본 처리](https://intl.cloud.tencent.com/document/product/1045/33443)에 설명된 대로 매개변수를 생성할 수 있습니다.

```
watermark/2/text/VUlOOiAxMjM0NTY3OA/font/SGVsdmV0aWNhLmRmb250/fontsize/36/fill/IzAwMDAwMA/dissolve/50/gravity/southeast/dx/10/dy/10
```
>? 여기서 `VUlOOiAxMjM0NTY3OA`는 `UIN: 12345678`의 URL 보안 base64 인코딩 텍스트입니다.
>
3. 파이프라인 연산자를 사용하여 이미지 및 텍스트 워터마크 매개변수를 연결합니다.
```
watermark/2/text/VUlOOiAxMjM0NTY3OA/font/SGVsdmV0aWNhLmRmb250/fontsize/36/fill/IzAwMDAwMA/dissolve/50/gravity/southeast/dx/10/dy/10|watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTgxMjU2MzguY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vbG9nby5wbmc/gravity/southeast/dx/10/dy/50/dissolve/60 
```
4. 이미지 다운로드 URL 끝에 연결된 매개변수를 추가합니다.
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/preview.png?watermark/2/text/VUlOOiAxMjM0NTY3OA/font/SGVsdmV0aWNhLmRmb250/fontsize/36/fill/IzAwMDAwMA/dissolve/50/gravity/southeast/dx/10/dy/10|watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTgxMjU2MzguY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vbG9nby5wbmc/gravity/southeast/dx/10/dy/50/dissolve/60 
```
혼합 워터마크 이미지를 가져올 수 있습니다.

URL을 단축하려면 [기본 처리](https://intl.cloud.tencent.com/document/product/1045/33443)의 지침에 따라 콘솔에서 `watermark1` 스타일로 이미지 워터마크(변경되지 않음)의 일부를 추가할 수 있습니다.

이런 식으로 URL은 다음과 같이 단축될 수 있습니다.
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/preview.png/watermark1?watermark/2/text/VUlOOiAxMjM0NTY3OA/font/SGVsdmV0aWNhLmRmb250/fontsize/36/fill/IzAwMDAwMA/dissolve/50/gravity/southeast/dx/10/dy/10
```
추후에 텍스트 콘텐츠를 변경해야 하는 경우 URL의 `VUlOOiAxMjM0NTY3OA`만 업데이트된 base64 코드로 바꾸면 됩니다. 예를 들어 `UIN: 88888888`은 `VUlOOiA4ODg4ODg4OA`로 인코딩되므로 텍스트를 바꾸려면 URL을 다음 콘텐츠로 변경하기만 하면 됩니다.
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/preview.png/watermark1?watermark/2/text/VUlOOiA4ODg4ODg4OA/font/SGVsdmV0aWNhLmRmb250/fontsize/36/fill/IzAwMDAwMA/dissolve/50/gravity/southeast/dx/10/dy/10
```



### 방법2: 텍스트 및 이미지 워터마크를 투명 이미지에 출력하고 이를 최종 이미지 워터마크로 사용

1. 400px * 400px의 투명 PNG 이미지를 [파일 관리](https://intl.cloud.tencent.com/document/product/1045/37766)의 지시에 따라 버킷에 업로드합니다.
예시: `https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/transparent.png`
2. **방법1의 1 - 3단계**에 설명된 대로 이미지 및 텍스트 워터마크 매개변수를 생성하고 연결합니다.
3. 투명한 PNG 이미지의 다운로드 URL 끝에 연결된 매개변수를 추가합니다.
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/transparent.png?watermark/2/text/VUlOOiAxMjM0NTY/font/SGVsdmV0aWNhLmRmb250/fontsize/48/fill/IzAwMDAwMA/dissolve/60/gravity/south/dx/0/dy/60|watermark/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTgxMjU2MzguY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vbG9nby5wbmc/gravity/center/dx/0/dy/0/dissolve/71
```


4. 투명 이미지를 이미지 워터마크로 사용하고 원본 이미지에 워터마크를 추가합니다.
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/preview.png?watermark/1/image/aHR0cDovL2V0ZXJuYXV4LTEzMDE0NTM1NTAuY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vdHJhbnNwYXJlbnQucG5nP3dhdGVybWFyay8yL3RleHQvVlVsT09pQXhNak0wTlRZL2ZvbnQvU0dWc2RtVjBhV05oTG1SbWIyNTAvZm9udHNpemUvNDgvZmlsbC9JekF3TURBd01BL2Rpc3NvbHZlLzYwL2dyYXZpdHkvc291dGgvZHgvMC9keS82MHx3YXRlcm1hcmsvMS9pbWFnZS9hSFIwY0RvdkwyVjBaWEp1WVhWNExURXpNREUwTlRNMU5UQXVZMjl6TG1Gd0xXZDFZVzVuZW1odmRTNXRlWEZqYkc5MVpDNWpiMjB2Ykc5bmJ5NXdibWMvZ3Jhdml0eS9jZW50ZXIvZHgvMC9keS8wL2Rpc3NvbHZlLzcx/gravity/southeast/dx/0/dy/0/dissolve/90
```


또한 `scatype` 매개변수를 사용하여 이미지 크기에 비례하여 이미지 워터마크의 크기를 조정하고 `batch` 매개변수를 사용하여 이미지 워터마크를 바둑판식으로 배열할 수 있습니다.
```
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/preview.png?watermark/1/image/aHR0cDovL2V0ZXJuYXV4LTEzMDE0NTM1NTAuY29zLmFwLWd1YW5nemhvdS5teXFjbG91ZC5jb20vdHJhbnNwYXJlbnQucG5nP3dhdGVybWFyay8yL3RleHQvVlVsT09pQXhNak0wTlRZL2ZvbnQvU0dWc2RtVjBhV05oTG1SbWIyNTAvZm9udHNpemUvNDgvZmlsbC9JekF3TURBd01BL2Rpc3NvbHZlLzYwL2dyYXZpdHkvc291dGgvZHgvMC9keS82MHx3YXRlcm1hcmsvMS9pbWFnZS9hSFIwY0RvdkwyVjBaWEp1WVhWNExURXpNREUwTlRNMU5UQXVZMjl6TG1Gd0xXZDFZVzVuZW1odmRTNXRlWEZqYkc5MVpDNWpiMjB2Ykc5bmJ5NXdibWMvZ3Jhdml0eS9jZW50ZXIvZHgvMC9keS8wL2Rpc3NvbHZlLzcx/scatype/3/spcent/30/gravity/southeast/dx/0/dy/0/dissolve/90/batch/1/degree/45
```


