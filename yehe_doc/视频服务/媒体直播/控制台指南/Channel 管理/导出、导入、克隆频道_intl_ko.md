StreamLive를 사용하면 채널 구성 파일을 가져오거나 내보내고 기존 채널을 복제할 수 있습니다.

## 채널 내보내기
**Channel Management** 페이지에는 생성된 채널과 해당 상태가 표시됩니다. 작업 열에서 **Export**를 클릭하여 채널 구성의 json 파일을 내보냅니다.
![](https://qcloudimg.tencent-cloud.cn/raw/df66d2e71c1dc9f54e3753eecbf1e12b.png)
![](https://qcloudimg.tencent-cloud.cn/raw/6c6402290ae2b5b9bfc987917f035941.png)

## 채널 가져오기
**Channel Management** 페이지에서 **Create Channel**을 클릭한 다음 **Import Configuration**을 클릭하고 가져올 json 파일을 선택합니다. 그런 다음 가져온 채널을 편집하고 구성을 저장할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7bf6af58535a57e11a9f92339b8e5e34.png)
가져오기 기능을 사용하면 채널을 빠르게 구성할 수 있습니다. 콘솔은 선택한 json 파일에 따라 **Basic Information** 및 **Output Group Setting**의 정보를 자동으로 채우지만 파일의 **Input Setting** 정보는 무시합니다. 바인딩할 Input을 선택해야 합니다.

>! 채널 편집 시 새로운 구성 파일을 가져오는 경우, 기존 채널 구성 정보는 덮어쓰기 됩니다.

## 채널 복제
채널 복제는 기본적으로 빠른 채널 내보내기 및 가져오기 프로세스입니다. **Channel Management** 페이지의 **Operation** 열에서 **Clone**을 클릭합니다. 새 채널의 구성 페이지로 이동합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/27f233ac35cc1bd1316901ac7457ffa9.png)
StreamLive는 복제된 채널에 따라 채널 구성(**Input Setting** 제외)을 자동으로 완료합니다. 나머지 구성을 완료하고 제출하십시오.