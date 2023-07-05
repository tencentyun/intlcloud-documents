### SSH 키 로그인과 비밀번호 로그인의 차이점은 무엇인가요?
SSH 키는 Linux 서버에서 사용하는 일종의 원격 로그인 방식입니다. 키 생성기를 사용하여 하나의 키 쌍(공개키와 프라이빗 키)을 만들어 공개키를 서버에 추가한 후, 클라이언트의 프라이빗 키를 이용하여 인증 및 로그인하는 원리입니다. 이러한 방식은 데이터 보안성이 더 높을 뿐 아니라, 전통적인 비밀번호 로그인 방식의 수동 입력과 비교하여 편리함까지 갖추고 있습니다.
현재 Linux 인스턴스는 비밀번호와 SSH 키의 두 가지 로그인 방식이 있으며, Windows 인스턴스는 비밀번호 로그인 방식만 사용합니다. 관련 내용은 다음의 문서를 참조 바랍니다.
- [Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/5436)
- [Windows 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/5435)

### Linux 인스턴스에 SSH 키를 연결한 후 사용자 이름/비밀번호로는 왜 로그인할 수 없나요?
CVM에 SSH 키를 연결하면 사용자 이름/비밀번호 로그인은 **기본적으로 비활성화되므로** [SSH 키를 사용하여 CVM에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)하시기 바랍니다. 

### SSH 키 로그인과 비밀번호 로그인을 동시에 사용할 수 있나요?
사용자가 [SSH 키를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)할 경우, 보안성 향상을 위해 비밀번호 로그인은 비활성화되도록 기본 설정되어 있습니다. 따라서 한 번 SSH 키로 로그인한 사용자는 더는 비밀번호 로그인을 사용할 수 없게 됩니다.

### 생성한 SSH 키를 분실했을 경우 어떻게 해야 하나요?
키 생성 문제에 관한 내용은 [SSH 키 생성](https://intl.cloud.tencent.com/document/product/213/16691)을 참조하여 생성하시기 바랍니다.
키를 분실했을 경우 다음 두 가지 해결 방법으로 해결하실 수 있습니다.
 - CVM의 [SSH 키 콘솔](https://console.cloud.tencent.com/cvm/sshkey)을 통해 신규 키를 생성하고 해당 키를 기존 인스턴스에 바인딩합니다.
  1. [SSH 키 생성](https://intl.cloud.tencent.com/document/product/213/16691)
  2. 키 생성 완료 후 [CVM 인스턴스 콘솔](https://console.cloud.tencent.com/cvm)에 들어갑니다.
  3. 키를 바인딩할 기존 인스턴스를 선택하고 [더 보기]>[비밀번호/보안키]>[키 업로드]를 클릭하면 신규 키를 사용하여 인스턴스에 로그인할 수 있습니다.
 - CVM 콘솔을 통해 비밀번호를 재설정하고 새 비밀번호를 사용하여 인스턴스에 로그인합니다. 자세한 작업 방식은 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참조 바랍니다.

### 서버와 SSH 키의 바인딩/바인딩 해제는 어떻게 하나요?

자세한 작업 방식은 [서버에 SSH 키 바인딩/바인딩 해제](https://intl.cloud.tencent.com/document/product/213/16691)를 참조 바랍니다.

### SSH 키의 이름/설명은 어떻게 수정하나요?

자세한 작업 방식은 [SSH 키 이름/설명 수정](https://intl.cloud.tencent.com/document/product/213/16691)을 참조 바랍니다.

### SSH 키는 어떻게 삭제하나요?

자세한 작업 방식은 [SSH 키 삭제](https://intl.cloud.tencent.com/document/product/213/16691)를 참조 바랍니다.

### SSH 키의 사용 제한은 무엇인가요?

[SSH 키 사용 제한](https://intl.cloud.tencent.com/document/product/213/6092)을 참조 바랍니다.

### SSH 키로 Linux 인스턴스에 로그인할 수 없습니다. 어떻게 해결하나요?

자세한 작업 방식은 [SSH 방식으로 Linux 인스턴스에 로그인할 수 없을 경우](https://intl.cloud.tencent.com/document/product/213/32486)를 참조 바랍니다.

### 키를 다운로드할 수 없는 이유는 무엇인가요?
키는 단 1회만 다운로드할 수 있습니다. 키를 분실했다면 신규 키를 생성한 후 다시 다운로드 받으시길 권장합니다.

### CVM 인스턴스가 어떤 키를 사용했는지 어디서 확인할 수 있나요?
CVM 콘솔에 로그인한 후, CVM 인스턴스의 상세 정보 페이지에서 사용한 키의 정보를 확인할 수 있습니다.
