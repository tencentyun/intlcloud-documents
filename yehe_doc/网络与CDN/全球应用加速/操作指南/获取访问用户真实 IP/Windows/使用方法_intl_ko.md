## 데이터 구조와 함수 설명
### class ToaFetcher
주체 유형으로 TOA 가져오기와 릴리스 관리에 사용됩니다.

### InitUpToaFetcher
#### 함수 설명
해당 함수는 TOA fetcher를 초기화하는 데 사용됩니다.

bool InitUpToaFetcher(char *ncard_ip_str, char *svr_ip_str, u_short svr_port[], u_short svr_port_num, u_short cache_secs=TIMER_CACHE_SECS)

#### 입력 매개변수 설명
ncard_ip_str	”10.75.132.39”와 같은 네트워크 인터페이스의 IP 주소 문자열을 식별하는 데에 사용됩니다. 해당 ENI는 클라이언트와 통신하는 ENI입니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/b9af3663b55b043d5891dfc2baa42877.png)
vr_ip_str: ”10.75.132.39”와 같은 서버의 IP 주소 문자열로 TCP 트래픽을 필터링하는 데에 사용됩니다.
svr_port: 서버의 포트 리스트로 TCP 트래픽을 필터링하는 데에 사용되며 최대 3개, 최소 1개의 포트를 입력할 수 있습니다.
svr_port_num: 서버의 포트 개수입니다.
cache_secs: 캐시의 시간으로 단위는 초이고, 기본값은 15초입니다. 세부 정보는 toa_fetcher.h: TIMER_CACHE_SECS를 참조하십시오. 캐시 시간이 만료되면 해당 TOA를 더 이상 보관하지 않습니다.

#### 반환값
TRUE: 바이패스 스레드 획득하기 위한 TOA 작성이 성공했음을 나타냅니다.
FALSE: 바이패스 스레드 획득하기 위한 TOA 작성이 실패했음을 나타냅니다.

### FetchToaValue
#### 함수 설명
해당 함수는 TOA 값을 획득하는 데에 사용됩니다. tcp-syn 패킷이 상호작용되면 최대 1ms를 기다린 후에 TOA를 얻을 수 있습니다. 일반적으로 3방향 핸드 셰이크는 1ms 이상을 걸립니다.

bool FetchToaValue(u_long fake_client_ip_addr, u_short fake_client_port, u_long &real_client_ip_addr, u_short &real_client_port)

#### 입력 매개변수 설명
fake_client_ip_addr: 클라이언트의 허위 IP 주소로 네트워크 순서에 따라 저장되고 서버 accept 함수를 반환한 피어 주소에서 획득합니다.
fake_client_port: 클라이언트의 허위 포트 번호로 네트워크 순서에 따라 저장되고 서버 accept 함수를 반환한 피어 주소에서 획득합니다.
real_client_ip_addr: 클라이언트의 실제 IP 주소로 네트워크 순서에 따라 저장되고 TOA에서 획득할 수 있습니다.
real_client_port: 클라이언트의 실제 포트 번호로 네트워크 순서에 따라 저장되고 TOA에서 획득할 수 있습니다.

#### 반환값
TRUE: TOA 획득 성공
FALSE: TOA 획득 실패. 일반적으로 캐시 시간 초과로 TOA가 지워집니다.


### StopToaFetcher
#### 함수 설명
해당 함수는 TOA fetcher를 중단하는 데에 사용됩니다.

void StopToaFetcher()

#### 입력 매개변수 설명
없음.
#### 반환값
없음.

### GetFetcherStatus
#### 함수 설명
해당 함수는 Fetcher 상태를 획득하는 데에 사용됩니다.

int GetFetcherStatus()

#### 입력 매개변수 설명
없음.
#### 반환값
0: 초기 상태를 의미합니다. 인스턴스를 생성한 후, 초기 상태가 해당 상태에 처하게 되고, Fetcher 초기화 중에는 해당 상태가 변하지 않고 유지됩니다. 중간에 오류가 발생하면, -1을 반환하고 성공적으로 실행하면 1을 반환합니다.
-1: 이상 상태를 의미합니다.
1: 정상 실행을 의미합니다.

### FetchThreadHandler
#### 함수 설명
해당 함수는 TOA 바이패스 스레드 핸들을 획득하는 데에 사용됩니다.

HANDLE FetchThreadHandler()

 #### 입력 매개변수 설명
없음.
#### 반환값
TOA 바이패스 스레드 핸들은 ToaFetcher 인스턴스가 폐기되었을 때 이 핸들을 주동적으로 종료합니다.

### FetchErrorInfo
#### 함수 설명
해당 함수는 오류 코드를 획득하는 데에 사용됩니다.

bool FetchErrorInfo(int* err_code_ptr, char* err_msg_ptr)

#### 입력 매개변수 설명
err_code_ptr: 오류 코드를 가리키고 오류 코드를 반환하는 데 사용되는 정수 포인터입니다.
err_msg_ptr	: 적어도 50 바이트의 문자열 버퍼를 가리키고 오류 메시지를 반환하는 데 사용되는 문자 포인터입니다.

#### 반환값
TRUE: 획득이 정상입니다.
FALSE: 획득이 이상입니다.

## 오류 코드
| 오류 코드 | 오류 정보 | 설명 |
|---------|---------|---------|
| 0	       | Ok	| 정상 |
| -1001	|Exceed max server port number |	최대 포트 수를 초과하였습니다. CreateToaFetecherThread: svr_port_num을 검사하십시오. |
| -1002	| Invalid IP address	| 잘못된 IPv4 주소입니다. |
| -1003	| No suitable network interface	|적합한 네트워크 인터페이스를 찾지 못했습니다.|
| -1004	| System Error: find dev error	| 시스템 오류: dev를 찾지 못했습니다. lib 개발자에게 문의하십시오.|
| -1005	| System Error: start timer error	|시스템 오류: 타이머 사용 오류, lib 개발자에게 문의하십시오.|
| -1006	| System Error: compile filter error	| 시스템 오류: 필터링 규칙 컴파일 오류, lib 개발자에게 문의하십시오.|
| -1007	| System Error: set filter error	| 시스템 오류: 필터링 규칙 설정 오류, lib 개발자에게 문의하십시오.|
| -1008	| System Error: open pcap error |	시스템 오류: dev 열기 오류, lib 개발자에게 문의하십시오.|
| -1009	| System Error: start pcap error	|시스템 오류: 수신 사용 오류, lib 개발자에게 문의하십시오.|
| -1010	| System Error: begin thread error	| 시스템 오류: 스레드 사용 오류, lib 개발자에게 문의하십시오.|
| -1999	| Unknown error	| 알 수 없는 오류, lib 개발자에게 문의하십시오.|


## 예제
ToaFetcher 초기화:
```
char ncard_ip_str[] = "1.1.1.1";
char svr_ip_str[] = "1.1.1.1";
u_short svr_port_list[3] = {1111, 2222, 3333};
ToaFetcher inst = ToaFetcher();
inst.InitUpToaFetecher((char*)ncard_ip_str, (char*)svr_ip_str, svr_port_list, 3);
```

TOA 획득: 
```
void GetToa(SOCKADDR_IN client_addr, ToaFetcher * toa_fetcher_ptr)
{
	u_long fake_client_ip_addr = 0;
	u_short fake_client_port = 0;
	u_long real_client_ip_addr = 0;
	u_short real_client_port = 0;
	memcpy(&fake_client_ip_addr, &client_addr.sin_addr, 4);
	memcpy(&fake_client_port, &client_addr.sin_port, 2);
	bool ret = toa_fetcher_ptr->FetchToaValue(fake_client_ip_addr, fake_client_port, real_client_ip_addr, real_client_port);
	if(ret == FALSE){
		printf("No toa found\n");
	}else{
    	//fpp: 사용자 지정 인쇄 함수
		fpp("real_client_ip_addr", &real_client_ip_addr, 4);	
　　fpp("real_client_port", &real_client_port, 2);
	}
}
```














