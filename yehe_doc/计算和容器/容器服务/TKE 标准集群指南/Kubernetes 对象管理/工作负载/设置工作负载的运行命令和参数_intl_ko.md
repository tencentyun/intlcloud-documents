## 개요

워크로드를 생성할 때 이미지는 포드의 컨테이너 프로세스를 지정하는 데 사용됩니다. 기본적으로 이미지는 기본 명령을 실행합니다. 특정 명령을 실행하거나 이미지의 기본값을 다시 쓰려면 다음 세 가지 설정을 사용해야 합니다.
- 작업 디렉터리( workingDir): 현재 작업 디렉터리를 지정합니다.
- 명령 실행( command ): 이미지가 실행하는 실제 명령을 제어합니다.
- 명령 인수( args ): 실행 중인 명령에 전달되는 매개변수입니다.

## 작업 디렉터리

WorkingDir은 현재 작업 디렉터리를 지정합니다. 존재하지 않는 경우 작업 디렉터리가 자동으로 생성됩니다. 이 매개변수를 지정하지 않으면 컨테이너 런타임의 기본값이 사용됩니다. 이미지나 콘솔에 WORKDIR이 지정되지 않은 경우 workingDir의 기본값은 ‘/’입니다.

## 명령 및 매개변수 사용법

Tencent Cloud TKE에 docker run 명령을 적용하는 방법에 대한 자세한 내용은 [docker run Parameter Adaptation](https://intl.cloud.tencent.com/document/product/457/9883)을 참고하십시오.
 
Docker 이미지에는 이미지 정보 저장소와 관련된 메타데이터가 포함됩니다. 컨테이너에 대한 명령이나 매개변수를 지정하지 않으면 컨테이너는 이미지가 생성될 때 사용되는 기본 명령 및 매개변수를 실행할 수 있습니다. 기본적으로 Docker의 ‘Entrypoint’ 및 ‘CMD’입니다. 자세한 내용은 Docker의 [Entrypoint](https://docs.docker.com/engine/reference/builder/#/entrypoint) 및 [CMD](https://docs.docker.com/engine/reference/builder/#/cmd)를 참고하십시오.
서비스를 생성할 때 컨테이너에 대한 실행 명령 및 매개변수를 입력하면 이미지가 생성될 때 TKE가 기본 명령(즉, ‘Entrypoint’ 및 ‘CMD’)을 재정의합니다. 규칙은 다음과 같습니다.

| 이미지 Entrypoint |이미지 CMD|컨테이너의 실행 명령|컨테이너의 실행 매개변수| 최종 실행|
| :-------- | :--------| :------ | :-------- | :------ |
| [ls]   | [/home]|  미설정  |미설정    |[ls / home]  |
| [ls]   | [/home]|  [cd]  |미설정    |[cd]        |
| [ls]   | [/home]|  미설정  |[/data] |[ls / data]  |
| [ls]   | [/home]|  [cd]  |[/data] |[cd / data]  |

> 
>- Docker entrypoint는 TKE 콘솔의 실행 명령에 해당하고 Docker run의 매개변수 CMD는 TKE 콘솔의 실행 매개변수에 해당합니다. 여러 매개변수가 있는 경우 각 매개변수가 자체 행에 있는 TKE의 매개변수 필드에 입력하십시오.
>- [TKE Console](https://console.cloud.tencent.com/tke2)을 사용하여 컨테이너에 대해 실행 중인 명령 및 매개변수를 설정하는 방법에 대한 예시는 [Commands and Args](https://intl.cloud.tencent.com/document/product/457/9883#command-.E5.92.8C-args)를 참고하십시오. 
