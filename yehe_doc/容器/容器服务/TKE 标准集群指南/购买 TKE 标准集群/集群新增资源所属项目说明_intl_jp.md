## クラスタ追加リソースが所属するプロジェクトの説明
### 概要
プロジェクトごとに財務清算などを行う場合、以下をお読みください：

1. クラスターにはプロジェクト属性がありません。クラスター内部のCVMやロードバランサーなどのリソースにはプロジェクト属性があります。
2. クラスターの追加リソースが所属するプロジェクト：当該クラスターに追加したリソースだけを当該プロジェクトの配下とします。

### アドバイス
1. クラスターにおけるすべてのリソースを同一プロジェクトの配下とすることを推奨します
2. クラスターにおけるCVMを異なるプロジェクトに分散させる場合、CVMコンソールでプロジェクトを移行する必要があります。
3. CVMの所属するプロジェクトが異なる場合、CVMが所属する「セキュリティグループインスタンス」も異なるため、同じクラスターにおけるCVMの「セキュリティグループルール」を統一することを推奨します。
