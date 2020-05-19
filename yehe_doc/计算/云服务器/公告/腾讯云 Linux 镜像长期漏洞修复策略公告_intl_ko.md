Tencent Cloud 보안 센터는 각종 보안 취약점에 즉각 대응합니다. 공식 홈페이지에서 중요 보안 취약점을 배포하면, Tencent Cloud 보안 센터가 취약점을 즉시 추적하여 사용자에게 취약점 정보를 전송하고 취약점 복구 솔루션을 제공합니다.

## Tencent Cloud의 공식 이미지 복구 주기
- 취약점 정기 복구: Tencent Cloud의 공식 이미지는 취약점 정기 복구를 매년 2회씩 진행합니다.
- 고위험 취약점 복구: Tencent Cloud는 고위험 취약점에 대해 긴급 복구를 진행하며 고객에게 신속한 서비스를 제공합니다.

## 취약점 복구에 포함되는 이미지 범위
이미지의 보안에 있어 Tencent Cloud와 업스트림 이미지 공식 릴리스 버전의 점검 원칙이 일치하므로, 공식 점검 주기에 해당하는 시스템 버전의 보안 점검을 진행합니다.

### CentOS
CentOS 공식 홈페이지는 현재 배포된 메이저 버전의 최신 마이너 버전 점검 소프트웨어 및 취약점만 업데이트하며, Tencent Cloud와 CentOS 공식 홈페이지의 점검 원칙이 일치합니다. 따라서 공식 점검 주기에 해당하는 각 메이저 버전의 최신 마이너 버전에 대해 정기적인 취약점 복구 및 고위험 취약점 긴급 복구를 진행합니다.

Tencent Cloud의 기존 CentOS 버전 이미지 점검 설명:
- CentOS 7.6 64비트 (CentOS 공식 홈페이지에서 지원 유지)
- CentOS 7.5 64비트 (CentOS 공식 홈페이지에서 지원 유지)
- CentOS 7.4 64비트 (CentOS 공식 홈페이지에서 지원 유지)
- CentOS 7.3 64비트 (CentOS 공식 홈페이지에서 지원 유지)
- CentOS 7.2 64비트 (CentOS 공식 홈페이지에서 지원 유지)
- CentOS 7.1 64비트 (CentOS 공식 홈페이지에서 지원 중단)
- CentOS 7.0 64비트 (CentOS 공식 홈페이지에서 지원 중단)
- CentOS 6.9 32/64비트 (CentOS 공식 홈페이지에서 다음 버전 배포까지 지원합니다)
- CentOS 6.8 32/64비트 (CentOS 공식 홈페이지에서 지원 중단)
- CentOS 6.7 32/64비트 (CentOS 공식 홈페이지에서 지원 중단)
- CentOS 6.6 32/64비트 (CentOS 공식 홈페이지에서 지원 중단)
- CentOS 6.5 32/64비트 (CentOS 공식 홈페이지에서 지원 중단)
- CentOS 6.4 32/64비트 (CentOS 공식 홈페이지에서 지원 중단)
- CentOS 6.3 32/64비트 (CentOS 공식 홈페이지에서 지원 중단)
- CentOS 6.2 64비트 (CentOS 공식 홈페이지에서 지원 중단)
- CentOS 5.11 32/64비트 (CentOS 공식 홈페이지에서 지원 중단)
- CentOS 5.8 32/64비트 (CentOS 공식 홈페이지에서 지원 중단)

### Ubuntu
Ubuntu 공식 홈페이지는 LTS 버전 시스템의 소프트웨어와 취약점을 장기적으로 업데이트 및 점검하며, 각 LTS 시스템의 서버 버전의 경우 5년 동안 업데이트가 유지됩니다. Tencent Cloud 운영사는 각 LTS 버전의 서버 시스템을 제공하며, Ubuntu의 공식 배포와 일치하므로 점검 주기에 해당하는 이미지의 취약점 업데이트 및 고위험 취약점 긴급 복구를 진행합니다.

Tencent Cloud의 기존 Ubuntu 버전 이미지 점검 설명:
- Ubuntu 18.04 LTS 64비트 (Ubuntu 공식 홈페이지에서 점검 지원)
- Ubuntu 16.04 LTS 64비트 (Ubuntu 공식 홈페이지에서 점검 지원)
- Ubuntu 14.04 LTS 32/64비트 (Ubuntu 공식 홈페이지에서 점검 지원)
- Ubuntu 12.04 LTS 64비트 (Ubuntu 공식 홈페이지에서 점검 중단)
- Ubuntu 10.04 LTS 32/64비트 (Ubuntu 공식 홈페이지에서 점검 중단)




### Debian
Debian 공식 홈페이지는 stable과 oldstable 두 가지의 주요 branch 시스템을 점검합니다. stable은 현재의 안정 버전이고 oldstable은 옛 안정 버전입니다. Debian 공식 홈페이지는 stable 시스템의 소프트웨어 점검과 취약점 업데이트를 진행하고, oldstable은 자원 봉사 및 커뮤니티에서 제공하는 장기 지원(Long Term Support, LTS)로 점검합니다. Tencent Cloud와 업스트림 공식 점검 정책이 일치하므로 Debian 공식 홈페이지에서 점검하는 stable branch 시스템의 취약점을 정기적으로 복구합니다.

Tencent Cloud의 기존 Debian 버전 이미지 점검 설명:
- Debian 9.0  64비트 (Debian 공식 홈페이지에서 점검 지원)
- Debian 8.2 32/64비트 (2019년 6월 점검 중단 예정)
- Debian 7.8 32/64비트 (Debian 공식 홈페이지에서 점검 중단함)
- Debian 7.4 64비트 (Debian 공식 홈페이지에서 점검 중단함)


### openSUSE
Tencent Cloud는 openSUSE 시스템의 라이프사이클에 따라, 공식 홈페이지에서 지원하는 시스템의 이미지 취약점을 정기적으로 복구합니다.

Tencent Cloud의 기존 openSUSE 버전 이미지 점검 설명:
- openSUSE 42.3 openSUSE 공식 홈페이지에서 점검 지원)
- openSUSE 13.2 openSUSE 공식 홈페이지에서 점검 중단함)
- openSUSE 12.3 32/64位 openSUSE 공식 홈페이지에서 점검 중단함)

### FreeBSD
FreeBSD 11.0-RELEASE 이후, FreeBSD는 stable branch에 5년의 점검 주기를 제공하며, 11.0-RELEASE 이전 버전은 유형에 따라 점검 주기가 제공됩니다. 또한, Tencent Cloud와 FreeBSD 와 공식 홈페이지의 점검 원칙이 일치합니다.

Tencent Cloud의 기존 FreeBSD 버전 이미지 점검 설명:
- FreeBSD 11.1 64비트 (FreeBSD 공식 홈페이지에서 점검 지원)
- FreeBSD 10.1 64비트 (FreeBSD 공식 홈페이지에서 점검 중단함)

### 비즈니스 버전 시스템
Tencent Cloud는 비즈니스 버전 시스템의 취약점 업데이트 및 점검을 지원하지 않습니다.
