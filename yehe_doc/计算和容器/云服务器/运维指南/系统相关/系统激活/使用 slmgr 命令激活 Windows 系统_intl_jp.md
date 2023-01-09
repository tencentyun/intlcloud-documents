## ユースケース
このドキュメントでは、Windows Cloud Virtual Machine (CVM)のOSを有効にする方法について説明します。



<dx-alert infotype="explain" title="">
このドキュメントは、Tencent Cloudが提供するWindows Serverパブリックイメージのみに対応し、カスタマイズイメージまたは外部からインポートされたイメージはこのドキュメントのアクティブ化方法を使用することができません。
</dx-alert>




## 操作手順
1. Windows CVMにログインします。詳細については、[標準方式を使用してWindowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/41018)をご参照ください。
2. OSのデスクトップの左下部の<img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">を右クリックし、ポップアップメニューから**Windows PowerShell（管理者）を選択します** 。
3. powershellウィンドウでは、次のコマンドを順番に実行して、OSを有効にします。
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
[](id:ProductKey)`slmgr /ipk <ProductKey>`コマンドの`<ProductKey>`を、対応するOSのバージョンに置き換えてください：
   - Windows Server 2008 R2 Enterprise Edition：`489J6-VHDMP-X63PK-3K798-CPX3Y`
   - Windows Server 2012 R2 Data Center Edition：`W3GGN-FT8W3-Y4M27-J84CP-Q3VJ9`
   - Windows Server 2016：`CB7KF-BWN84-R7R2Y-793K2-8XDDG`
   - Windows Server 2019：`WMDGN-G9PQG-XVVXX-R3X43-63DFG`
   - Windows Server 2022：`WX4NM-KYWYW-QJJR4-XV3QB-6VM33`
ProductKeyの詳細については、[キー管理サービス(KMS)クライアントの有効化とプロダクトキー](https://docs.microsoft.com/zh-cn/windows-server/get-started/kms-client-activation-keys)をご参照ください。
4. 設定を有効にするために、CVMをリスタートします。詳細については、[インスタンスのリスタート](https://intl.cloud.tencent.com/document/product/213/4928)をご参照ください。


## 関連する質問
Windows OSが有効になっていない一部のシナリオでは、ハイエンドマシンのシステムメモリは2GBに制限され、残りのメモリは「ハードウェア用に予約されたメモリ」の形式で制限されます。その理由は、`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\ProductOptions`レジストリが破損されるためです。次のコマンドを実行して、システムを再度アクティブにするかどうかを決定できます。
```
(Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Control\ProductOptions\).ProductPolicy.count
```
 - 返された結果が56184などの10000レベルの値である場合、システムを再度有効にする必要はありません。
 - 返された結果が「非有効値：1960」の場合、次の方法を参照して解決してください。
<dx-tabs>
::: 方法1
1. 次のコマンドを実行して、システムを有効にします。
```
slmgr.vbs /ipk <ProductKey>
```
<dx-alert infotype="explain" title="">
`<ProductKey>`は実際のOSのバージョンに応じて置き換えてください。詳細については、[ProductKey](#ProductKey)をご参照ください。
</dx-alert>
2. コマンドを実行した後、`(Get-ItemProperty...`コマンドを繰り返し実行して確認することができます。戻り値は56184になっています。
3. 設定を有効にするために、CVMをリスタートします。詳細については、[インスタンスのリスタート](https://intl.cloud.tencent.com/document/product/213/4928)をご参照ください。
4. 次のコマンドを実行して、システムを有効にします。
```
slmgr.vbs /ato
```

:::
::: 方法2
1. 次のコマンドを実行して、リカバーします。
```
slmgr.vbs /rilc 
```
2. コマンドを実行した後、`(Get-ItemProperty...`コマンドを繰り返し実行して確認することができます。戻り値は1960のままです。
3. 次のコマンドを実行して、システムを有効にします、Cloud Virtual Machineのリスタート。
```
slmgr.vbs /ato
```

:::
::: 方法3
1. あらゆるmsiプログラムをアンインストールします。
2. `(Get-ItemProperty...`コマンドを繰り返し実行して確認します。戻り値が変わる可能性があります。ただし、システムをリスタートした後でも、メモリ制限は2GBのままです。
2. 次のコマンドを実行して、システムを有効にします、Cloud Virtual Machineのリスタート。
```
slmgr.vbs /ato
``` 
:::
</dx-tabs>

