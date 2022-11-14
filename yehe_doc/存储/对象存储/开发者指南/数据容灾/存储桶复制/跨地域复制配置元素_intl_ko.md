## 기본 구조

각 COS(Cloud Object Storage) 버킷에는 다음 기본 구조의 XML 언어로 구성 및 편집되는 하나의 리전 간 복제 규칙이 있을 수 있습니다.

```
<ReplicationConfiguration>
	<Role>qcs::cam::uin/[UIN]:uin/[Subaccount]</Role>
	<Rule>
        <Status></Status>
        <ID></ID>
        <Prefix></Prefix>
        <Destination>
            <Bucket>qcs::cos:[Region]::[Bucketname-Appid]</Bucket>
            <StorageClass></StorageClass>
        </Destination>
	</Rule>
	<Rule>
	...
	</Rule>
</ReplicationConfiguration>
```

여기서 `<Role>`은 리전 간 복제 개시자의 ID를 나타내고 `<Rule>`은 구성된 리전 간 복제 규칙을 나타냅니다. 각 규칙에는 다음이 포함됩니다.

- Status: 규칙의 활성화 Enable 또는 비활성화 Disable 여부를 나타냅니다.
- ID: 특정 Rule에 레이블을 지정하는 데 사용되는 이름입니다.
- Prefix: 중복될 수 없는 접두사 일치 정책을 나타냅니다. 그렇지 않으면 오류가 반환됩니다. 접두사가 비어 있으면 버킷의 모든 객체가 복제됩니다. 접두사에 값이 있으면 지정된 접두사 값을 가진 객체가 복제됩니다.
- Destination: 'Bucket' 및 'StorageClass' 요소를 포함한 대상 버킷 정보를 나타냅니다.
	1. Bcuket: 대상 버킷의 이름 및 리전입니다.
	2. StorageClass: 대상 버킷에 복제된 후 객체의 스토리지 클래스입니다.

## 규칙 설명

### 객체 복제 요소

#### 버킷의 모든 객체 복제

리전 간 복제 규칙이 버킷의 모든 객체를 복제하도록 빈 `<Prefix>`를 지정합니다.

```
<ReplicationConfiguration>
	<Role>qcs::cam::uin/[UIN]:uin/[Subaccount]</Role>
	<Rule>
        <Status></Status>
        <ID></ID>
        <Prefix></Prefix>
        <Destination>
            <Bucket>qcs::cos:[Region]::[Bucketname-Appid]</Bucket>
            <StorageClass></StorageClass>
        </Destination>
	</Rule>
</ReplicationConfiguration>
```

#### 버킷에서 지정된 접두사로 객체 복제

리전 간 복제 규칙이 지정된 접두사가 있는 객체에만 적용되도록 접두사를 지정합니다. 예를 들어 접두사 logs/를 사용하여 객체를 복제할 수 있습니다.

```
<ReplicationConfiguration>
	<Role>qcs::cam::uin/[UIN]:uin/[Subaccount]</Role>
	<Rule>
        <Status></Status>
        <ID></ID>
        <Prefix>logs</Prefix>
        <Destination>
            <Bucket>qcs::cos:[Region]::[Bucketname-Appid]</Bucket>
            <StorageClass></StorageClass>
        </Destination>
	</Rule>
</ReplicationConfiguration>
```

### 대상 버킷 요소

#### 대상 버킷 리전 및 이름

`<Bucket>` 매개변수를 수정하여 다른 리전의 버킷을 대상 버킷으로 지정할 수 있습니다. 원본 및 대상 버킷은 동일한 계정의 서로 다른 리전에 있어야 합니다.

```
<ReplicationConfiguration>
	<Role>qcs::cam::uin/[UIN]:uin/[Subaccount]</Role>
	<Rule>
        <Status></Status>
        <ID></ID>
        <Prefix></Prefix>
        <Destination>
            <Bucket>qcs::cos:cn-south::sevenyousouthtest-7319456</Bucket>
            <StorageClass></StorageClass>
        </Destination>
	</Rule>
</ReplicationConfiguration>
```

#### 대상 버킷의 객체 스토리지 클래스

`<StorageClass>` 매개변수를 수정하면 대상 버킷에 복제된 객체의 스토리지 클래스를 지정할 수 있습니다. 복사본은 기본적으로 소스 객체의 스토리지 클래스에 저장됩니다. COS는 현재 객체 복사본에 대해 STANDARD 및 STANDARD_IA의 두 가지 스토리지 클래스를 지원합니다. 사본을 ARCHIVE에 저장하려면 대상 버킷에서 라이프사이클을 활성화하여 객체 관리를 구현해야 합니다.

```
<ReplicationConfiguration>
	<Role>qcs::cam::uin/[UIN]:uin/[Subaccount]</Role>
	<Rule>
        <Status></Status>
        <ID></ID>
        <Prefix></Prefix>
        <Destination>
            <Bucket>qcs::cos:cn-south::sevenyousouthtest-7319456</Bucket>
            <StorageClass>Standard</StorageClass>
        </Destination>
	</Rule>
</ReplicationConfiguration>
```

