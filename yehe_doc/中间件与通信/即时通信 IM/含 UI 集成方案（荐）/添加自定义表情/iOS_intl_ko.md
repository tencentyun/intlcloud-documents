[](id:overview)

## 개요

TUIChat 이모티콘 패널에는 몇 가지 작은 이모티콘이 내장되어 있습니다. 필요에 따라 사용자 지정 이모티콘을 추가할 수도 있습니다. 이 문서는 사용자 지정 이모티콘 추가에 중점을 둡니다.

<table style="text-align:center;vertical-align:middle;width:1000px">
  <tr>
    <th style="text-align:center;" width="200px">작은 이모티콘 패널 내장<br></th>
    <th style="text-align:center;" width="200px">사용자 지정 이모티콘 패널<br></th>
  </tr>
  <tr>
    <td style="text-align:center;"><img style="width:200px" src="https://im.sdk.cloud.tencent.cn/tools/resource/custom_face/ios/1.PNG"  />    </td>
    <td style="text-align:center;"><img style="width:200px" src="https://im.sdk.cloud.tencent.cn/tools/resource/custom_face/ios/2.PNG"  />     </td>
	 </tr>
</table>


전체 이모티콘 패널은 아래 그림과 같이 두 부분으로 구성됩니다.

* 이모티콘 리소스 이미지 관리, 포함: 이모티콘 이미지 표시;
* 이모티콘 그룹 관리, 포함: 이모티콘 그룹 커버 이미지, 보내기 버튼.

<img src="https://im.sdk.cloud.tencent.cn/tools/resource/custom_face/ios/7.png" style="zoom:30%;" />





[](id:add)

## 사용자 지정 이모티콘 패키지 추가

사용자 지정 이모티콘 패키지를 추가하려면 다음 두 단계만 따라 구성하면 됩니다.

1. 이모티콘 리소스 준비
2. App 실행 시 이모티콘 로딩

TUIChat에는 이모티콘 전송 및 구문 분석 로직이 내장되어 있으며 사용자 지정 이모티콘의 멀티 단말 통신을 쉽게 실현할 수 있습니다.

다음으로, 아래 이미지와 같이 사용자 지정 이모티콘 ‘programer’를 예로 들어 사용자 지정 이모티콘 패키지를 추가하는 방법을 보여줍니다.

<img src="https://im.sdk.cloud.tencent.cn/tools/resource/custom_face/ios/3.png" style="zoom:25%;" />



[](id:add_prepare)

### 이모티콘 리소스 준비

이모티콘을 추가하기 전에 먼저 저작권이 있는 이모티콘 리소스 세트를 준비해야 합니다. 아래 이미지와 같이 이모티콘 사진만 bundle 파일로 패키징하면 됩니다.

<img src="https://im.sdk.cloud.tencent.cn/tools/resource/custom_face/ios/4.png" style="zoom:30%;" />



[](id:add_load)

### 이모티콘 패키지 로딩

아래 이미지와 같이 ‘programer’ 이모티콘 리소스가 포함된 사용자 지정 이모티콘 패키지 `CustomFaceResource.bundle`을 xcode 프로젝트로 드래그합니다. 그 다음 App이 실행될 때 로딩합니다.

<img src="https://im.sdk.cloud.tencent.cn/tools/resource/custom_face/ios/5.png" style="zoom:30%;" />



```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    app = self;
    // App 실행 시 이모티콘 리소스 로딩
    [self setupCustomSticker];    
    return YES;
}

- (void)setupCustomSticker {
    // 1 사용자 지정 이모티콘 패키지 bundle의 경로 가져오기
    NSString *customFaceBundlePath = [[NSBundle mainBundle] pathForResource:@"CustomFaceResource" ofType:@"bundle"];
    
    // 2 사용자 지정 이모티콘 그룹 로딩
    // 2.1 programer 이모티콘 리소스 이미지를 로딩하고 TUIFaceCellData로 구문 분석
    NSMutableArray<TUIFaceCellData *> *faceItems = [NSMutableArray array];
    for (int i = 0; i <= 17; i++) {
        TUIFaceCellData *data = [[TUIFaceCellData alloc] init];
        // 이모티콘 리소스 이미지의 파일명(확장자 없음), 멀티 단말 통신에 사용(멀티 단말 통신시 파일명이 일관되어야 함)
        data.name = [NSString stringWithFormat:@"yz%02d", i];
        // 로컬 표시에 사용되는 이모티콘 리소스 이미지의 경로
        data.path = [customFaceBundlePath stringByAppendingPathComponent:[NSString stringWithFormat:@"programer/%@", data.name]];
        [faceItems addObject:data];
    }
    // 2.2 programer 이모티콘 그룹을 생성하고, TUIFaceGroup으로 구문 분석
    TUIFaceGroup *programGroup = [[TUIFaceGroup alloc] init];
    // 이모티콘 패널에서 현재 이모티콘 그룹의 일련번호를 식별하여 멀티 단말 통신에 사용(멀티 단말 통신 시 이모티콘 name과 함께 상대 단말에서 해당 아미지 검색)
    // groupIndex는 0부터 시작한다는 점에 유의해야 하며, 이모티콘 패널에서 현재 이모티콘 패키지의 실제 위치 식별(내장 이모티콘 그룹 기본값은 0)
    programGroup.groupIndex = 1;
    // 사용자 지정 이모티콘 bundle에 있는 현재 이모티콘 패키지의 루트 경로
    programGroup.groupPath = [customFaceBundlePath stringByAppendingPathComponent:@"programer/"];
    // 현재 이모티콘 패키지의 이모티콘 리소스
    programGroup.faces = faceItems;
    // 현재 이모티콘 패키지의 레이아웃
    programGroup.rowCount = 2;
    programGroup.itemCountPerRow = 5;
    // 현재 이모티콘 패키지의 커버 이미지 경로(확장자 없음)
    programGroup.menuPath = [customFaceBundlePath stringByAppendingPathComponent:@"programer/menu"];
    
    // 3 이모티콘 패널에 program 이모티콘 그룹 추가
    [TUIConfig.defaultConfig appendFaceGroup:programGroup];
}
```



[](id:add_sync)

### 멀티 단말 통신

TUIChat에는 이모티콘 패키지 전송 및 구문 분석 로직이 내장되어 있으므로 플랫폼 간에 다음 두 속성만 일관되게 유지하면 됩니다.

* 이모티콘 패키지에 있는 이미지의 파일명은 동일하며, App이 이모티콘 패키지 로딩 시 `TUIFaceCellData`로 구문 분석하는 `name` 필드 값은 멀티 단말에서 일관되어야 합니다.
* 이모티콘 패키지는 이모티콘 패널에서 동일한 순서로 표시되며, App이 이모티콘 패키지 로딩 시 `TUIFaceGroup`으로 구문 분석되는 `groupIndex` 필드의 값은 멀티 단말에서 일관되어야 합니다.

상기 두 정보가 일치하면 TUIChat의 내장 이모티콘 패키지 전송 로직은 이모티콘 파일 이름과 소속 이모티콘 패키지 인덱스 정보를 다른 단말로 전송하여 멀티 단말 통신을 실현합니다.

groupIndex는 0부터 시작한다는 점에 유의해야 하며, 이모티콘 패널에서 현재 이모티콘 패키지의 실제 위치 식별합니다(내장 이모티콘 그룹 기본값은 0).

<img src="https://im.sdk.cloud.tencent.cn/tools/resource/custom_face/ios/9.png" style="zoom:40%;" />





[](id:advance_config)

## 이모티콘 패널 고급 설정

[](id:advance_config_order)

### 이모티콘 패널 순서 조정

TUIChat의 이모티콘 패널은 이모티콘 그룹의 순서 조정을 지원하므로 실제 순서에 따라 `TUIConfig`의 `-appendFaceGroup:` 메소드를 호출하기만 하면 됩니다.

내장된 이모티콘 그룹을 사용자 지정 이모티콘 뒤로 조정하려면 다음과 같이 하십시오.

* 현재 이모티콘 패널에 내장된 이모티콘 그룹 `TUIConfig.defaultConfig.faceGroups`를 가져옵니다.
* 재정렬;
* 정렬된 이모티콘 그룹 목록을 이모티콘 패널에 할당합니다.

```
- (void)setupCustomSticker {
    // 1 사용자 지정 이모티콘 패키지 bundle의 경로 가져오기
    NSString *customFaceBundlePath = [[NSBundle mainBundle] pathForResource:@"CustomFaceResource" ofType:@"bundle"];
    
    // 2 사용자 지정 이모티콘 그룹 로딩
    // 2.1 programer 이모티콘 리소스 이미지를 로딩하고 TUIFaceCellData로 구문 분석
    NSMutableArray<TUIFaceCellData *> *faceItems = [NSMutableArray array];
    for (int i = 0; i <= 17; i++) {
        TUIFaceCellData *data = [[TUIFaceCellData alloc] init];
        // 이모티콘 리소스 이미지의 파일명(확장자 없음), 멀티 단말 통신에 사용(멀티 단말 통신시 파일명이 일관되어야 함)
        data.name = [NSString stringWithFormat:@"yz%02d", i];
        // 로컬 표시에 사용되는 이모티콘 리소스 이미지의 경로
        data.path = [customFaceBundlePath stringByAppendingPathComponent:[NSString stringWithFormat:@"programer/%@", data.name]];
        [faceItems addObject:data];
    }
    // 2.2 programer 이모티콘 그룹을 생성하고, TUIFaceGroup으로 구문 분석
    TUIFaceGroup *programGroup = [[TUIFaceGroup alloc] init];
    // 이모티콘 패널에서 현재 이모티콘 그룹의 일련번호를 식별하여 멀티 단말 통신에 사용(멀티 단말 통신 시 이모티콘 name과 함께 상대 단말에서 해당 아미지 검색)
    // groupIndex는 0부터 시작한다는 점에 유의해야 하며, 이모티콘 패널에서 현재 이모티콘 패키지의 실제 위치 식별(내장 이모티콘 그룹 기본값은 0)
    programGroup.groupIndex = 0;
    // 사용자 지정 이모티콘 bundle에 있는 현재 이모티콘 패키지의 루트 경로
    programGroup.groupPath = [customFaceBundlePath stringByAppendingPathComponent:@"programer/"];
    // 현재 이모티콘 패키지의 이모티콘 리소스
    programGroup.faces = faceItems;
    // 현재 이모티콘 패키지의 레이아웃
    programGroup.rowCount = 2;
    programGroup.itemCountPerRow = 5;
    // 현재 이모티콘 패키지의 커버 이미지 경로(확장자 없음)
    programGroup.menuPath = [customFaceBundlePath stringByAppendingPathComponent:@"programer/menu"];
    
    // 3 이모티콘 패널 맨 앞에 programer 이모티콘 그룹 추가
    // 3.1 내장 이모티콘 그룹 가져오기
    NSMutableArray *faceGroupsMenu = [NSMutableArray arrayWithArray:TUIConfig.defaultConfig.faceGroups];
    // 3.2 이모티콘 그룹 맨 앞에 programer 추가
    [faceGroupsMenu insertObject:programGroup atIndex:0];
    // 3.3 이모티콘 패널 재할당
    TUIConfig.defaultConfig.faceGroups = faceGroupsMenu;
    
    // 4 내장된 이모티콘의 순서를 변경하지 않으려면 순서대로 추가하면 됩니다.
    // [TUIConfig.defaultConfig appendFaceGroup:programGroup];

    // groupIndex가 실제 순서와 일치하는지 확인해야 합니다
    // 현재 위치를 직접 읽고 복사할 수 있습니다
    programGroup.groupIndex = [TUIConfig.defaultConfig.faceGroups indexOfObject:programGroup];
}
```

> ?
>
> 이모티콘 패키지 멀티 단말 통신은 이모티콘 이미지의 이름과 이모티콘 그룹이 있는 패널의 순서에 의존하기 때문에 로컬 순서를 조정한 후에는 groupIndex와 실제 순서가 일치하도록 하여 각 단말이 쉽게 통신할 수 있도록 해야 합니다.





[](id:advance_config_cover)

### 이모티콘 그룹의 커버 수정

사용자 지정 이모티콘 그룹 로딩 시 `TUIFaceGroup`의 `menuPath` 속성에 커버 이미지의 경로(@2x.png 확장자 없음)를 설정하여 이모티콘 그룹의 커버를 사용자 지정할 수 있습니다.

예를 들어 "programer" 이모티콘 그룹의 `menu@2x.png` 이미지를 커버 이미지로 사용합니다.

```
- (void)setupCustomSticker {
    ....
 		
    // 2.2 programer 이모티콘 그룹을 생성하고, TUIFaceGroup으로 구문 분석
    TUIFaceGroup *programGroup = [[TUIFaceGroup alloc] init];
    ....
    // 현재 이모티콘 패키지의 커버 이미지 경로(확장자 없음)
    programGroup.menuPath = [customFaceBundlePath stringByAppendingPathComponent:@"programer/menu"];
    ....
    
    ....
}
```





[](id:advance_config_style)

### 이모티콘 이미지의 레이아웃 조정

현재 TUIChat 이모티콘 패널은 이모티콘 이미지의 레이아웃을 위해 다음 두 가지 양식을 지원합니다.

* rowCount, 현재 이모티콘 그룹 내 이미지 표시의 행 수;
* itemCountPerRow, 각 행에 표시되는 이모티콘 이미지의 개수입니다.

예를 들어 ‘programer’ 이모티콘 그룹의 이모티콘 이미지 배열을 조정하는 규칙은 페이지당 2행, 한 행당 최대 5장의 이미지입니다.

```
- (void)setupCustomSticker {
    ...
 		
    // 2.2 programer 이모티콘 그룹을 생성하고, TUIFaceGroup으로 구문 분석
    TUIFaceGroup *programGroup = [[TUIFaceGroup alloc] init];
    // 현재 이모티콘 패키지의 레이아웃
    programGroup.rowCount = 2;
    programGroup.itemCountPerRow = 5;
    
    ...
}
```

<img src="https://im.sdk.cloud.tencent.cn/tools/resource/custom_face/ios/10.jpg" style="zoom:33%;" />



[](id:render)

## 이모티콘 패키지 렌더링 원리

TUIChat에는 이모티콘을 전송하고 렌더링하는 메커니즘이 내장되어 있으므로 이 부분에 주의를 기울일 필요가 없습니다.

소스 코드를 수정하거나 사용자 지정 이모티콘 콘텐츠를 인코딩하여 직접 전송해야 하는 경우 이 섹션을 참고하십시오.

[](id:render_send)

### 이모티콘 전송

TUIChat의 이모티콘 패널은 UICollectionView로 구성되어 있으며, 각각의 이모티콘 이미지를 클릭하면 `TUIInputController`의 `-faceView:didSelectItemAtIndexPath:` 메소드가 트리거되며, 선택한 이모티콘 이름과 해당 이모티콘 그룹의 패널 내 인덱스 정보가 콜백됩니다.

콜백에서 두 단계로 이모티콘을 보낼 수 있습니다.

- 이모티콘 이름과 이모티콘 그룹 인덱스로 이모티콘 메시지를 생성합니다.
- TUIChat의 메소드를 호출하여 이모티콘 메시지를 보냅니다.

```
- (void)faceView:(TUIFaceView *)faceView didSelectItemAtIndexPath:(NSIndexPath *)indexPath
{
    TUIFaceGroup *group = [TUIConfig defaultConfig].faceGroups[indexPath.section];
    TUIFaceCellData *face = group.faces[indexPath.row];
    if(indexPath.section == 0){
        // 내장된 작은 이모티콘인 경우, 작은 이모티콘을 입력란에 표시해야 합니다
        [_inputBar addEmoji:face];
    }
    else{
        // 사용자 지정 이모티콘인 경우, 상대방에게 직접 전송
        if (face.name) {
            // 이모티콘 메시지 생성
            V2TIMMessage *message = [[V2TIMManager sharedInstance] createFaceMessage:group.groupIndex data:[face.name dataUsingEncoding:NSUTF8StringEncoding]];
            // 상대방에게 전송
            if(_delegate && [_delegate respondsToSelector:@selector(inputController:didSendMessage:)]){
                [_delegate inputController:self didSendMessage:message];
            }
        }
    }
}
```



[](id:render_parse)

### 이모티콘을 구문 분석하고 렌더링

상대방으로부터 이모티콘 메시지를 수신한 후 TUIChat은 `TUIFaceMessageCellData`의 `- getCellData:` 메소드를 트리거하고 이모티콘을 표시하기 위해 이모티콘 메시지를 `TUIFaceMessageCellData`로 구문 분석합니다.

TUIChat은 렌더링을 위해 구문 분석된 'TUIMessageCellData'를 'TUIFaceMessageCell'에 할당합니다.

전체 TUIChat의 메시지 구문 분석 프로세스는 [통합(UI 포함) - 사용자 지정 메시지 추가](https://intl.cloud.tencent.com/document/product/1047/50043)를 참고하십시오.

```
+ (TUIMessageCellData *)getCellData:(V2TIMMessage *)message{
    // 메시지 수신 후 이모티콘 정보 가져오기
    V2TIMFaceElem *elem = message.faceElem;
    
    // 이모티콘 표시를 위한 TUIFaceMessageCellData 생성
    TUIFaceMessageCellData *faceData = [[TUIFaceMessageCellData alloc] initWithDirection:(message.isSelf ? MsgDirectionOutgoing : MsgDirectionIncoming)];
    // 이모티콘 패널에서 현재 이모티콘 그룹의 순서 가져오기
    faceData.groupIndex = elem.index;
    // 이모티콘 이미지 파일명 가져오기
    faceData.faceName = [[NSString alloc] initWithData:elem.data encoding:NSUTF8StringEncoding];
    // 이모티콘 이미지의 이름과 이모티콘 그룹에 따라 로컬 이모티콘 패키지에서 이모티콘 이미지의 특정 경로 가져오기
    for (TUIFaceGroup *group in [TUIConfig defaultConfig].faceGroups) {
        if(group.groupIndex == faceData.groupIndex){
            NSString *path = [group.groupPath stringByAppendingPathComponent:faceData.faceName];
            faceData.path = path;
            break;
        }
    }
    faceData.reuseId = TFaceMessageCell_ReuseId;
    return faceData;
}
```
