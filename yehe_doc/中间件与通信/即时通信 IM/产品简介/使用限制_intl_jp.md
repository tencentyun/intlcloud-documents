## 業務特徴の制限

<table>
        <tr>
            <th  width="15%">機能特徴</th>
            <th  width="20%">制限事項</th>
            <th>制限の説明</th>
        </tr>
        <tr>
            <td  rowspan="5">シングルチャット/グループチャットメッセージ</td>
            <td>コンテンツの長さ</td>
            <td>シングルチャット/グループチャットメッセージは、1件のメッセージの長さは最大12Kとします</td>
        </tr>
	<tr>
            <td>送信頻度</td>
            <td>シングルチャットメッセージの送信頻度：端末での送信には制限がありません。REST APIでの送信の場合、該当するインターフェースには頻度制限があります。詳細については、関連インターフェースのドキュメントをご参照ください。<br>グループチャットメッセージの送信頻度：グループごとに40件/秒とします（すべてのグループタイプを対象とします。異なるグループでの送信は頻度制限がかかりません）</td>
        </tr>
	<tr>
            <td>受信頻度</td>
            <td>Android/iOS/Mac/Windows/iPad：シングルチャットとグループチャットはどちらも無制限です<br>Web：2.11.2より前のSDKの場合、1,000件/秒以下（シングルチャットとグループチャットの合計）とします。2.11.2以降の場合、無制限とします</td>
        </tr>	
        <tr>
            <td>単一のファイルサイズ</td>
		<td><li>ファイルメッセージを送信する時、SDKでは、送信できる単一ファイルの最大サイズは100MBです。</li><li> SDKでは、ファイルメッセージの作成と送信がサポートされません</li><li>WebIM SDKでは、音声メッセージの作成と送信がサポートされません</li></td>
        </tr>
	<tr>
            <td>メッセージ履歴の保存時間</td>
            <td>シングルチャットメッセージと非ライブストリーミンググループメッセージには、メッセージ履歴の保存機能があります。<a href="https://console.cloud.tencent.com/im">IMコンソール</a>にログインして、関連の設定を変更することができます。デフォルトの設定は次のとおりです。<ul style="margin:0;"><li>体験版：7日間。延長不可。</li><li>プロフェッショナル版：7日間。延長可能。</li><li>アルティメット版：30日間。延長可能。</li></ul>履歴メッセージの保存期間の延長は、有料の付加価値サービスです。料金の詳細については、<a href="https://www.tencentcloud.com/document/product/1047/34350#zz">中国本土以外の付加価値サービス料金</a>をご参照ください</td>
        </tr>
        <tr>
            <td>UserID</td>
            <td>命名規則</td>
            <td>ユーザーアカウントの長さは32バイト以下とし、特殊文字はサポートしていません。アルファベットまたは数字の使用をお勧めします</td>
        </tr>
		<tr>
            <td>ユーザープロファイル</td>
            <td>カスタムフィールド</td>
            <td>カスタムフィールドのキーワードはアルファベット、8バイト以下とします。カスタムフィールドの値は最長で500バイト以下とします</td>
        </tr>
        <tr>
            <td>UserSig</td>
            <td>有効期間</td>
            <td>ユーザーパスワード、IMバックエンドSDKのデフォルトインターフェイスによって生成された署名の有効期間は180日です</td>
        </tr>
				<tr>
            <td>セッション管理</td>						
            <td>最近の連絡先の数</td>
            <td>ユーザーごとにデフォルトでは100人の最近連絡先を保存します。アルティメット版では、最近連絡先を500人まで保存できます。具体的な設定は、コンソールで自由に行ってください</td>
        </tr>
        <tr>
            <td  rowspan="2">ユーザーリレーションシップチェーン</td>
            <td>友達とグループ</td>
            <td><ul style="margin:0;"><li>1人のユーザーは3,000友達を追加できます</li><li>友達を追加する時に、最大100件の未読メッセージをサポートします</li><li>友達グループは最大32グループを作成できます</li><li>グループ名は最大30バイトです</li><li>友達ノートは最大96バイトです</li><li>WebIM SDK 2.13.0以降では、友達リレーションシップチェーンがサポートされます</li></ul></td>
        </tr>
        <tr>
            <td>ブラックリスト</td>
            <td>ユーザー1人あたりのブラックリストの最大許容人数は1,000人です</td>
        </tr>
         <tr>
            <td  rowspan="8">グループ</td>
            <td>グループ数</td>
            <td>単一SDKAppIDに同時に存在するすべてのグループタイプのグループ数の合計を指します。既に解散したグループはカウントされません。ピーク値に達している場合、使用しなくなるグループを解散して、新しいグループを作成すればよいです。具体的な制限は次のとおりです。<li>体験版：100件</li><li>プロフェッショナル版またはアルティメット版：無制限</li><br>1日あたりの正味グループ追加数は最大で1万グループで、無料ピークグループ数は10万/月です。ピークグループ数が無料利用枠を超えると、パッケージ超過分の料金が発生します。料金の詳細については、<a href="https://www.tencentcloud.com/document/product/1047/34350#jc">中国本土以外パッケージ超過分の料金</a>をご参照ください</li></ul></td>
        </tr>
        <tr>
            <td>グループメンバー数</td>
            <td>ライブストリーミンググループ(AvChatRoom)：メンバー数には上限がありません<br>非ライブストリーミンググループのデフォルト設定は次のとおりです。<ul style="margin:0;"><li>体験版：20人/グループ</li><li>プロフェッショナル版：200人/グループ。2,000人/グループまで拡張可能</li><li>アルティメット版：2,000人/グループ。6,000人/グループまで拡張可能</li>グループメンバー数の上限拡張は、有料の付加価値サービスです。料金の詳細については、<a href="https://www.tencentcloud.com/document/product/1047/34350#zz">中国本土以外の付加価値サービス料金</a>をご参照ください</ul></td>
        </tr>
        <tr>
            <td>ユーザーが参加できるグループ数</td>
            <td>ユーザーが同時に参加したすべてのグループタイプのグループ数の合計を指します。具体的な制限は次のとおりです：<ul style="margin:0;"><li>体験版：50人/グループ</li><li>プロフェッショナル版：500人/グループ。1000人/グループまで拡張可能</li><li>アルティメット版：3000人/グループまで拡張可能</ul>ユーザーが参加できるグループ数の上限拡張は、有料の付加価値サービスです。料金の詳細については、<a href="https://www.tencentcloud.com/document/product/1047/34350#zz">中国本土以外の付加価値サービス料金</a>をご参照ください</li></td>
        </tr>
        <tr>
            <td>グループ情報</td>
            <td><ul style="margin:0;"><li>グループ名の最長は30バイトです</li><li>グループ概要の最長は240バイトです</li><li>グループアナウンスの最長は300バイトです</li><li>グループプロファイルフォトのURLの最長は100バイトです</li><li>グループ名刺の最長は50バイト以下です</li></ul></td>
        </tr>
        <tr>
            <td>カスタムグループID</td>
            <td>カスタムグループIDは、印刷可能なASCII文字(0x20-0x7e)でなければなりません。最長48バイトとし、プレフィックスに@TGS#を設定することはできません（デフォルトで割り当てられたグループIDとの混同を避けるため）</td>
        </tr>
        <tr>
            <td>グループディメンションのカスタムフィールド</td>
            <td>グループディメンションは最大10件のカスタムフィールドをサポートします。<ul style="margin:0;"><li> KeyフィールドはString型で、長さは16バイト以下です。命名では、アルファベットの大文字・小文字、数字、下線のみをサポートしています。</li><li> Valueフィールドはユーザー定義のBufferで、バイナリーデータにすることができます。グループディメンションのValueの長さは、512バイト以下とします</li></ul></td>
        </tr>
        <tr>
            <td>グループメンバーディメンションのカスタムフィールド</td>
            <td>グループメンバーディメンションは最大5件のカスタムフィールドをサポートします。<ul style="margin:0;"><li> KeyフィールドはString型で、長さは16バイト以下です。命名では、アルファベットの大文字・小文字、数字、下線のみをサポートしています。</li><li> Valueフィールドはユーザー定義のBufferであり、バイナリーデータにすることができます。グループディメンションのValueの長さは、64バイト以下とします</li></ul></td>
        </tr>
        <tr>
            <td>コミュニティ内のトピックス数</td>
            <td>現在、1つのコミュニティでは、200トピックスまでサポートされています</td>
        </tr></table>


## インターフェース関連の制限
>?ここでは、使用制限を伴うREST APIのみをリストアップしています。APIのより包括的なリストについては、[REST APIインターフェースリスト](https://intl.cloud.tencent.com/document/product/1047/34621)をご参照ください。

### 共通制限

<table>
        <tr>
            <th  width="30%">制限事項</th>
            <th>制限の説明</th>
        </tr>
        <tr>
            <td>呼び出し頻度</ td>
            <td><ul style="margin:0;"><li>最大100回/秒：<a href="https://intl.cloud.tencent.com/document/product/1047/34954">複数アカウントのインポート</a>、<a href="https://intl.cloud.tencent.com/document/product/1047/34955">アカウントを削除</a>および<a href="https://intl.cloud.tencent.com/document/product/1047/34956">アカウントのクエリー</a></li><li>最大200回/秒：その他は<a href="https://intl.cloud.tencent.com/document/product/1047/34621">REST API</a></li></ul></td>
        </tr>
</table>



### アカウント管理

<table>
        <tr>
            <th  width="30%">インターフェース</th>
            <th>制限の説明</th>
        </tr>
        <tr>
            <td>複数アカウントのインポート</td>
            <td>1回あたり最大100件のユーザー名をインポートします。また、このインターフェースは、アカウントのニックネームとプロファイルフォト情報の直接インポートはサポートしていません</td>
        </tr>
				<tr>
            <td>アカウントのオンライン状態をクエリーします</td>
            <td>1回のリクエストで最大500人のユーザーの状態をクエリーできます</td>
        </tr>
</table>

### シングルチャットメッセージ

<table>
        <tr>
            <th  width="30%">インターフェース</th>
            <th>制限の説明</th>
        </tr>
        <tr>
            <td>シングルチャットメッセージの一斉送信</td>
            <td>1回のリクエストで最大500人のユーザーにシングルチャットメッセージを送信できます</td>
        </tr>
</table>


### リレーションシップチェーン管理 


<table>
        <tr>
            <th  width="30%">インターフェース</th>
            <th>制限の説明</th>
        </tr>
        <tr>
            <td>フレンドのインポート</td>
            <td>1回のリクエストでは、最大1,000人のフレンドをインポートできます</td>
        </tr>
</table>


### グループ管理

<table>
        <tr>
            <th  width="30%">インターフェース</th>
            <th>制限の説明</th>
        </tr>
        <tr>
            <td>グループメンバーの追加</td>
            <td>1度に最大100人のメンバーを追加できます</td>
        </tr>
        <tr>
            <td>グループメンバーの削除</ td>
            <td>1回のリクエストで最大500人のメンバーを削除できます</td>
        </tr>
        <tr>
            <td>グループ内でのユーザーIDのクエリー</td>
            <td>1回のリクエストで最大500のアカウントのクエリーをサポートします</td>
        </tr>
        <tr>
            <td>アカウントの一斉停止とアカウント停止の解除</td>
            <td>1回のリクエストで最大500件のアカウントを停止/停止解除できます</td>
        </tr>
        <tr>
            <td>グループ内での通常メッセージの送信</td>
            <td>1グループあたりのデフォルトの送信頻度は40件/秒に制限されています。<br><b>5分以内に同じ送信者から送信された2つのメッセージのランダム値（Randomパラメータ）が同じである場合、後のメッセージは重複メッセージとみなされ、破棄されます</b></td>
        </tr>
        <tr>
            <td>グループメッセージのインポート</td>
            <td>1回のリクエストで最大20件のメッセージをインポートできます。メッセージのタイムスタンプが大きい順にインポートする必要があります。メッセージのタイムスタンプは、グループの作成時刻より後、現在時刻より前にしなければならず、そうでない場合は失敗します</td>
        </tr>
        <tr>
            <td>グループメンバーのインポート</td>
            <td>ライブストリーミンググループ(AvChatRoom)は、グループメンバーのインポートをサポートしていません。<br>1回のリクエストで最大300人のメンバーをインポートできますが、グループメンバーの上限は、同時にさまざまなグループタイプの特性から制約を受けます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/1047/33515">グループ機能</a>をご参照ください</td>
        </tr>
</table>
