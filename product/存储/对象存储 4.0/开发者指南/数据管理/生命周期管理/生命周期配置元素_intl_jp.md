## 基本的構造

ライフサイクルの構成はXML説明方法を使用し、1つまたは複数のライフサイクルルールを構成できます。その基本的構造を下記に示します：

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

そのうち、すべてのルールは下記内容を含みます：

- ID（オプション）：ルールの内容をカスタマイズ説明できます。
- Status：ルールの有効Enabledまたは無効Disabledの状態を選択できます。
- Filter：操作を必要とするオブジェクトの選別条件の指定に用いられます。
- 操作：上記説明に適合するオブジェクトの実行を必要とする操作。
- 時間：最終変更時間により日数`Days`を指定し、または特定の日付`Date`の前に変更したオブジェクトを指定することをサポートします。

## ルールの説明

### Filter要素

#### バケットにおけるすべてのオブジェクトを対象に

ブランクを指定する選別条件は、バケットにおけるすべてのオブジェクトに応用されます。

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

#### 指定のオブジェクトキーのプレフィックスを対象に

オブジェクトのプレフィックスを指定し、プレフィックスの説明に適合する一部のオブジェクトグループに対して操作を実行できます。例えば、`logs/`をプレフィックスとするすべてのオブジェクトを設定します。

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

#### 指定のオブジェクトタグを対象に

オブジェクトタグに適合する一部の`key`と`value`を選別条件に指定し、特定タグのオブジェクトに対して操作を実行します。例えば、タグの`key=type`と`value=image`を選別条件のオブジェクトに設定します：

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

#### 複数の選別条件の一括使用

Tencent Cloud COSは`AND`のロジックによる複数の選別条件の一括使用をサポートします。例えば、`logs/`をプレフィックスとし、同時にオブジェクトタグの`key=type`と`value=image`を選別条件とするオブジェクトを設定します：

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

### 操作の要素

ライフサイクルルールにおいて、条件に適合するオブジェクトグループに対して1つまたは複数の操作を実行できます。

#### 変換の操作

Transition操作を指定することで、オブジェクトのストレージタイプをその他のストレージタイプに変換できます。バケットがバージョンコントロールをオンにしている場合、最新バージョンのみに対して操作を実行できます。最短のTransition時間を0日に設定します。例えば、30日後にCASに沈下するように設定します：

```xml
<Transition>
	<StorageClass>ARCHIVE</StorageClass>
    <Days>30</Days>
</Transition>
```

#### 期限切れ時の削除

Expiration操作を指定することで、ルールに適合するオブジェクトが期限切れ時の削除を実現できます。バケットがバージョンコントロールをオンにしたことがない場合、オブジェクトは完全に削除されます。バケットがバージョンコントロールをオンにしたことがある場合、期限切れのオブジェクトに**DeleteMarkerのマーカーを付け**、それを最新バージョンに設定します。例えば、30日後にオブジェクトが削除されるように設定します：

```xml
<Expiration>
	<Days>30</Days>
</Expiration>
```

#### 未完了のパートアップロード

AbortIncompleteMultipartUpload操作を指定することで、パートアップロードされた指定UploadIdタスクが一定の継続時間後に削除されるように確保できます。その継続送信または検索可能性の特性が消えます。例えば、7日後に未完了のパートアップロードのタスクが削除されるように設定します：

```xml
<AbortIncompleteMultipartUpload>
	<Days>7</Days>
</AbortIncompleteMultipartUpload>
```

#### 最新バージョンでないオブジェクト

バージョンコントロールをオンにしたことのあるバケットにおいて、最新バージョンの変換のみが実行されます。期限切れの操作につき、削除タグの追加のみが実行されます。したがって、Tencent Cloud COSでは、最新バージョンでないオブジェクトに対して下記操作を提供します：

NoncurrentVersionTransitionを指定することで、最新バージョンでないオブジェクトを指定時間内にその他のストレージタイプに変換できます。例えば、過去バージョンが30日後にCASに沈下させるように設定します：

```xml
<NoncurrentVersionTransition>
	<StorageClass>ARCHIVE</StorageClass>
    <Days>30</Days>
</NoncurrentVersionTransition>
```

NoncurrentVersionExpirationをしてすることで、最新バージョンでないオブジェクトを期限切れ時に削除できます。例えば、過去バージョンが30日後に削除されるように設定します：

```xml
<NoncurrentVersionExpiration>
	<Days>30</Days>
</NoncurrentVersionExpiration>
```

ExpiredObjectDeleteMarkerを指定することで、オブジェクトキーのすべての過去バージョンが削除され、且つ最新オブジェクトのバージョンが削除タグDeleteMarkerである場合、この削除タグを削除できます。例えば、31日後に、期限切れたオブジェクトの削除タグが削除されるように設定します：

```xml
<ExpiredObjectDeleteMarker>
	<Days>31</Days>
</ExpiredObjectDeleteMarker>
```

### 時間要素

#### 日数による計算

`Days`で日数を指定する場合、オブジェクトの最終変更時間により計算されます。
例えば、あるオブジェクトが0日後にCASタイプに変換され、オブジェクトは2018-01-01 23:55:00 GMT+8にアップロードされるように設定する場合、2018-01-02 00:00:00 GMT+8にストレージタイプを変換する処理キューに加えられ、最遅2018-01-02 23:59:59 GMT+8までに変換を完了させます。
例えば、あるオブジェクトが1日後の期限切れ時に削除され、オブジェクトは2018-01-01 23:55:00 GMT+8にアップロードされるように設定する場合、2018-01-03 00:00:00 GMT+8に期限切れ時の削除処理キューに加えられ、最遅2018-01-03 23:59:59 GMT+8までに削除を完了させます。

#### 指定日付による計算

`Date`で日付を指定する場合、特定の日付に達する時、選別条件に適合するすべてのオブジェクトに対してこの操作を実行します。現時点では、GMT+8タイムゾーンに指定され、0時に設定されたISO8601フォーマットの時間のみをサポートします。
例えば、2018年1月1日の説明：`2018-01-01T00:00:00+08:00`。
