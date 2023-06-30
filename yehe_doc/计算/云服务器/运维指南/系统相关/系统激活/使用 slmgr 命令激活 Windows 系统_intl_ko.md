## 작업 시나리오
본 문서는 Windows CVM(Cloud Virtual Machine)의 운영 체제를 활성화하는 방법에 대해 설명합니다.



<dx-alert infotype="explain" title="">
본 문서는 Tencent Cloud에서 제공하는 Windows Server 공용 미러 이미지에만 해당됩니다. 사용자 정의 이미지 또는 외부 가져오기 이미지는 본 문서의 활성화 방법으로 사용할 수 없습니다.
</dx-alert>




## 작업 단계
1. Windows CVM에 로그인합니다. 자세한 내용은 [표준 로그인 방식으로 Windows 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/41018)을 참고하십시오.
2. 운영 체제 데스크톱의 왼쪽 하단 모서리를 우클릭하고 <img src="https://qcloudimg.tencent-cloud.cn/raw/10c0728e4d194732be4eb6c1a95e0a8c.png" style="margin: -5px 0px;"/> 팝업 메뉴에서 **Windows PowerShell(관리자)** 을 선택합니다.
3. powershell 창에서 다음 명령을 차례로 실행하여 운영 체제를 활성화합니다.
```
slmgr /upk
```
```
slmgr /ipk <ProductKey>
```
```
slmgr /skms kms.tencentyun.com
```
```
slmgr /ato
```
[](id:ProductKey)`slmgr /ipk <ProductKey>` 명령의 `<ProductKey>` 해당 운영 체제 버전을 교체하십시오.
   - Windows Server 2008 R2 엔터프라이즈 버전: `489J6-VHDMP-X63PK-3K798-CPX3Y`
   - Windows Server 2012 R2 데이터센터 버전: `W3GGN-FT8W3-Y4M27-J84CP-Q3VJ9`
   - Windows Server 2016: `CB7KF-BWN84-R7R2Y-793K2-8XDDG`
   - Windows Server 2019: `WMDGN-G9PQG-XVVXX-R3X43-63DFG`
   - Windows Server 2022: `WX4NM-KYWYW-QJJR4-XV3QB-6VM33`
ProductKey에 대한 자세한 내용은 [키 관리 서비스(KMS) 클라이언트 활성화 및 제품 키](https://docs.microsoft.com/zh-cn/windows-server/get-started/kms-client-activation-keys)를 참고하십시오.
4. 설정을 적용하려면 CVM을 재시작합니다. 자세한 내용은 [인스턴스 재시작](https://intl.cloud.tencent.com/document/product/213/4928)을 참고하십시오.


## FAQ
Windows 운영 체제가 활성화되지 않은 일부 시나리오에서 고급형 시스템의 시스템 메모리는 2GB로 제한되고 나머지 메모리는 ‘하드웨어용으로 보관된 메모리’ 형태로 제한됩니다. 그 이유는 `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\ProductOptions` 레지스트리가 손상되었기 때문입니다. 다음 명령을 실행하여 시스템 재활성화 여부를 결정할 수 있습니다.
```
(Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Control\ProductOptions\).ProductPolicy.count
```
 - 반환된 결과가 56184와 같이 만 단위 값이면 시스템을 다시 활성화할 필요가 없습니다.
 - 반환된 결과가 ‘비활성 값: 1960’인 경우 다음 방법을 참고하여 해결하시기 바랍니다.
<dx-tabs>
::: 방법1
1. 다음 명령을 실행하여 시스템을 활성화합니다.
```
slmgr.vbs /ipk <ProductKey>
```
<dx-alert infotype="explain" title="">
`<ProductKey>` 실제 운영 체제 버전에 따라 교체하십시오. 자세한 내용은 [ProductKey](#ProductKey)를 참고하십시오.
</dx-alert>
2. 명령이 실행된 후 `(Get-ItemProperty...` 명령 인증을 반복적으로 실행하여 인증할 수 있습니다. 반환 값이 56184가 됩니다.
3. 설정을 적용하려면 CVM을 재시작합니다. 자세한 내용은 [인스턴스 재시작](https://intl.cloud.tencent.com/document/product/213/4928)을 참고하십시오.
4. 다음 명령을 실행하여 시스템을 활성화합니다.
```
slmgr.vbs /ato
```

:::
::: 방법2
1. 다음 명령을 실행하여 복구합니다.
```
slmgr.vbs /rilc 
```
2. 명령이 실행된 후 `(Get-ItemProperty...` 명령을 반복적으로 실행하여 인증할 수 있으며 반환 값은 여전히 ​​1960입니다.
3. 다음 명령을 실행하여 시스템을 활성화합니다.Cloud Virtual Machine 재시작.
```
slmgr.vbs /ato
```

:::
::: 방법3
1. 모든 msi 프로그램을 언마운트합니다.
2. `(Get-ItemProperty...` 명령을 반복적으로 실행하여 인증하면 반환 값이 변경될 수 있습니다. 그러나 시스템을 다시 시작한 후에도 메모리 제한은 여전히 ​​2GB입니다.
2. 다음 명령을 실행하여 시스템을 활성화합니다.Cloud Virtual Machine 재시작.
```
slmgr.vbs /ato
``` 
:::
</dx-tabs>

