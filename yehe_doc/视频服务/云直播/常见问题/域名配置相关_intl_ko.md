<span id="que1"></span>
LVB에 도메인을 추가하는 방법은 어떻게 됩니까?

1. Tencent Cloud [라이브 방송 콘솔](https://console.cloud.tencent.com/live)에 로그인하여 [Domain Management] 페이지에 접속합니다.
2. 자체 푸시 스트리밍 도메인 또는 재생 도메인을 추가합니다. 구체적인 사항은 [도메인 관리](https://intl.cloud.tencent.com/document/product/267/35970)를 참조하십시오.
3. 도메인 추가 후 CNAME 설정을 완료합니다. 구체적인 사항은 [CNAME 설정](https://intl.cloud.tencent.com/document/product/267/31057)을 참조하십시오.
4. 설정 성공 후 자체 도메인을 사용하여 푸시 스트리밍 및 재생을 진행할 수 있습니다.

<span id="que2"></span>
### CNAME 설정 완료 후에도 CNAME이 미설정으로 표시되는 이유는 무엇입니까?

문서 [도메인 CNAME 설정](https://intl.cloud.tencent.com/document/product/267/31057) 가이드에 따라 CNAME 설정을 완료한 경우, CNAME 설정 적용까지 15분~30분이 걸리니 조금만 기다려 주십시오. 자체적으로 CANME 성공 여부를 확인할 수도 있습니다. 구체적인 인증 방법은 [CNAME 적용 여부 인증](https://intl.cloud.tencent.com/document/product/267/31057)을 참조하십시오.
>
> - Linux/Mac/Windows 시스템은 공용 네트워크 DNS를 통해 리졸브해야 합니다.
> - CNAME 조작 후 점검에 실패할 경우 도메인 등록 서비스 제공 업체에 문의하십시오.

<span id="que3"></span>
### 자체 도메인에 액세스하지 않으면 어떻게 됩니까?
2018년 10월 17일 이후에 LVB 서비스를 개통한 경우 자체 도메인을 추가해야 재생이 가능하며 추가하지 않을 경우 라이브 방송 콘텐츠를 재생할 수 없습니다.

위의 날짜 이전에 LVB 서비스를 개통한 경우 기본 도메인이 제공됩니다. Tencent Cloud는 2018년 12월 31일부터 점진적으로 기본 도메인 사용을 중단하고 있으니 신속히 자체 도메인으로 교체하실 것을 권장합니다.

> 기본 도메인은 LVB에서 분배한 시스템 도메인입니다. 포맷은 `bizid.livepush.myqcloud.com` 및 `bizid.liveplay.myqcloud.com`입니다.

<span id="que4"></span>
### 기본 도메인으로 특수 설정을 진행한 경우 자체 도메인을 기존의 기본 도메인에 리졸브할 수 있습니까?
신규 도메인 액세스 시 라이브 방송 액세스를 권장하며, 라이브 방송 콘솔을 통해 자체 도메인을 추가하여 각종 설정을 진행할 수 있습니다.

