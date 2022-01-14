## 소개
클라이언트에서 업로드하든 서버에서 업로드하든 관계없이 파일 전송 중에 다음과 같은 일반적인 품질 문제가 발생할 수 있습니다.

1. 파일 업로드가 느린 이유는 무엇입니까?
2. 업로드 속도를 높이는 방법은 무엇입니까?
3. 업로드 성공률을 높이는 방법은 무엇입니까?
4. 약한 네트워크 환경에서 모바일 장치의 업로드 실패를 수정하는 방법은 무엇입니까?

업로드 품질을 측정하는 지표에는 업로드 속도와 성공률이 포함됩니다.
- 업로드 속도는 가장 직관적인 방식으로 사용자 경험에 영향을 미치는 경우가 많습니다. 예를 들어, 사용자가 50MB의 동영상을 업로드하고 30분 후에도 완료되지 않으면 인내심을 잃어 고객 손실 가능성으로 이어질 수 있습니다.
- 업로드 성공률은 서비스 품질을 보장합니다. 네트워크 문제로 인해 초기 업로드가 실패한 후 사용자가 다시 업로드를 시작할 가능성이 줄어듭니다. 즉각적인 결과는 사용자 불만입니다. 따라서 높은 업로드 성공률을 보장하는 것이 가장 기본적인 요구 사항입니다.

본문은 VOD 업로드 시나리오에서 발생하는 문제의 원인과 해결 방법을 설명합니다. 실제 비즈니스 시나리오를 기반으로 비교하고 적절한 솔루션을 선택하여 업로드 품질을 개선할 수 있습니다.

## 업로드 품질에 영향을 미치는 요소

### 네트워크 대역폭
네트워크 대역폭은 시간 단위로 전송할 수 있는 데이터의 양을 나타냅니다. 대역폭이 높을수록 시간 단위당 업로드되는 데이터의 양이 많아지고 업로드 속도가 빨라집니다. 업로드는 엔드 투 엔드 활동이므로 각 엔드의 대역폭이 업로드 품질에 영향을 미칩니다. VOD의 백엔드 서버는 현재 충분한 대역폭을 가지고 있으므로 업로드 품질은 사용자측 대역폭에 따라 다를 가능성이 큽니다.

### 사용자와 스토리지 센터 사이의 거리
업로드된 파일은 결국 VOD의 스토리지 센터에 저장해야 합니다. 사용자가 VOD를 활성화하면 VOD는 기본적으로 **충칭** 리전을 스토리지 센터로 할당합니다. 사용자와 스토리지 센터 사이의 거리는 네트워크 연결 길이에 영향을 줍니다.

예를 들어, 베이징에서 충칭으로 파일을 업로드할 때 동일한 파일을 청두에서 충칭으로 업로드하는 것보다 링크 길이가 길어지고 거리가 멀어질수록 영향 요인이 증가하여 결국 업로드 속도가 느려집니다. 긴 연결로 인해 전송 중 네트워크 지터 및 패킷 손실과 같은 문제도 업로드 성공률에 영향을 미칩니다. 짧은 연결의 경우에도 이러한 문제가 발생할 수 있지만 발생 확률은 긴 연결보다 훨씬 낮습니다. 사용자와 스토리지 센터 사이의 거리를 줄이는 것은 업로드 품질을 향상시키는 핵심 단계입니다.

### 약한 네트워크
약한 네트워크는 지연 및 패킷 손실률이 높은 네트워크 상태를 말하며 일반적으로 ‘느린 인터넷 액세스’라고 합니다. 이 문제는 엘리베이터 및 지하철과 같은 실생활에서 매우 일반적입니다. 주요 원인은 영향을 받는 환경에서 수신 불량으로 인해 데이터 패킷 전송이 느리거나 실패하기 때문입니다. 이 시나리오는 특히 현재 모바일 인터넷 시대에 클라이언트에서 업로드할 때 일반적입니다. 취약한 네트워크는 업로드 성공률을 향상시키는 데 가장 극복하기 어려운 문제로 많은 개발자를 괴롭히고 있습니다.

## 해결 방안

### 동시 업로드
네트워크 대역폭이 충분하지 않은 시나리오의 경우 직접적인 솔루션은 더 많은 대역폭을 적용하는 것입니다. 그러나 대역폭이 제한된 네트워크에서 업로드를 위한 대역폭을 어떻게 최대한 활용하느냐는 해결해야 할 문제입니다. 동시 업로드는 두 가지 수준으로 나눌 수 있습니다.
- 파일 레벨, 즉 여러 파일이 동시에 업로드됩니다.
- 파트 레벨, 즉 단일 파일의 여러 파트가 동시에 업로드됩니다.

두 레벨 모두에서 해당하는 동시 수를 조정하여 대역폭 활용을 개선할 수 있습니다.

#### 파일 동시 업로드
파일 동시 업로드는 여러 프로세스 또는 스레드를 사용하여 동시에 업로드 작업을 시작하는 것을 말합니다. 현재 VOD는 이 모드에 대한 관련 SDK 패키지를 제공하지 않습니다. 특정 프로그래밍 언어의 특성을 참고하여 이 기능을 구현할 수 있습니다. 다음은 VOD [SDK for Java](https://intl.cloud.tencent.com/document/product/266/33914) 기반의 간단한 예시입니다.

```
import com.qcloud.vod.VodUploadClient;
import com.qcloud.vod.model.VodUploadRequest;
import com.qcloud.vod.model.VodUploadResponse;

import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class Main {
    public static void main(String[] args) throws Exception {
        // 동시 전송 수
        Integer threadNumber = 20;
        // 업로드할 파일의 경로 목록
        List<String> filePathList = new ArrayList<String>();

        // 업로드할 파일에 경로 추가
        filePathList.add("/data/path1.mp4");
        filePathList.add("/data/path2.mp4");
        filePathList.add("/data/path3.mp4");

        // 스레드 풀 생성
        ExecutorService pool = Executors.newFixedThreadPool(threadNumber);
        // 업로드 Client 만들기
        VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");

        // 동시 업로드
        for (String path : filePathList) {
            // 업로드 작업 제출
            pool.submit(new UploadThread(client, path));
        }
    }
}

// 스레드 업로드
class UploadThread implements Runnable {
    // Client 업로드
    private VodUploadClient uploadClient;
    // 파일 경로
    private String filePath;

    public UploadThread(VodUploadClient uploadClient, String filePath) {
        this.uploadClient = uploadClient;
        this.filePath = filePath;
    }

    public void run() {
        VodUploadRequest request = new VodUploadRequest();
        request.setMediaFilePath(filePath);
        try {
            // 업로드 실행
            VodUploadResponse response = uploadClient.upload("ap-guangzhou", request);
            System.out.println(response.getFileId());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

#### 파트 동시 업로드
파트 동시 업로드는 여러 파트에 대용량 파일을 동시에 업로드하는 데 적용할 수 있습니다. 멀티파트 업로드의 장점은 대용량 파일을 빠르게 업로드할 수 있다는 것입니다. VOD에서 제공하는 SDK는 파일 크기에 따라 자동으로 단순 업로드 또는 멀티파트 업로드를 선택하므로 멀티파트 업로드의 모든 단계를 처리할 필요가 없습니다. 파일의 동시 파트 수는 ConcurrentUploadNumber 매개변수로 지정됩니다. 특정 사용 사례의 경우 해당 SDK를 참고하십시오. 현재 이 매개변수를 지원하는 SDK는 다음과 같습니다.

- [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914#.E6.8C.87.E5.AE.9A.E5.88.86.E7.89.87.E5.B9.B6.E5.8F.91.E6.95.B0)
- [Python SDK](https://intl.cloud.tencent.com/document/product/266/33917)
- [Go SDK](https://intl.cloud.tencent.com/document/product/266/33919)

### 근거리 업로드
근거리 업로드는 업로더의 위치를 감지하여 업로더와 가장 가까운 스토리지 센터를 할당하여 파일을 업로드하는 기능을 말합니다. 예를 들어 청두의 사용자는 업로드를 위해 상하이 지역이 아닌 충칭에 할당됩니다.

근거리 업로드 기능의 가장 큰 장점은 업로더와 서버 간의 전송 거리를 단축할 수 있다는 것입니다. 이 기능에는 다음과 같은 장점이 있습니다.
- 전송 거리가 단축되고 업로드 속도가 향상됩니다.
- 안정성이 향상되고 성공률이 보장됩니다.

VOD는 기본적으로 근거리 업로드를 지원합니다. 다음 두 가지 사항만 확인하면 됩니다.

- **여러 스토리지 리전 활성화**
VOD에서 제공하는 스토리지 리전은 기본적으로 **싱가포르**입니다. 근거리 업로드 기능을 최대한 활용하려면 콘솔에서 근거리 업로드를 원하는 리전을 활성화해야 합니다. 자세한 내용은 [스토리지 설정 업로드](https://intl.cloud.tencent.com/document/product/266/18874)를 참고하십시오. 멀티 리전 스토리지가 활성화된 후 사용자가 파일을 업로드하면 VOD가 IP로 사용자의 리전을 식별하고 업로드를 위해 활성화된 리전 중 사용자와 가장 가까운 리전을 지능적으로 할당합니다.
- **스케쥴링 확인**
충칭 및 상하이의 스토리지 리전이 활성화되고 사용자가 청두에서 업로드를 시작하면 파일은 이론적으로 가까운 일정을 통해 충칭에 업로드됩니다. 일정이 합당한지 확인하려면 업로드 완료 시 반환되는 `FileId`를 가져오고 업로드된 미디어 파일의 스토리지 리전을 나타내는 `StorageRegion` 필드가 포함된 [DescribeMediaInfos API](https://intl.cloud.tencent.com/zh/document/product/266/34181)에서 반환된 기본 정보(basicInfo)와 대조합니다.

프록시 또는 포워딩을 통해 전송되어 VOD의 IP 식별 지역이 잘못된 경우, 파일 업로드를 위한 스토리지 리전을 강제로 지정할 수 있습니다. 구체적인 내용은 다음을 참고하십시오.

- [클라이언트 업로드 가이드](https://intl.cloud.tencent.com/document/product/266/33921)
- [서버 업로드 가이드](https://intl.cloud.tencent.com/document/product/266/33912)


### 사전 탐지 업로드
사전 탐지 업로드는 주로 네트워크 연결 실패, 시간 초과 및 DNS 하이재킹과 같은 네트워크 오류가 있는 다양한 유형의 시나리오를 최적화하는 수단입니다. 취약한 네트워크의 업로드에 대해 VOD에서 제공하는 효과적인 완화 솔루션입니다. 최적화 전략에는 다음 사항이 포함됩니다.
- HTTPDNS는 DNS 하이재킹을 방지하기 위해 도메인을 확인하고 백엔드 주소를 얻는 데 사용됩니다.
- 여러 지역의 연결성 및 업로드 속도를 감지하여 최적의 업로드 대상 지역을 결정합니다.
- Tencent Cloud CDN 가속 네트워크를 활용하여 안정적이고 안정적인 전송 터널을 제공합니다.

현재 클라이언트의 업로드에 사전 감지 업로드 기능이 적용되어 있으며 연결 방법이 간단합니다. 구체적인 내용은 해당 SDK의 사전 업로드 설명을 참고하십시오.

- [Android 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33925)
- [iOS 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33926)



