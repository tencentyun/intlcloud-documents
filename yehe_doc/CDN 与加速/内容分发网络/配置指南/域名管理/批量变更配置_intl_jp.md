## 機能シナリオ

一括変更設定では、複数のアクセラレーションドメイン名に対して、ドメイン名設定を同時に変更する機能をサポートしています。複数のドメイン名に対し、特定のドメイン名設定項目の変更を行いたい場合に、この機能を使えば、1つ1つのドメイン名に対して操作する必要なく一括で操作でき、設定効率をアップさせることができます。



## 操作ガイド

[CDN コンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のメニューバーから【Domain Management】を選択して、ドメイン名管理のページに入ります。アクティブになっているドメイン名を2つもしくは2つ以上選択した時に、上側の【更なる操作】の中で【一括変更設定】をクリックすると、一括変更設定のページに入れます。
![](https://main.qcloudimg.com/raw/8ef48d5c4b5f2794eb97850cdb275de3.png)


>!
>- すでに無効化/封鎖/ロックされているドメイン名については、一括変更設定機能はサポートされません。
>- 選択したドメイン名に特別なバックエンド設定（コンソール以外の設定）がある場合、その特別な設定は変更できません。


##  その他の説明

- 設定変更の操作後は元に戻せません。変更後は通常のドメイン名設定で管理することが可能です。
- 一部の設定項目はアクセラレーションリージョン/サービスタイプ/HTTPS証明書と関連付けられているため、アクセラレーションリージョン/サービスタイプ/HTTPS設定の状態が同じドメイン名を選択して、一括変更を行うことを推奨します。
- HTTPS証明書の設定の一括変更については、証明書管理のページで行ってください。ここではサポートしていません。
- 1回につき、最大50ドメイン名の同時変更をサポートしています。ドメイン名が多いほど、変更を配布する時間が長くなります。一括変更1回あたりに選択するドメイン名を多くしすぎないでください。
- この機能はドメイン名のすべての設定項目をカバーしているわけではなく、まだサポートされていない設定項目がいくつかあります。今後少しずつアップデートし、リリースしていく予定です。
