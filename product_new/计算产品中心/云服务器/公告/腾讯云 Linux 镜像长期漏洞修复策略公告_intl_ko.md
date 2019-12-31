Tencent Cloud의 보안 센터는 각종 보안 취약점 상황에 주의를 기울입니다. 공식 사이트에서 중요한 보안 취약점을 발표한 후 Tencent Cloud 보안 센터는 취약점 상황을 추적하여 사용자에게 취약점 정보를 전송하고 취약점 복구 솔루션을 제공합니다.

## Tencent Cloud 공식 미러 이미지 복구 주기
- 취약점 정기 복구: Tencent Cloud 공식 미러 이미지는 정기적으로 취약점을 복구하며 복구 주기는 1년에 '2'회입니다.
- 고위험 취약점 복구: 고위험 취약점에 대해 Tencent Cloud는 긴급 복구를 진행하고 가장 빠른 시간 내에 고객에게 복구 서비스를 제공합니다.

## 취약점 복구에 포함되는 미러 이미지 범위
Tencent Cloud 미러 이미지의 보안 유지 보수 원칙은 공식적인 메이저 미러 이미지 버전과 일치하며 공식적인 유지 보수 주기의 시스템 버전에 대해 보안 유지 보수를 진행합니다.
### CentOS
CentOS는 공식적으로 현재 메이저 버전에 대한 최신 마이너 버전의 유지 보수 소프트웨어 및 취약점에 대해 업데이트하며, Tencent Cloud 및 CentOS 공식적인 유지 보수 원칙과 일치합니다. 공식적인 유지 보수 주기 내에 각 메이저 버전의 최신 마이너 버전에 대해 정기적으로 취약점 복구 및 고위험 취약점 긴급 복구를 진행합니다.

Tencent Cloud 기존 CentOS 버전 미러 이미지 유지 보수 설명
- Centos 7.2 64 비트(Centos는 공식적으로 다음 마이너 버전 릴리스를 지원합니다)
- Centos 7.1 64 비트(Centos는 공식적으로 지원을 중단합니다)
- Centos 7.0 64 비트(Centos는 공식적으로 지원을 중단합니다)
- Centos 6.8 32/64비트(Centos는 공식적으로 다음 버전까지 릴리스를 지원합니다)
- Centos 6.7 32/64비트(Centos는 공식적으로 지원을 중단합니다)
- Centos 6.6 32/64비트(Centos는 공식적으로 지원을 중단합니다)
- Centos 6.5 32/64비트(Centos는 공식적으로 지원을 중단합니다)
- Centos 6.4 32/64비트(Centos는 공식적으로 지원을 중단합니다)
- Centos 6.3 32/64비트(Centos는 공식적으로 지원을 중단합니다)
- Centos 6.2 64 비트(Centos는 공식적으로 지원을 중단합니다)
- Centos 5.11 32/64비트(Centos는 공식적으로 지원합니다)
- Centos 5.8 32/64비트(Centos는 공식적으로 지원을 중단합니다)

### Ubuntu
Ubuntu는 공식적으로 LTS 버전 시스템의 장기적인 소프트웨어와 취약점에 대해 업데이트 및 유지 보수를 제공하며 각 LTS 시스템의 서버 버전은 5년 동안 업데이트가 유지됩니다. Tencent Cloud는 공식적으로 각각의 LTS 버전 서버 시스템을 제공하여 Ubuntu의 공식적인 릴리스와 일치하도록 유지 보수 주기 내의 미러 이미지에 대해 정기적으로 취약점 업데이트 및 고위험 취약점 긴급 복구를 진행합니다.

Tencent Cloud 기존 Ubuntu 버전 미러 이미지 유지 보수 설명
- Ubuntu 10.04 LTS 32/64비트(Ubuntu은 공식적으로 유지 보수를 중단하고 비활성화합니다)
- Ubuntu 12.04 LTS 64 비트(2017년 4월에 유지 보수가 중단됩니다)
- Ubuntu 14.04 LTS 32/64비트(2019년 4월에 유지 보수가 중단됩니다)
- Ubuntu 16.04 LTS 32/64비트(2021년 4월에 유지 보수가 중단됩니다)

### Debian
Debian은 공식적으로 두 가지의 주요 시스템을 유지 보수합니다. stable과 oldstable 중에서 stable은 현재 안정적인 버전이고 oldstable은 이전의 안정적인 버전입니다. Debian은 공식적으로 stable 시스템 유지 보수 소프트웨어와 취약점에 대해 업데이트하고 oldstable에 대해서는 자원 봉사자와 커뮤니티에서 장기적인 지원(LTS, Long Term Support) 의 유지 보수 솔루션을 제공합니다. Tencent Cloud와 메이저 공식 유지 보수 정책은 일치하며 Debian이 공식적으로 유지 보수하는 stable 시스템에 대해 정기적으로 취약점을 복구합니다.

Tencent Cloud 기존 Debian 버전 미러 이미지 유지 보수 설명
- Debian 8.2 32/64비트(2018년 6월 6일에 유지 보수가 중단됩니다)
- Debian 7.8 32/64비트(Debian은 공식적으로 유지 보수를 중단하였습니다)
- Debian 7.4 64 비트(Debian은 공식적으로 유지 보수를 중단하였습니다)

### openSUSE
openSUSE 시스템의 라이프사이클에 따라 Tencent Cloud는 공식적인 지원되는 시스템에 대해 정기적인 미러 이미지 취약점 복구를 진행합니다.

Tencent Cloud 기존 openSUSE 버전 미러 이미지 유지 보수 설명
- openSUSE 13.2(2017년 1분기에 유지 보수가 중단됩니다)
- openSUSE 12.3 32/64비트(openSUSE은 공식적으로 유지 보수를 중단하였습니다)

### FreeBSDㄴ
FreeBSD 11.0-RELEASE 이후, FreeBSD는 stable에 5년의 유지 보수 주기를 제공하며 11.0-RELEASE 이전 버전은 유형에 따라 다양한 유지 보수 주기가 제공됩니다. Tencent Cloud의 유지 보수 원칙은 FreeBSD의 공식적인 유지 보수 원칙과 일치합니다.

Tencent Cloud 기존 FreeBSD 버전 미러 이미지 유지 보수 설명
- 10.1-RELEASE(2016년 12월 31일에 유지 보수가 중단됩니다)

### 비즈니스 버전 시스템
Tencent Cloud는 비즈니스 버전 시스템의 취약점에 대한 업데이트 및 유지 보수를 제공하지 않으며 현재 제공하는 비즈니스 버전 미러 이미지에 포함되는 것은 다음과 같습니다.
- SUSE Linux Enterprise Server 12 64 비트
- SUSE Linux Enterprise Server 11 SP3 64 비트