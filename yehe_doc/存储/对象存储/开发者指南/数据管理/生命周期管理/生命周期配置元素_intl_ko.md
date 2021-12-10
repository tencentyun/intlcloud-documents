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

- ID(선택 사항): 사용자 지정 가능한 설명 규칙의 콘텐츠
- Status: 규칙으로 활성화 Enable 또는 비활성화 Disable된 상태를 선택할 수 있음
- Filter: 작업이 필요한 객체의 필터링 조건을 지정하는데 사용함
- 작업: 위 설명에 적합한 객체에 대해 수행할 작업이 필요함
- 시간: 마지막 수정 시간에 따라 일수 Days를 지정하거나, 구체적인 날짜 Date 이전에 수정한 객체를 지정할 수 있음

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

객체 접두사를 지정하면 접두사 설명에 부합한 일부 객체 그룹에 대해 작업을 수행할 수 있습니다. 예를 들어, logs/ 를 접두사로 한 모든 객체를 설정합니다.

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

객체 태그에 부합한 key 와 value 를 필터링 조건으로 지정하고, 특정 태그의 객체에 대한 작업을 수행합니다. 예를 들어, 태그의 key=type과 value=image 를 필터링 조건으로 한 객체를 설정합니다.

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

Tencent Cloud COS는 AND 의 로직을 통해 다중 필터링 조건을 통합 사용할 수 있습니다. 예를 들어, logs/를 접두사로 하면서 객체 태그의 key=type과 value=image를 필터링 조건으로 한 객체를 설정합니다.

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

Transition 작업을 지정하면 객체를 하나의 스토리지 유형에서 다른 스토리지 유형으로 전환할 수 있습니다. 버킷이 버전 제어를 활성화하면 현재 버전에 대해서만 작업을 수행하며, 최단 Transition 설정 시간은 0입니다. 예를 들어 30일 후 CAS로 전환되도록 설정합니다.

```xml
<Transition>
	<StorageClass>ARCHIVE</StorageClass>
    <Days>30</Days>
</Transition>
```

### 만료 삭제

Expiration 작업을 지정하면 규칙에 부합한 객체가 만료 삭제 작업을 수행할 수 있도록 합니다. 버킷이 버전 제어를 활성화한 적이 없으면 대상을 영구 삭제합니다. 버킷이 버전 제어를 활성화한 적이 있으면 만료 객체에 **DeleteMarker 표시를 추가하고**, 현재 버전으로 설정합니다. 예를 들어 30일 후 객체를 삭제하도록 설정합니다.

```xml
<Expiration>
	<Days>30</Days>
</Expiration>
```

### 미완성 멀티파트 업로드

AbortIncompleteMultipartUpload 작업을 지정하면 멀티파트 업로드의 지정 UploadId 작업이 일정 기간 동안 유지 후 삭제되도록 허용하며, 계속 업로드 또는 인덱스 가능한 특성을 제공하지 않습니다. 예를 들어, 7일 후 미완성 멀티파트 업로드 작업을 제거하도록 설정합니다.

```xml
<AbortIncompleteMultipartUpload>
	<Days>7</Days>
</AbortIncompleteMultipartUpload>
```

#### 현재 버전이 아닌 객체

버전 제어를 활성화한 적 있는 버킷에서는 전환이 최신 버전에서만 수행되고 만료 작업은 삭제 표시만 추가되므로, Cloud Object Storage COS는 현재 버전이 아닌 객체에 대해 다음과 같은 작업을 제공합니다.

NoncurrentVersionTransition을 지정하면 현재 버전이 아닌 객체를 지정 시간에 다른 스토리지 유형으로 전환할 수 있습니다. 예를 들어 이전 버전이 30일 후 CAS로 전환되도록 설정합니다.

```xml
<NoncurrentVersionTransition>
	<StorageClass>ARCHIVE</StorageClass>
    <Days>30</Days>
</NoncurrentVersionTransition>
```

NoncurrentVersionExpiration을 지정하면 현재 버전이 아닌 객체를 지정 시간 내 만료 삭제할 수 있습니다. 예를 들어 이전 버전이 30일 후 삭제되도록 설정합니다.

```xml
<NoncurrentVersionExpiration>
	<Days>30</Days>
</NoncurrentVersionExpiration>
```

ExpiredObjectDeleteMarker를 지정하면 객체 키의 모든 이전 버전을 삭제할 수 있으며, 최신 객체 버전은 삭제 표시 DeleteMarker를 삭제할 때 이 삭제 표시를 제거할 수 있습니다. 예를 들어 31일 후 만료 객체의 삭제 표기를 제거하도록 설정합니다.

```xml
<ExpiredObjectDeleteMarker>
	<Days>31</Days>
</ExpiredObjectDeleteMarker>
```

### 시간 요소

#### 일별 계산

Days를 사용해 지정된 일수는 객체의 최종 수정 시간에 따라 계산한 것입니다.
- 예를 들어 한 객체를 0일 후 CAS 유형으로 전환되도록 설정할 경우, 객체는 2018-01-01 23:55:00 GMT+8에 업로드되며, 2018-01-02 00:00:00 GMT+8부터 전환 스토리지 유형의 처리 큐로 들어가, 늦어도 2018-01-02 23:59:59 GMT+8 전에 전환을 완료합니다.
- 예를 들어 한 객체를 1일 후 만료 삭제되도록 설정할 경우, 객체는 2018-01-01 23:55:00 GMT+8에 업로드되며, 2018-01-03 00:00:00 GMT+8부터 만료 삭제된 처리 큐로 들어가, 늦어도 2018-01-03 23:59:59 GMT+8 전에 삭제를 완료합니다.

#### 지정 날짜에 따라

Date를 사용해 날짜를 지정하면 특정 날짜가 됐을 때, 필터링 조건에 부합한 모든 객체는 해당 작업을 수행하게 됩니다. 현재는 GMT+8을 기준으로 ISO8601 형식의 시간이 0으로 지정된 설정만 지원합니다.
예를 들어, 2018년 1월 1일은 `2018-01-01T00:00:00+08:00`으로 설명합니다.
