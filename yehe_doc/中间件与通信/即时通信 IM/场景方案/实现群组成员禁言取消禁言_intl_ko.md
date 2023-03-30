- - - - 그룹의 한 구성원 또는 모든 구성원을 음소거 처리하고 음소거 기간을 설정할 수 있습니다. 음소거 기간 동안 음소거된 구성원은 해당 그룹에서 메시지를 보낼 수 없습니다. 이 작업은 현재 그룹에서만 유효합니다. 음소거가 해제되지 않는 한, 음소거 기간 동안 음소거된 구성원은 해당 그룹 퇴장 후 재입장하여도 음소거 상태를 유지합니다. 
        본문에서는 주로 Web 및 미니프로그램 SDK에서 그룹 구성원을 음소거/음소거 해제하는 방법을 소개합니다.
  
        ## 사용 제한
  
        - 그룹 유형 제한
         <table>
        <tr>
        <th width="25%">업무 그룹(Work 또는 이전 버전의 Private）</th>
        <th width="25%">공개 그룹(Public)</th>
        <th width="25%">회의 그룹(Meeting 또는 이전 버전의 ChatRoom)</th>
        <th width="25%">라이브 방송 그룹(AvChatRoom)</th>
        </tr>
        <tr>
        <td><strong>미지원</strong></td>
        <td>지원</td>
        <td>지원</td>
        <td>지원</td>
        </tr>
        </table>
  
        - 구성원 역할 제한
        <table>
        <tr>
        <th width="25%">구성원 역할</th>
        <th>권한</th>
        </tr>
        <tr>
        <td>App 관리자</td>
        <td>SDKAppID에 속한 모든 그룹의 모든 구성원에 대한 음소거/음소거 해제 작업</td>
        </tr>
        <tr>
        <td>그룹 소유자</td>
        <td>그룹 내 관리자 및 일반 구성원에 대한 음소거/음소거 해제 작업</td>
        </tr>
        <tr>
        <td>그룹 관리자</td>
        <td>그룹 내 일반 구성원에 대한 음소거/음소거 해제 작업</td>
        </tr>
        <tr>
        <td>일반 구성원</td>
        <td>음소거 권한 없음</td>
        </tr>
        </table>
  
        ## 작업 절차
  
        ### 1단계: 작업 권한 확인
        1. [getGroupProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupProfile) 인터페이스를 호출하여 그룹 유형을 확인하고 음소거/음소거 해제 작업 지원 여부를 확인합니다.
         >!그룹 유형이 Private 또는 Work(업무 그룹)인 경우 음소거가 지원되지 않습니다.
         >
        2. [getGroupMemberProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberProfile) 인터페이스를 호출하여 userID의 그룹 구성원 역할을 확인하고 음소거/음소거 해제 권한을 확인합니다.
  
        ### 2단계: 그룹 구성원 음소거/음소거 해제
        #### 단일 사용자 음소거/음소거 해제
        App 관리자, 그룹 소유자 또는 그룹 관리자는 [setGroupMemberMuteTime](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setGroupMemberMuteTime) 인터페이스를 호출하여 그룹 내 구성원에 대해 음소거/음소거 해제할 수 있습니다. 1회 호출당 1명의 그룹 구성원의 음소거/음소거 해제가 지원됩니다.
        요청 매개변수는 다음 표와 같습니다.
  
        | 이름     | 유형   | 설명                                 |
        | -------- | ------ | ------------------------------------ |
        | groupID  | String | 그룹 ID                              |
        | userID   | String | 그룹 구성원 ID                       |
        | muteTime | Number | 음소거 시간. 단위:초. 0: 음소거 해제 |
  
        요청 예시는 다음과 같습니다.
        ```javascript
        let promise = tim.setGroupMemberMuteTime({
          groupID: 'group1',
          userID: 'user1',
          muteTime: 1000
        });
        ```
  
        #### 전체 구성원 음소거/음소거 해제
        >!이 기능을 사용하려면 SDK를 2.6.2 또는 그 이후 버전으로 업그레이드해야 합니다. 전체 음소거 또는 전체 음소거 해제는 현재 그룹 알림 메시지가 발송되지 않습니다.
  
        App 관리자 또는 그룹 소유자는 [updateGroupProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateGroupProfile) 인터페이스를 호출하여 전체 그룹 관리자 및 일반 구성원 음소거/음소거 해제를 진행할 수 있습니다.
        요청 매개변수는 다음 표와 같습니다.
  
        | 이름           | 유형    | 설명                                                    |
        | -------------- | ------- | ------------------------------------------------------- |
        | groupID        | String  | 그룹 ID                                                 |
        | muteAllMembers | Boolean | 음소거 설정. true: 전원 음소거, false: 전원 음소거 해제 |
  
        요청 예시는 다음과 같습니다.
        ```javascript
        let promise = tim.updateGroupProfile({
          groupID: 'group1',
          muteAllMembers：true, // true: 전원 음소거, false: 전원 음소거 해제
        });
        promise.then(function(imResponse) {
          console.log(imResponse.data.group) // 수정 완료 후 그룹 상세 정보
        }).catch(function(imError) {
          console.warn('updateGroupProfile error:', imError); // 그룹 정보 수정 실패 관련 정보
        });
        ```
  
        
  
        ### 3단계: TIM.EVENT.MESSAGE_RECEIVED 이벤트 모니터링 및 처리
        음소거된 그룹 구성원은 음소거되었음을 나타내는 [그룹 알림 메시지](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupTipPayload)를 받게 됩니다. event.data를 순회하여 관련 데이터를 가져와 인터페이스에 렌더링할 수 있습니다.
        >?음소거/음소거 해제 관련 알림을 받은 후, disable/enable 입력창 또는 입력 구역의 상태를 구현할 것을 권장합니다.
  
        <pre>
        tim.on(TIM.EVENT.MESSAGE_RECEIVED, function(event) {
          // 1:1채팅, 그룹 채팅, 그룹 알림, 그룹 시스템 알림 등의 새로운 메시지 수신 시, event.data를 순회하여 메시지 리스트 데이터를 가져와 페이지에 렌더링할 수 있습니다.
          // event.name - TIM.EVENT.MESSAGE_RECEIVED
          // event.data - Message 객체를 저장하는 배열 - [Message]
          const length = event.data.length;
          let message;
          for (let i = 0; i < length; i++) {
            message = event.data[i];
            switch (message.type) {
              // 사용자 A 음소거 처리. 사용자 A는 음소거 그룹 알림 메시지를 수신합니다.
              case TIM.TYPES.MSG_GRP_TIP:
                this._handleGroupTip(message);
                break;
              case TIM.TYPES.MSG_TEXT: // 텍스트 메시지. 더 많은 메시지 유형은 <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html">Message를 참고하십시오.</a>
                break;
              default:
                break;
            }
          }
        });
  
        _handleGroupTip(message) {
          switch (message.payload.operationType) {
            case TIM.TYPES.GRP_TIP_MBR_PROFILE_UPDATED: // 그룹 구성원 정보 변경(예: 음소거됨).
              const memberList = message.payload.memberList;
              for (let member of memberList) {
                console.log(`${member.userID} 음소거됨${member.muteTime}초`);
              }
              break;
            case TIM.TYPES.GRP_TIP_MBR_JOIN: // 그룹에 참여한 구성원이 있음.
              break;
            case TIM.TYPES.GRP_TIP_MBR_QUIT: // 그룹에서 퇴장한 구성원이 있음.
              break;
            case TIM.TYPES.GRP_TIP_MBR_KICKED_OUT: // 그룹에서 내보내기 당한 구성원이 있음.
              break;
            case TIM.TYPES.GRP_TIP_GRP_PROFILE_UPDATED: // 그룹 정보가 변경됨.
              break;
        	default:
        	  break;
          }
        }
        </pre>
  
        ### 4단계: 음소거 상태 확인
  
        - 2.6.2 및 이후 버전 SDK 버전은 [getGroupMemberList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberList) 인터페이스를 호출하여 그룹 구성원의 음소거 기한 타임스탬프(muteUntil)를 풀링할 수 있으며, 이 값을 기준으로 그룹 구성원의 음소거 여부와 남은 음소거 시간을 판단할 수 있습니다. 음소거가 해제된 후 해당 그룹 구성원의 GroupMember.muteUntil * 1000 <= Date.now() 계산 공식은 유효합니다.
        ```javascript
        // v2.6.2부터 getGroupMemberList 인터페이스는 그룹 구성원의 음소거 기한 타임스탬프 풀링을 지원합니다.
        let promise = tim.getGroupMemberList({ groupID: 'group1', count: 30, offset:0 }); // 0부터 그룹 구성원 30명 풀링.
        promise.then(function(imResponse) {
          console.log(imResponse.data.memberList); // 그룹 구성원 리스트.
          for (let groupMember of imResponse.data.memberList) {
            if (groupMember.muteUntil * 1000  > Date.now()) {
              console.log(`${groupMember.userID} 음소거 중`);
            } else {
              console.log(`${groupMember.userID} 음소거 되지 않음`);
            }
          }
        }).catch(function(imError) {
          console.warn('getGroupMemberProfile error:', imError);
        });
        ```
        - 2.6.2 이전 버전 SDK의 경우, [getGroupMemberProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberProfile) 인터페이스를 호출하여 그룹 구성원의 음소거 기한 타임스탬프(muteUntil) 등 상세 정보를 쿼리할 수 있습니다.
