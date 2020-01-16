### SSH 키 로그인 및 비밀번호 로그인의 차이점은 무엇입니까?
SSH 키는 일종 원격으로 Linux 서버에 로그인하는 방식으로 키 생성기를 사용하여 한 쌍의 키(공개키와 개인키)를 만드는 원리입니다. 공개키를 서버에 추가한 후 클라이언트에서 개인키를 이용하여 인증 및 로그인을 완료합니다. 이런 방식은 데이터의 안정성을 더욱 중요시하는 한편 전통적인 비밀번호 로그인 방식의 수동 입력과 구별하여 편리성을 높여 줍니다.
현재 Linux 인스턴스는 비밀번호가 있고 SSH 키는 두 가지 로그인 방식이 있으며 Windows 인스턴스는 현재 비밀번호 로그인 방식만 사용합니다. 관련 문서를 참조하십시오.
- [Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/5436)
- [Windows 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32498)

### SSH 키 로그인 방식을 사용하는 동시에 비밀번호 로그인 방식을 사용할 수 있습니까?
사용자가 [SSH 키를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)하면 기본적으로 비밀번호 로그인을 금지하므로 보안성을 향상시킬 수 있습니다. 키 로그인 후 사용자는 다시는 비밀번호 로그인 방식을 사용할 수 없습니다.

### 비밀번호를 잊으면 어떻게 해야 하나요?
비밀번호를 재설정할 수 있습니다. 작업에 대한 자세한 내용은 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참조하십시오.

### SSH 키 생성 및 키 분실하면 어떻게 해야 합니까?
키 생성 관련 문제에 대한 자세한 내용은 [SSH 키 생성](https://intl.cloud.tencent.com/document/product/213/16691)을 참조하고 생성을 완료하십시오.
키 분실 시 다음 두 가지 해결 방법을 제공합니다.
 - CVM의 [SSH 키 콘솔](https://console.cloud.tencent.com/cvm/sshkey)을 통해 새 키를 생성하고 새 키를 기존 인스턴스에 바인딩합니다.
  1. [SSH 키 생성](https://intl.cloud.tencent.com/document/product/213/16691)
  2. 키 생성 완료 후 [CVM 인스턴스 콘솔](https://console.cloud.tencent.com/cvm)에 진입합니다.
  3. 바인딩할 키의 기존 인스턴스를 선택하고 [MORE]>[비밀번호/키]>[키 추가]를 클릭하면 새 키를 사용하여 인스턴스에 로그인할 수 있습니다.
 - CVM 콘솔을 통해 비밀번호를 재설정하고 새 비밀번호를 사용하여 인스턴스에 로그인합니다. 작업에 대한 자세한 내용은 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참조하십시오.

### SSH 키로 서버를 어떻게 바인딩/바인딩 해제합니까?

[SSH 키 작업 가이드](https://intl.cloud.tencent.com/document/product/213/16691)에서 **키로 서버 바인딩/바인딩 해제**부분을 참조하십시오.

### SSH 키 이름/설명을 어떻게 수정합니까?

[SSH 키 작업 가이드](https://intl.cloud.tencent.com/document/product/213/16691)에서 **SSH 키 이름/설명 수정**부분을 참조하십시오.

### SSH 키를 어떻게 삭제합니까?

[SSH 키 작업 가이드](https://intl.cloud.tencent.com/document/product/213/16691)의 **SSH 키 삭제**부분을 참조하십시오.

### SSH 키는 이용 제한은 무엇입니까?

[SSH 키 소개](https://intl.cloud.tencent.com/document/product/213/6092)에서 **이용 제한**부분을 참조하십시오.

### SSH 키로 Linux 인스턴스에 로그인할 수 없는 경우 어떻게 조사합니까?

[SSH 방식으로 Linux 인스턴스에 로그인할 수 없는 경우](https://cloud.tencent.com/document/product/213/37925)를 참조하십시오.
