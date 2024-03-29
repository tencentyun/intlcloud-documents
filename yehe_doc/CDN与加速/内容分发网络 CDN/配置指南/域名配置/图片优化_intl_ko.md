
## 설정 시나리오
Tencent Cloud CDN으로 대용량 이미지를 배포할 때 이미지 최적화를 활성화할 수 있습니다. 이 기능은 지정된 요구 사항을 충족하는 이미지를 webp, guetzli 및 tpg 형식으로 압축하는 동시에 다운스트림 트래픽과 비용을 크게 줄일 수 있습니다. 

## 설정 가이드
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하고 왼쪽 사이드바에서 **도메인 관리**를 선택합니다. COS 오리진으로 구성된 도메인 이름 오른쪽의 **관리**를 클릭합니다. 표시되는 페이지에서 **이미지 최적화**를 선택합니다.
- COS V5 오리진으로 구성된 도메인 이름만 지원됩니다.
- 이 기능이 활성화되기 전에 CI 서비스가 아직 활성화되지 않은 경우 CDN 콘솔에서 활성화를 빠르게 완료할 수 있습니다.
- CI 서비스가 이미 활성화되어 있는 경우 이 기능을 바로 사용할 수 있습니다.

>?[Tencent Cloud CI](https://intl.cloud.tencent.com/products/ci)는 안전하고 안정적이며 효율적인 클라우드 데이터 처리 서비스를 제공합니다. 이미지(Webp, Guetzli, TPG) 처리 시 CI 서비스 요금이 발생합니다. 자세한 내용은 [Billing Overview](https://intl.cloud.tencent.com/document/product/1045/33431)를 참고하십시오.

### Webp 어댑티브
Webp 어댑티브가 활성화되면 다음 압축 요구 사항을 충족하는 이미지가 처리되어 반환됩니다. 이러한 요구 사항이 충족되지 않으면 원본 이미지가 반환됩니다.
- HTTP accept 헤더에는 image/webp가 포함되어 있습니다. 
- 이미지는 jpg, jpeg, bmp, gif 또는 png 형식입니다.

>! 
>- 발생한 비용은 CI-기본 이미지 처리 요금에 포함됩니다.
>- 처리할 이미지는 20MB 이하여야 하며 너비와 높이는 30000픽셀을 초과하지 않으며 총 1억 픽셀을 초과하지 않아야 합니다. 출력 이미지의 너비와 높이는 9999픽셀을 초과해서는 안 됩니다.
>- 애니메이션 이미지의 경우 총 픽셀 수(너비 * 높이 * 프레임 수)는 1억 픽셀(GIF 프레임 제한: 300)을 초과할 수 없습니다.

### Guetzli 어댑티브
CI에서 출시한 Guetzli 이미지 압축 기능은 시각적으로 무손실입니다. 다운스트림 트래픽을 줄이고 다운로드 속도를 높이기 위해 JPG 이미지를 높은 비율로 압축합니다. Guetzli는 특정 색상 영역 및 세부 정보에 대한 인간의 둔감함을 이용, 특정 세부 정보를 버려 품질을 변경하지 않고 다운로드 트래픽을 35%에서 50%까지 줄입니다.

Guetzli 어댑티브가 활성화되면 다음 압축 요구 사항을 충족하는 이미지가 처리되어 반환됩니다.
- HTTP accept 헤더에는 image/guetzli가 포함되어 있습니다.
- 이미지는 jpg 또는 jpeg 형식입니다.

> !
> - 발생한 요금은 CI 청구서의 청구 가능 항목 Guetzli 압축에 포함됩니다.
> - Guetzli를 활성화하면 이미지에 처음 액세스할 때 원본 JPG 이미지가 반환되고 Guetzli는 이미지를 비동기식으로 압축합니다. 압축이 완료된 후 이미지를 다시 요청하면 압축된 이미지가 반환됩니다.
> - 현재 Guetzli는 품질이 q>70, 픽셀 수가 400만 미만인 JPG 이미지를 처리할 수 있습니다.

### TPG 어댑티브

TPG 어댑티브는 CI에서 출시한 고급 이미지 압축 기능입니다. 이미지를 더 작은 이미지 크기의 TPG 형식으로 변환하여 다운로드 트래픽을 크게 줄이고 페이지 로드 속도를 향상시킵니다.

TPG 어댑티브가 활성화되면 다음 압축 요구 사항을 충족하는 이미지가 처리되어 반환됩니다.
- HTTP accept 헤더에는 image/tpg가 포함되어 있습니다.
- 이미지는 jpg, jpeg, bmp, gif, png 또는 webp 형식입니다.

> !발생한 요금은 CI-이미지 고급 압축 요금에 포함됩니다.

## 주의 사항
이미지 최적화가 활성화되면 요청 URL의 캐시 키가 변경되고 **구성된 캐시 키 규칙**과 충돌합니다. 이 경우 캐시 키 규칙이 더 높은 우선 순위를 갖습니다.
예를 들어, jpg 파일에 대해 이미지 최적화가 활성화된 경우 요청 URL `http://www.test.com/a.jpg?colour=red`가 `http://www.test.com/a.jpgxxxxxx?colour=red`로 변경되어 모든 파일에 대한 모든 매개변수를 무시하는 **구성된 캐시 키 규칙**과 충돌합니다. 이 경우 규칙이 실행되고 요청 URL은 결국 `http://www.test.com/a.jpgxxxxxx`로 변경됩니다.




