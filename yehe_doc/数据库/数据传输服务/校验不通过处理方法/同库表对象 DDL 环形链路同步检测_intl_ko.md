## 확인 사항 
양방향 동기화, 다대일 동기화, 멀티 사이트 활성화 등 여러 동기화 작업을 설정해야 하는 경우 DDL의 설정은 링크를 형성할 수 없습니다. 그렇지 않으면 DDL 명령이 시스템에서 순환하여 오류를 일으킬 수 있습니다.

예시: 아래 그림의 파란색 라인 1, 3, 5의 3가지 동기화 작업 중 DDL은 최대 2개의 동기화 작업에서만 선택할 수 있으며, 3개를 선택하면 원형 링크가 형성됩니다. 

<img src="https://qcloudimg.tencent-cloud.cn/raw/f1e3638e92d99b6e51b61e0980e96a83.png" style="zoom:40%;" />

## 수정 방법
**동기화 옵션 및 동기화 객체 설정** > **데이터 동기화 옵션** > **동기화 작업 유형**에서 동기화 작업 설정을 수정하여 원형 링크가 형성되지 않도록 DDL 매개변수 설정을 수정합니다.

