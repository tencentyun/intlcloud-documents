## 기본 구조

수명 주기 구성은 XML 설명 방법으로 하나 또는 여러 수명 주기 규칙을 구성할 수 있습니다. 기본 구조는 아래와 같습니다.

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

모든 규칙은 아래와 같은 내용을 포함합니다.

- ID(옵션): 사용자가 지정할 수 있는 설명 규칙의 내용입니다.
- Status: 규칙의 사용 가능(Enabled) 또는 사용 금지(Disabled) 상태를 선택할 수 있습니다.
- Filter: 실행해야 할 객체의 필터링 조건을 지정하는 데에 사용됩니다.
- 작업: 위의 설명에 부합한 객체에 실행해야 할 작업입니다.
- 시간: 마지막 수정 시간에 따라 일수 `Days`를 지정하거나 구체적인 날짜 `Date`를 지정하여 이 날짜전에 객체를 작업해야 합니다.

## 규칙 설명

### Filter 요소

#### 버킷에서 모든 객체를 대상으로

빈 필터링 조건을 지정할 경우 버킷에서 모든 객체에 적용됩니다.

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

#### 지정한 객체 키 접두사를 대상으로

객체 접두사를 지정할 경우 접두사 설명에 부합한 일부 객체 그룹에 대해 조작을 실행할 수 있습니다. 예를 들어, `logs/`를 접두사로 하는 모든 객체를 설정할 수 있습니다.

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

#### 지정한 객체 태그를 대상으로

객체 태그에 부합한 `key`와 `value`를 필터링 조건으로 지정하여 지정한 태그 객체에 대해 조작을 실행합니다. 예를 들어 태그의 `key=type`와 `value=image`를 필터링 조건으로 하는 객체를 설정할 수 있습니다.

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

#### 여러 개 필터링 조건의 동시 사용

COS는 `AND`의 로직을 통한 여러 개 필터링 조건의 동시 사용을 지원합니다. 예를 들어, `logs/`를 접두사로 하고 객체 태그의 `key=type`와 `value=image`를 필터링 조건으로 하는 객체를 설정할 수 있습니다.

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

수명 주기 규칙에서 조건에 부합하는 한 그룹 객체에 하나 또는 여러 작업을 실행할 수 있습니다.

#### 전환 작업

Transition 작업을 지정하면 객체의 스토리지 클래스를 전환할 수 있습니다. 버킷에서 버전 제어가 활성화되었다면 현재 버전에 대해서만 조작을 실행합니다. 가장 짧은 Transition 설정 시간은 0일입니다. 예를 들어, 30일 후 보관 스토리지로의 전환을 설정할 수 있습니다.

```xml
<Transition>
	<StorageClass>ARCHIVE</StorageClass>
    <Days>30</Days>
</Transition>
```

#### 만료 삭제

Expiration 작업을 지정하면 규칙에 부합하는 객체에 대해 만료 삭제 작업을 실행할 수 있습니다. 버킷에서 버전 제어가 활성화된 적이 없을 경우 객체는 영구적으로 삭제됩니다. 버킷에서 버전 제어가 활성화된 적이 있을 경우 만료된 객체에 **하나의 DeleteMarker 마크를 추가**하며 현재 버전으로 설정합니다. 예를 들어, 30일 후 객체를 삭제하도록 설정할 수 있습니다.

```xml
<Expiration>
	<Days>30</Days>
</Expiration>
```

#### 미완료 멀티파트 업로드

AbortIncompleteMultipartUpload 작업을 지정하면 멀티파트 업로드의 지정한 UploadId 태스크를 일정한 시간으로 유지한 후에 삭제되며, 업로드 재개 또는 인덱스 가능한 특성을 더 이상 제공하지 않습니다. 예를 들어, 7일 후 미완료 멀티파트 업로드 태스크를 삭제하도록 설정할 수 있습니다.

```xml
<AbortIncompleteMultipartUpload>
	<Days>7</Days>
</AbortIncompleteMultipartUpload>
```

#### 현재 버전이 아닌 객체

버전 제어가 활성화된 버킷에서 전환은 최신 버전에 대해서만 실행되며 만료 조작은 마크만 추가합니다. 그러므로 COS는 현재 버전이 아닌 푸시에 아래와 같은 조작을 제공합니다.

NoncurrentVersionTransition 작업을 지정하면 현재 버전이 아닌 객체가 지정한 시간에 다른 스토리지 클래스로 전환할 수 있습니다. 예를 들어, 이전 버전이 30일 후 보관 스토리지로 분류되도록 설정할 수 있습니다.

```xml
<NoncurrentVersionTransition>
	<StorageClass>ARCHIVE</StorageClass>
    <Days>30</Days>
</NoncurrentVersionTransition>
```

NoncurrentVersionExpiration 작업을 지정하면 현재 버전이 아닌 객체가 지정한 시간에 만료 삭제될 수 있습니다. 예를 들어, 이전 버전이 30일 후 삭제되도록 설정할 수 있습니다.

```xml
<NoncurrentVersionExpiration>
	<Days>30</Days>
</NoncurrentVersionExpiration>
```

ExpiredObjectDeleteMarker 작업을 지정하면 객체 키의 모든 이전 버전은 삭제되고 최신 객체 버전이 삭제 마크(DeleteMarker)일 경우 이 삭제 마크를 제거할 수 있습니다. 예를 들어, 31일 후 만료 객체의 삭제 마크를 제거하도록 설정할 수 있습니다.

```xml
<ExpiredObjectDeleteMarker>
	<Days>31</Days>
</ExpiredObjectDeleteMarker>
```

### 시간 요소

#### 일수별 계산

`Days`로 일수를 지정하면 객체의 마지막 수정 시간으로 계산됩니다.
예를 들어, 하나의 객체를 0일 후 보관 스토리지 클래스로 전환하도록 설정할 경우 이 객체는 2018-01-01 23:55:00 GMT+8에 업로드되고 2018-01-02 00:00:00 GMT+8부터 스토리지 클래스 전환의 처리 대기열에 들어가고 늦어도 2018-01-02 23:59:59 GMT+8전까지 전환을 완료할 수 있습니다.
예를 들어, 하나의 객체를 1일 후 만료 삭제로 전환하도록 설정할 경우 이 객체는 2018-01-01 23:55:00 GMT+8에 업로드되고 2018-01-03 00:00:00 GMT+8부터 만료 삭제의 처리 대기열에 들어가고 늦어도 2018-01-03 23:59:59 GMT+8전까지 삭제를 완료할 수 있습니다.

#### 지정한 날짜에 따름

`Date`로 날짜를 지정하면 특정 날짜에 도달하면 필터링 조건에 부합한는 모든 객체에 조작을 실행합니다. 현재 GMT+8 시간대, 0시로 설정한 ISO8601 형식의 시간 지정만 지원합니다.
예를 들어, 2018년 1월 1일은 `2018-01-01T00:00:00+08:00`로 설명됩니다.
