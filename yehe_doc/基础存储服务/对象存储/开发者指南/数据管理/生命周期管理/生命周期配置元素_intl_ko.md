## 기본 구조

라이프사이클 설정은 XML 설명 방법을 사용합니다. 단일 또는 다중 라이프사이클 규칙을 설정할 수 있으며 기본 구조는 다음과 같습니다.

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

모든 규칙은 다음 내용을 포함합니다.

- ID(선택 사항): 규칙의 내용을 나타내며 사용자 정의할 수 있습니다.
- Status: 규칙의 활성화 Enable 또는 비활성화 Disable 여부를 나타냅니다.
- Filter: 규칙이 적용되는 객체를 식별합니다.
- 작업: 위의 설명과 일치하는 객체에 대해 수행해야 하는 작업입니다.
- 시간: Days(객체가 마지막으로 수정된 날짜부터 계산됨) 또는 객체에 대해 수행된 작업을 기반으로 하는 Date입니다.

## 규칙 설명

### Filter 요소

#### 버킷의 모든 객체 대상

비어있는 필터링 조건을 지정하면 버킷의 모든 객체에 적용됩니다.

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

#### 지정된 객체 키 접두사 대상

객체 접두사를 지정하면 접두사 설명에 부합한 일부 객체 그룹에 대해 작업을 수행할 수 있습니다. 예를 들어, logs/를 접두사로 한 모든 객체를 설정합니다.

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

#### 지정된 객체 태그 대상

객체 태그에 부합한 key와 value를 필터링 조건으로 지정하고, 특정 태그의 객체에 대한 작업을 수행합니다. 예를 들어, 태그의 key=type과 value=image를 필터링 조건으로 한 객체를 설정합니다.
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

#### 다중 필터링 조건 통합 사용

Tencent Cloud COS(Cloud Object Storage)는 AND의 로직을 통해 다중 필터링 조건을 통합 사용할 수 있습니다. 예를 들어, logs/를 접두사로 하면서 객체 태그의 key=type과 value=image를 필터링 조건으로 한 객체를 설정합니다.
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

### 작업 요소

라이프사이클 규칙 중, 조건에 부합한 한 그룹 객체에 단일 또는 다중 작업을 수행할 수 있습니다.

#### 전환 작업

한 스토리지 유형에서 다른 스토리지 유형으로 객체를 전환하려면 Transition 작업을 지정합니다. 버전이 지정된 버킷의 경우 전환 작업이 현재 객체 버전에 적용됩니다. Transition 날짜를 0일로 짧게 설정할 수 있습니다. 예를 들어 30일 후에 객체를 아카이브 스토리지로 전환합니다.

```xml
<Transition>
	<StorageClass>ARCHIVE</StorageClass>
    <Days>30</Days>
</Transition>
```

### 만료 삭제

만료된 객체를 삭제하려면 Expiration 작업을 지정합니다. 버전이 지정되지 않은 버킷의 경우 만료된 객체는 영구적으로 삭제됩니다. 버전이 지정된 버킷의 경우 만료된 객체가 **DeleteMarker로 추가**되고 현재 버전이 됩니다. 예를 들어 만료일이 30일인 객체를 삭제합니다.
```xml
<Expiration>
	<Days>30</Days>
</Expiration>
```

### 미완성 멀티파트 업로드


>! 동일한 라이프사이클 규칙에서 객체 태그 지정과 업로드 완료되지 않은 파일 조각 정리를 동시에 설정할 수 없습니다.
>

미리 정의된 기간 내에 성공적으로 완료되지 않은 경우 특정 UploadId가 있는 멀티파트 업로드 작업을 삭제하려면 AbortIncompleteMultipartUpload 작업을 지정하십시오. 이 경우 이러한 작업도 재개하거나 인덱싱할 수 없습니다. 예를 들어, 7일 이내에 성공적으로 완료되지 않은 멀티파트 업로드 작업을 중단합니다.
```xml
<AbortIncompleteMultipartUpload>
   <DaysAfterInitiation>7</DaysAfterInitiation>
</AbortIncompleteMultipartUpload>
```

#### 현재 버전이 아닌 객체

버전이 지정된 버킷에서 전환 작업은 최신 버전의 객체에만 적용되고 만료 작업은 객체에 삭제 마커를 추가하는 결과만 가져옵니다. 따라서 COS는 현재 버전이 아닌 객체에 대해 다음 작업을 제공합니다.

지정된 시간에 현재 버전의 객체를 다른 스토리지 클래스로 전환하려면 NoncurrentVersionTransition 작업을 지정합니다. 예를 들어, 30일 후에 객체의 이전 버전을 아카이브 스토리지로 전환합니다.

```xml
<NoncurrentVersionTransition>
	<StorageClass>ARCHIVE</StorageClass>
    <Days>30</Days>
</NoncurrentVersionTransition>
```

지정된 시간에 만료된 현재 버전의 객체를 삭제하려면 NoncurrentVersionExpiration 작업을 지정합니다. 예를 들어 30일 후에 만료된 이전 버전의 객체를 삭제합니다.
```xml
<NoncurrentVersionExpiration>
	<Days>30</Days>
</NoncurrentVersionExpiration>
```

ExpiredObjectDeleteMarker를 지정하여 나머지 삭제 마커를 제거합니다. 입력 가능 값은 true 또는 false입니다. 이 옵션의 적용은 만료된 기록 버전(NoncurrentVersionExpiration) 제거 작업에 의해 트리거됩니다. 이 기능이 활성화되어 있으면 객체의 마지막 기록 버전이 라이프사이클에 의해 삭제될 때 나머지 여러 삭제 마커가 자동으로 제거됩니다.

만료된 기록 버전(NoncurrentVersionExpiration) 제거 작업이 적용되는 구체적인 상황은 다음과 같습니다.
- ExpiredObjectDeleteMarker 활성화 여부와 상관없이 삭제 마커가 하나만 남아 있으면 마지막 삭제 마커가 자동으로 정리됩니다.
- 남은 삭제 마커가 여러 개인 경우 COS는 ExpiredObjectDeleteMarker가 활성화되어 있는지 확인합니다. true이면 나머지 여러 삭제 마커가 자동으로 정리되고, false이면 나머지 여러 삭제 마커가 정리되지 않습니다.


```xml
<ExpiredObjectDeleteMarker>
	<Days>true|false</Days>
</ExpiredObjectDeleteMarker>
```

### 시간 요소

#### 일별 계산

Days는 객체가 마지막으로 수정된 이후의 일 수를 나타냅니다.
- 예를 들어 객체가 0일 후 아카이브 스토리지로 전환되도록 설정되어 있는 경우 객체가 2018-01-01 23:55:00 GMT+8에 업로드되면 2018-01-02 00:00:00 GMT+8에 전환 대기열에 추가되고 2018-01-02 23:59:59 GMT+8 이전에 전환됩니다.
- 예를 들어 객체가 만료로 인해 1일 후에 삭제되도록 설정되어 있는 경우 객체가 2018-01-01 23:55:00 GMT+8에 업로드되면 객체가 2018-01-03 00:00:00 GMT+8에 만료 대기열에 추가되고 2018-01-03 23:59:59 GMT+8 이전에 삭제됩니다.

#### 지정 날짜 기준

특정 Date의 필터 기준에 따라 모든 규정된 개체에 대해 미리 정의된 작업을 수행합니다. 날짜 값은 ISO8601 형식을 따라야 합니다. 시간은 항상 00:00 GMT+8입니다.
예를 들어, 2018년 01월 01일은 2018-01-01T00:00:00+08:00로 사용합니다.


