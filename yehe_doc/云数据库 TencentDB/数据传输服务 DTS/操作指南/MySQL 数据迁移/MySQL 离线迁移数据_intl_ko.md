본 문서는 콘솔 및 TCCLI를 통한 두 가지 데이터 마이그레이션 방법에 대해 소개합니다.

## 콘솔로 데이터 마이그레이션
콘솔을 통해 데이터를 물리적 백업 혹은 로직 백업하여 마이그레이션할 수 있으며, 자세한 작업은 다음을 참조하십시오.
- [물리 백업을 사용하여 데이터베이스 복구](https://intl.cloud.tencent.com/document/product/236/31910)
- [로직 백업으로 데이터베이스 복구](https://intl.cloud.tencent.com/document/product/236/31909)

<span id="AA"></span>
## TCCLI로 데이터 마이그레이션
1. 다음과 같이 MySQL의 TCCLI인 mysqldump로 가져올 SQL 파일을 생성합니다.
>!
>- mysqldump로 내보낸 데이터 파일은 구매한 TencentDB for MySQL 버전의 SQL 규격과 호환되어야 하며, CDB에 로그인한 뒤 `select version();`을 통해 MySQL 버전 정보를 확인할 수 있습니다. 생성한 SQL 파일 이름은 영어/숫자/언더바로 구성되어야 하며, 'test'란 단어는 포함할 수 없습니다.
>- 원본 데이터베이스와 타깃 데이터베이스의 버전 및 문자 세트, mysqldump 툴의 버전이 일치해야 합니다. ```--default-character-set```와 같은 매개변수를 통해 문자 세트를 지정할 수 있습니다.
>
```
shell > mysqldump [options] db_name [tbl_name ...] > bak_pathname
```
options은 내보내기 옵션, db_name은 데이터베이스 이름, tbl_name은 테이블 명칭, bak_pathname은 내보내기 경로를 각각 나타냅니다.
mysqldump로 데이터 내보내기에 관한 자세한 설명은 [MySQL 공식 매뉴얼](https://dev.mysql.com/doc/refman/5.6/en/mysqldump.html)을 참조하십시오.
2. 다음의 방식처럼, MySQL의 TCCLI를 통해 타깃 데이터베이스로 데이터를 가져옵니다.
```
shell > mysql -h hostname -P port -u username -p < bak_pathname
```
그중, hostname은 데이터를 복원할 타깃 CVM, port는 타깃 CVM의 포트, username은 타깃 CVM 데이터베이스의 사용자 이름, bak_pathname은 백업 파일의 전체 경로를 각각 나타냅니다.

### 데이터 마이그레이션(Windows 시스템)
1. Windows 시스템의 mysqldump 툴로 가져올 SQL 파일을 생성합니다. 자세한 내용은 [TCCLI로 데이터 마이그레이션](#AA)의 설명을 참조하십시오.
2. 명령 프롬프트에서 MySQL TCCLI를 통해 타깃 데이터베이스로 데이터를 가져옵니다.
![](https://main.qcloudimg.com/raw/82fece0fed5c61437215836a6a5fdc54.png)
3. [타깃 MySQL 데이터베이스에 로그인](https://dev.mysql.com/doc/refman/5.7/en/connecting.html)하여 `show databases;` 명령어를 실행하면 타깃 데이터베이스로 가져온 백업 데이터베이스를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/ac73c7b6cd2dd6682dffce3cb696a3dd.png)

### 데이터 마이그레이션(Linux 시스템)
본 문서는 Linux 시스템의 CVM을 예로 들고 있습니다. CVM에서 데이터베이스에 액세스하려면 <a href="https://intl.cloud.tencent.com/document/product/236/37788" target="_blank">MySQL 데이터베이스 액세스</a>를 참조하십시오.  

1. [CVM에 로그인](https://intl.cloud.tencent.com/zh/document/product/213/10517)한 뒤, MySQL TCCLI인 mysqldump로 가져올 SQL 파일을 생성합니다. CDB의 db_blog 데이터베이스를 예시로 사용합니다.
![](https://main.qcloudimg.com/raw/53d9cb3eace605f1f6a470f44a3d4b99.png)
2. MySQL TCCLI를 통해 타깃 데이터베이스로 데이터를 복원합니다.
3. 타깃 MySQL 데이터베이스에 로그인하여 `show databases;` 명령어를 실행하면 타깃 데이터베이스로 가져온 백업 데이터베이스를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/814943da5e7ee28312a3c15e6c431b73.png)

## 가져온 데이터 파일 문자 세트의 인코딩 문제
1. CDB에 가져온 데이터 파일에 지정된 문자 세트 인코딩이 없다면, CDB에 설정된 문자 세트로 인코딩이 실행됩니다.
2. 가져온 데이터 파일에 지정된 문자 세트 인코딩이 있다면, 지정된 문자 세트로 인코딩이 실행됩니다.
3. 가져온 데이터 파일의 문자 세트 인코딩과 CDB의 문자 세트 인코딩이 다를 경우 에러 코드가 나타날 수 있습니다.

문자 세트 인코딩 문제에 관한 더 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/236/7259" target="_blank">사용 제한</a>의 문자 세트 설명을 참조하십시오.


