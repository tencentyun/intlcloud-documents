
COSCLI는 Tencent Cloud Cloud Object Storage(COS)에서 제공하는 클라이언트 TCCLI입니다. COSCLI 툴을 사용하면 간단한 명령 라인 지침을 통해 COS의 객체(Object)에 대한 일괄 업로드, 다운로드 및 삭제 작업을 구현할 수 있습니다.

COSCLI는 Go를 사용하여 작성되었으며, Cobra 프레임워크를 기반으로 다중 버킷 설정 및 버킷 간 작업을 지원합니다. COSCLI 사용 방법은 `./coscli [command] --help`를 통해 확인할 수 있습니다.


## 기능 리스트

- [프로파일 생성 및 수정 -  config](https://intl.cloud.tencent.com/document/product/436/43251)
- [버킷 생성 - mb](https://intl.cloud.tencent.com/document/product/436/43252)
- [버킷 삭제 - rb](https://intl.cloud.tencent.com/document/product/436/43253)
- [Tagging Bucket - bucket-tagging](https://intl.cloud.tencent.com/document/product/436/46272)
- [버킷 또는 파일 리스트 쿼리 - ls](https://intl.cloud.tencent.com/document/product/436/43254)
- [다양한 유형의 파일에 대한 통계 정보 가져오기   - du](https://intl.cloud.tencent.com/document/product/436/43255)
- [파일 업/다운로드 또는 복사 - cp](https://intl.cloud.tencent.com/document/product/436/43256)
- [파일 동기화 업/다운로드 또는 복사 - sync](https://intl.cloud.tencent.com/document/product/436/43257)
- [파일 삭제 - rm](https://intl.cloud.tencent.com/document/product/436/43258)
- [파일 해시 값 가져오기 -   hash](https://intl.cloud.tencent.com/document/product/436/43259)
- [멀티파트 업로드에서 생성된 조각 파일 나열   - lsparts](https://intl.cloud.tencent.com/document/product/436/43260)
- [조각 파일 정리 -   abort](https://intl.cloud.tencent.com/document/product/436/43261)
- [아카이브 파일 검색 -   restore](https://intl.cloud.tencent.com/document/product/436/43262)
- [사전 서명된 URL 가져오기 -   signurl](https://intl.cloud.tencent.com/document/product/436/43263)






