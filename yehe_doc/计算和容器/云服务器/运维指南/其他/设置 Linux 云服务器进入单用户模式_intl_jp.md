## 操作シナリオ
Linuxユーザーは一部のケースで、単一ユーザーモードで特殊な操作またはメンテナンス関連の操作を実行する必要があります。例えば、パスワード管理の実行、sshd破損の修復またはディスクマウント前にメンテナンス作業を実行する必要がある場合などです。このドキュメントでは主要なLinuxオペレーティングシステムで単一ユーザーモードの操作に進む手順について説明します。

## 操作手順
1. CVMコンソールから、VNCを使用してCVMにログインします。詳細については、[VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)をご参照ください。
2. VNCのログインインターフェースで、左上隅の**リモートコマンドの送信**>**Ctrl-Alt-Delete**を選択して、ポップアップウィンドウで**OK**をクリックします。
3. リンク失敗のメッセージが表示される時は、直ちにページをリフレッシュして上下キー（↑↓）を押し、システムがgrubメニューで止まるようにします。下図に示すとおりです。
![](https://main.qcloudimg.com/raw/350187ce0a771d00e6d54e929291ebae.png)
4. **e**を押してgrubモードに入ります。
5. grubモードに入ってから、実際に使用するOSタイプに基づいて、以下のように異なる操作手順を選択する必要があります。
<dx-tabs>
::: CentOS\s6.x
1. grubモードのインターフェースで、下図のようにカーネルを選択します。
![](https://main.qcloudimg.com/raw/5abc9f57184cc74bba927513fb1c4a88.png)
2. **e**を押してカーネル編集インターフェースに入り、↑↓キーを使用して**kernel**のある行を選択し、再び**e**を押します。下図のようになります。
![](https://main.qcloudimg.com/raw/1a596a48df87d1d619e415d8d5b0cb65.png)
3. 行末に**single**を入力します。下図のとおりです。
![](https://main.qcloudimg.com/raw/e1f74a4ce211a34301c4f74ffcc790b8.png)
4. **Enter**を押して入力を確認してから、**b**を押して現在選択中の起動コマンドラインを開始すると、単一ユーザーモードに入ることができます。下図のとおりです。
![](https://main.qcloudimg.com/raw/b379937bfc15e93f0823ec50095d1dc6.png)
下図のように表示されれば、単一ユーザーモードが開始されています。
![](https://main.qcloudimg.com/raw/517c4d2c24864f3fc8f5002bd1e2c2a1.png)
<dx-alert infotype="explain" title="">
`exec /sbin/init`コマンドを実行して、単一ユーザーモードを終了することができます。
</dx-alert>
:::
::: CentOS\s7.x
1. grubモードのインターフェースで、下図のようにカーネルを選択します。
![](https://main.qcloudimg.com/raw/2ddc7d1e4416d9fa763922e23b59d580.png)
2. **e**を押してカーネル編集インターフェースに入り、↑↓キーを使用してlinux16開始行まで移動し、`ro`を`rw init=/bin/bash`または`/usr/bin/bash`に変更します。下図のとおりです。
![](https://main.qcloudimg.com/raw/1b861ba0ecee1cd82da4364523e8a1c6.png)
3. **Ctrl+X**を押し、単一ユーザーモードを起動して入ります。
下図のように表示されれば、単一ユーザーモードが開始されています。
![](https://main.qcloudimg.com/raw/fbe8cfcf43aa4c914882edc4c3ee5faf.png)
<dx-alert infotype="explain" title="">
`exec /sbin/init`コマンドを実行して、単一ユーザーモードを終了することができます。
</dx-alert>
:::
::: CentOS\s8.0
1. grubモードのインターフェースで、下図のようにカーネルを選択します。
![](https://main.qcloudimg.com/raw/a6ce701e5845141929d822635bd42b9a.png)
2. **e**を押してカーネル編集インターフェースに入り、↑↓キーを使用してlinux開始行まで移動し、`ro`を`w init=/sysroot/bin/bash`に変更します。下図のとおりです。
![](https://main.qcloudimg.com/raw/d06effc3cab12d545fd7bc92f4577b14.png)
3. **Ctrl+X**を押し、単一ユーザーモードを起動して入ります。
下図のように表示されれば、単一ユーザーモードが開始されています。
![](https://main.qcloudimg.com/raw/126dcdb5916e57815c3632e9e4b24412.png)
:::
::: Ubuntu\sまたは\sDebian
1. grubモードのインターフェースで、下図のようにカーネルを選択します。
![](https://main.qcloudimg.com/raw/c3c0be766481edf3f6521f7764f8d4cb.png)
2. **e**を押してカーネル編集インターフェースに入り、↑↓キーを使用してlinux開始行まで移動し、行末に`quiet splash rw init=/bin/bash`を追加します。下図のとおりです。
![](https://main.qcloudimg.com/raw/40882cf22d755c0338ea9d7c106bc280.png)
3. **Ctrl+X**を押し、単一ユーザーモードを起動して入ります。
下図のように表示されれば、単一ユーザーモードが開始されています。
![](https://main.qcloudimg.com/raw/df55d20b7eb087744fb6283c5124e7fc.png)
:::
::: SUSE
1. grubモードのインターフェースで、下図のようにカーネルを選択します。
![](https://main.qcloudimg.com/raw/4da4d0c5c98e4f0dbe4990e920a11daf.png)
2. **e**を押してカーネル編集インターフェースに入り、↑↓キーを使用してlinux開始行まで移動し、`splash`パラメータの前に`rw`を追加し、後ろに`1`を加えます。下図のとおりです。
![](https://main.qcloudimg.com/raw/013a0099ccb5c19d04441dd60ea7558b.png)
3. **Ctrl+X**を押し、単一ユーザーモードを起動して入ります。
:::
::: tlinux
1. grubモードのインターフェースで、下図のようにカーネルを選択します。
![](https://main.qcloudimg.com/raw/c497e63321b76e5cd1f0eea06f53cdb2.png)
2. **e**を押してカーネル編集インターフェースに入り、↑↓キーを使用して**kernel**のある行を選択し、再び**e**を押します。下図のようになります。
![](https://main.qcloudimg.com/raw/06c66e0f30163e9fc7e6aafbf9463645.png)
3. 行末、つまり256Mのスペースの後に`1`が追加されます。下図のとおりです。
![](https://main.qcloudimg.com/raw/06efb32e3a2edb39f32e13be1ab8527f.png)
4. **Enter**を押すと、単一ユーザーモードに入ることができます。
:::
</dx-tabs>
