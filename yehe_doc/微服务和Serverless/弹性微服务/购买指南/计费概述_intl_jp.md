# 課金概要

>! 説明
>
>Tencent Cloud Elastic Microserviceは、2022年7月18日の10:00:00（北京時間）にパブリックベータを終了し、請求が正式に開始します。この製品の使用により発生された請求書と詳細については、Tencent Cloud[料金センター](https://console.intl.cloud.tencent.com/expense/bill/overview)で確認できます。課金モードと課金周期などの詳細については、以下をご参照ください。

## 課金モード
TEMは、**従量課金（後払い）**の課金モードを提供します。

従量課金（後払い）とは、ユーザーの実際のリソース使用量に基づいて請求することであり、未使用の場合は請求されません。請求可能なリソースを作成するときに前払いする必要はなく、リソース消費により発生する費用は、決済周期に従ってTencent Cloudアカウントの残高から自動的に差し引かれます。

## 課金項目と課金区間の説明
TEMの費用は、**環境費用**と**アプリケーション費用**の2つの部分に分けられます。アプリケーション費用には、**CPU**、**メモリ**費用の2つの部分が含まれています。

課金区間は次のとおりです。

- 環境費用：請求は、環境が正常に作成されたときに開始され、環境が正常に破棄されたときに終了します。
- アプリケーション費用：請求は、アプリケーションインスタンスのリソースアサインが完了し、アプリケーションのイメージをプルする準備ができたときに開始され、実行中のインスタンスが終了したときに終了します。

課金項目の明細と価格設定については、[製品の価格設定](https://intl.cloud.tencent.com/document/product/1094/47759)をご参照ください。

## 課金周期
TEMの**課金周期は1分**です。1分未満の場合は、1分としてカウントされます。

## 決済周期
TEMの**決済周期は1時間**です。つまり、時間単位で請求書を生成します。前の決済周期で発生した費用は、Tencent Cloudアカウントの残高から1時間ごとに差し引かれます。

## TEMで他の製品を使用するための課金説明
TEMで、[ファイルシステムCFS](https://intl.cloud.tencent.com/document/product/582/9553)、[Cloud Log Service](https://intl.cloud.tencent.com/document/product/614/37509)など、他の製品を使用する場合は、対応する製品の課金規則に従って請求されます。