

## 확인 사항 
- 확인 요건: 원본 데이터베이스가 Alibaba Cloud RDS인 경우 해당 테이블에는 기본 키 또는 null이 아닌 고유 키가 있어야 합니다.
- 확인 설명: RDS 테이블에 숨겨진 열이 있습니다. 잠금 없이 마이그레이션하는 동안 기본 키 또는 null이 아닌 고유 키가 없는 테이블은 데이터 불일치의 위험이 있을 수 있습니다.

## 수정 방법
페이지에 표시된 대로 기본 키 또는 null이 아닌 고유 키가 없는 테이블을 수정하고 확인 작업을 다시 실행합니다.

