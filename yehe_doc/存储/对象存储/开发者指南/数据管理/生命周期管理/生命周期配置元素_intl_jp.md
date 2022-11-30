## 基本構造

ライフサイクルの設定にはXML記述方法を使用します。1つまたは複数のライフサイクルルールを設定することが可能です。基本構造は次のとおりです。

```xml
<LifecycleConfiguration>
	<Rule>
		<ID>**your lifecycle name**</ID>
        <Status>Enabled</Status>
        <Filter>
            <And>
            	<Prefix>projectA/</Prefix>
                <Tag>
                	<Key>key1</Key>
                    <Value>value1</Value>
                </Tag>
            </And>
        </Filter>
        **transition/expiration actions**
	</Rule>
	<Rule>
		...
	</Rule>
</LifecycleConfiguration>
```

各ルールには次の内容が含まれます。

- ID（オプション）：カスタマイズ可能な記述ルールの内容です。
- Status：ルールの有効（Enabled）または無効（Disabled）のステータスを選択できます。
- Filter：操作したいオブジェクトのフィルタリング条件の指定に用います。
- アクション：上記の記述に該当するオブジェクトに対して実行する必要がある操作です。
- 時間：最終変更時間に基づいて日数（Days）を指定するか、またはある具体的な日付（Date）までに変更するオブジェクトを指定することができます。

## ルールの記述

### Filter要素

#### バケット内の全オブジェクトを対象とする

空のフィルタリング条件を指定すると、バケット内の全オブジェクトに適用されます。

```xml
<LifecycleConfiguration>
    <Rule>
        <Filter>
        </Filter>
        <Status>Enabled</Status>
        **transition/expiration actions**
    </Rule>
</LifecycleConfiguration>
```

#### 指定したオブジェクトキーのプレフィックスを対象とする

オブジェクトのプレフィックスを指定することで、プレフィックスの記述に該当する一部のオブジェクトグループに対してアクションを実行することができます。例えば、logs/をプレフィックスとするすべてのオブジェクトを設定する場合は次のようになります。

```xml
<LifecycleConfiguration>
    <Rule>
        <Filter>
           <Prefix>logs/</Prefix>
        </Filter>
        <Status>Enabled</Status>
        **transition/expiration actions**
    </Rule>
</LifecycleConfiguration>
```

#### 指定したオブジェクトタグを対象とする

あるオブジェクトキーに該当するkeyおよびvalueをフィルタリング条件として指定し、特定のタグのオブジェクトに対しアクションを実行します。例えば、タグのkey=typeおよびvalue=imageをフィルタリング条件としてオブジェクトを設定する場合は次のようになります。
```xml
<LifecycleConfiguration>
    <Rule>
        <Filter>
           <Tag>
              <Key>type</Key>
              <Value>image</Value>
           </Tag>
        </Filter>
        <Status>Enabled</Status>
        **transition/expiration actions**
    </Rule>
</LifecycleConfiguration>
```

#### 複数のフィルタリング条件を併用する

Tencent CloudのCloud Object Storage（COS）は、ANDロジックによる複数のフィルタリング条件の併用をサポートしています。例えば、logs/をプレフィックスとして設定すると同時に、オブジェクトタグのkey=typeおよびvalue=imageをフィルタリング条件としてオブジェクトを設定する場合は次のようになります。
```xml
<LifecycleConfiguration>
    <Rule>
        <Filter>
            <And>
            	<Prefix>logs/</Prefix>
                <Tag>
              		<Key>type</Key>
              		<Value>image</Value>
           	 </Tag>
            </And>
        </Filter>
        <Status>Enabled</Status>
        **transition/expiration actions**
    </Rule>
</LifecycleConfiguration>
```

### アクションの要素

ライフサイクルルールにおいて、条件に該当するオブジェクトのグループに対し、1つまたは複数のアクションを実行することができます。

#### 切り替えアクション

Transitionアクションを指定すると、オブジェクトをあるストレージタイプから別のストレージタイプに切り替えることができます。バケットでバージョン管理を有効にしている場合は、現在のバージョンに対してのみアクションが実行されます。最短のTransition設定時間は0日です。例えば、30日後にアーカイブストレージに移行するよう設定する場合は次のようになります。

```xml
<Transition>
	<StorageClass>ARCHIVE</StorageClass>
    <Days>30</Days>
</Transition>
```

#### 期限切れの削除

Expirationアクションを指定すると、ルールに該当するオブジェクトに対し期限切れ後に削除するアクションを行うことができます。バケットのバージョン管理を有効にしていない場合は、オブジェクトが完全に削除されます。バケットのバージョン管理を有効にしている場合は、期限切れのオブジェクトに**DeleteMarkerを追加**し、それを現在のバージョンとして設定します。例えば、30日後にオブジェクトを削除するよう設定する場合は次のようになります。
```xml
<Expiration>
	<Days>30</Days>
</Expiration>
```

#### 未完了のマルチパートアップロード


>! 同一のライフサイクルルール内で、指定したオブジェクトタグの設定とアップロードが完了していないファイルフラグメントのクリーンアップを同時に行うことはサポートしていません。
>

AbortIncompleteMultipartUploadアクションを指定すると、マルチパートアップロードの指定されたUploadIdタスクを一定期間保持した後に削除することを許可し、それについてはアップロード再開または検索可能な特性の提供も行われないようにすることができます。例えば、未完了のマルチパートアップロードタスクを7日後に消去するよう設定する場合は次のようになります。
```xml
<AbortIncompleteMultipartUpload>
   <DaysAfterInitiation>7</DaysAfterInitiation>
</AbortIncompleteMultipartUpload>
```

#### 現在のバージョンではないオブジェクト

バージョン管理を有効にしているバケットでは、切り替えは最新バージョンに対してのみ実行され、期限切れ操作は削除マーカーの追加だけとなります。そのため、COSでは現在のバージョンではないオブジェクトに対して、次のような操作を提供しています。

NoncurrentVersionTransitionを指定すると、現在のバージョンではないオブジェクトを指定の時間に別のストレージタイプに切り替えることができます。例えば、過去のバージョンを30日後にアーカイブストレージに移行するよう設定する場合は次のようになります。

```xml
<NoncurrentVersionTransition>
	<StorageClass>ARCHIVE</StorageClass>
    <Days>30</Days>
</NoncurrentVersionTransition>
```

NoncurrentVersionExpirationを指定すると、現在のバージョンではないオブジェクトを指定の時間に期限切れとして削除することができます。例えば、過去のバージョンを30日後に削除するよう設定する場合は次のようになります。
```xml
<NoncurrentVersionExpiration>
	<Days>30</Days>
</NoncurrentVersionExpiration>
```

ExpiredObjectDeleteMarkerの指定は余分な削除マーカーを消去するために用います。入力可能な値はtrueまたはfalseです。このオプションの発効は、期限切れとなった過去のバージョンを消去する動作（NoncurrentVersionExpiration）によってトリガーされます。この機能を有効にすると、ライフサイクルによってオブジェクトの最後の過去バージョンが削除された時点で、余分な複数の削除マーカーが自動的に消去されます。

具体的には次のようになります。期限切れとなった過去のバージョンを消去する動作（NoncurrentVersionExpiration）が発効した時点で、
- 余分な削除マーカーが1個しかない場合は、ExpiredObjectDeleteMarkerが有効かどうかにかかわらず、最後の削除マーカーが自動的に消去されます。
- 余分な削除マーカーが複数ある場合は、ExpiredObjectDeleteMarkerが有効かどうかをCOSがチェックします。その結果がtrueであれば、余分な複数の削除マーカーが自動的に消去されます。falseであれば、余分な複数の削除マーカーは消去されません。


```xml
<ExpiredObjectDeleteMarker>
	<Days>true|false</Days>
</ExpiredObjectDeleteMarker>
```

### 時間の要素

#### 日数に基づく計算

Daysを使用する日数の計算は、 オブジェクトの最終変更時間に基づいて行われます。
- 例えば、あるオブジェクトを0日後にアーカイブストレージタイプに切り替えるよう設定し、オブジェクトを2018-01-01 23:55:00 GMT+8にアップロードした場合、そのオブジェクトは2018-01-02 00:00:00 GMT+8からストレージタイプ切り替えの処理キューに入り、遅くとも2018-01-02 23:59:59 GMT+8までに切り替えが完了します。
- 例えば、あるオブジェクトを1日後に期限切れとして削除するよう設定し、オブジェクトを2018-01-01 23:55:00 GMT+8にアップロードした場合、そのオブジェクトは2018-01-03 00:00:00 GMT+8から期限切れ削除の処理キューに入り、遅くとも2018-01-03 23:59:59 GMT+8までに削除が完了します。

#### 指定の日付に基づく

Dateを使用して日付を指定すると、特定の日付になった時点で、フィルタリング条件に該当するすべてのオブジェクトに対しこのアクションが実行されます。現時点ではGMT+8タイムゾーンの、0時に設定するISO8601形式の時間のみサポートしています。
例えば、2018年1月1日の場合、2018-01-01T00:00:00+08:00と記述します。


