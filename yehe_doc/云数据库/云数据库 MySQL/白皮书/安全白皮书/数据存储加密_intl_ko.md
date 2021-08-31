
TencentDB for MySQL은 [투명한 데이터 암호화 기능](https://intl.cloud.tencent.com/document/product/236/38491)을 지원하며, 해당 기능은 Tencent Cloud 데이터베이스 팀이 자체 개발했습니다. 투명한 암호화란 데이터의 암호화 및 복호화 조작이 사용자에게 투명하다는 의미입니다. 사용자가 암호화 테이블을 생성할 때, 암호화키를 지정할 필요가 없으며 데이터는 디스크 쓰기 시 암호화되고, 디스크 읽기 시 복호화 됩니다.

TDE는 국제적으로 통용되는 AES 알고리즘을 적용하며 키 길이는 256비트입니다. 암호화 키는 Tencent Cloud [Key Management Service (KMS)](https://intl.cloud.tencent.com/document/product/1030/31961)가 관리합니다. KMS 서비스에 액세스하려면 사용자 라이선스를 취득해야 하며, KMS 콘솔을 통한 키 변경으로 시스템 보안성을 한층 향상시킬 수 있습니다. 

