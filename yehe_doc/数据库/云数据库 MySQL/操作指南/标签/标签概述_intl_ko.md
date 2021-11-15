### 소개

**태그**는 Tencent Cloud가 클라우드 상의 리소스 식별을 위해 제공하는 표기로, 키-값 쌍(Key-Value)을 뜻합니다. 자세한 사항은 [태그 개요](http://intl.cloud.tencent.com/document/product/651/13334)를 참조 바랍니다.
태그를 사용하여 다양한 각도(예: 비즈니스, 용도, 담당자 등)에서 TencentDB for MySQL 리소스를 분류 및 관리할 수 있습니다. 태그를 통해 해당하는 리소스를 손쉽게 필터링할 수 있습니다. 태그 키 값 쌍은 Tencent Cloud에 어떠한 semantic meaning도 가지지 않으며 문자열에 따라 엄격하게 리졸브 매칭이 이루어집니다. 따라서 사용 중에는 [사용 제한](http://intl.cloud.tencent.com/document/product/651/13354)에만 유의하시면 됩니다.
구체적인 사례를 통해 태그 사용법에 대해 소개하겠습니다.

### 사례 배경
모 회사는 Tencent Cloud에 총 10대의 TencentDB for MySQL를 보유하고 있습니다. 전자상거래, 게임, 문화 엔터테인먼트 3개 부서에 걸쳐 마케팅 이벤트와 게임 A, 게임 B, 후반 작업 등의 업무를 수행하고 있으며, 홍길동, 심청이, 왕 씨가 각 부서의 유지보수 담당자로 활동하고 있습니다.

### 태그 설정
이 회사는 용이한 관리를 위해 TencentDB for MySQL 리소스를 분류 및 관리하는 태그를 사용하여 다음 태그 키/값을 정의했습니다.

| 태그 키     | 태그 값                             |
| :---------- | ---------------------------------- |
| 부서       | 전자상거래, 게임, 문화 엔터테인먼트                   |
| 업무       | 마케팅 이벤트, 게임 A, 게임 B, 후반 작업 |
| 유지보수 담당자 | 홍길동, 심청이, 왕 씨                   |

이 태그 키/값들은 TencentDB for MySQL에 바인딩되어 있습니다. 리소스와 태그 키/값의 관계는 다음 표와 같습니다.

|instance-id	|부서	|업무	|유지보수 담당자|
|----------------|-------|----|--------------|
|cdb-abcdef1	|전자상거래	|마케팅 이벤트	|왕 씨|
|cdb-abcdef2	|전자상거래	|마케팅 이벤트	|왕 씨|
|cdb-abcdef3	|게임|	게임 A	|홍길동|
|cdb-abcdef3	|게임|	게임 B	|홍길동|
|cdb-abcdef4|	게임	|게임 B	|홍길동|
|cdb-abcdef5|	게임	|게임 B	|심청이|
|cdb-abcdef6	|게임	|게임 B|	심청이|
|cdb-abcdef7	|게임	|게임 B	|심청이|
|cdb-abcdef8	|문화 엔터테인먼트	|후반 작업|	왕 씨|
|cdb-abcdef9	|문화 엔터테인먼트	|후반 작업	|왕 씨|
|cdb-abcdef10	|문화 엔터테인먼트	|후반 작업	|왕 씨|

### 태그 사용
태그 생성과 삭제 방법은 [운영 가이드](https://intl.cloud.tencent.com/document/product/651/41684)를 참조 바랍니다.

TencentDB for MySQL 태그 편집 방법은 [태그 편집](https://intl.cloud.tencent.com/document/product/236/31918)을 참조 바랍니다.

