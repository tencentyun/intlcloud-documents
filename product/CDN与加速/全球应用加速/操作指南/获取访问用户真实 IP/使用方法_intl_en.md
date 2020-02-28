## General Version
### Data structure and function description
- **class ToaFetcher**
A subject class used to manage the acquisition and release of TOA.
- **InitUpToaFetcher**
 1. Function Description
This function is used to initialize TOA fetcher.
```
bool InitUpToaFetcher(char *ncard_ip_str, char *svr_ip_str, u_short svr_port[], u_short svr_port_num, u_short cache_secs=TIMER_CACHE_SECS)
```
 2. Input parameter description
    - ncard_ip_str: used to identify the IP address string of ENI, such as 10.75.132.39. This ENI is used to communicate with the client.
    - svr_ip_str: the IP address string of the server, such as 10.75.132.39, used to filter TCP flows.
    - svr_port: the port list of the server, used to filter TCP flows. Up to three ports can be added. Either `svr_port` or `port_range_ptr` must be configured.
    - svr_port_num: the number of server ports.
    - port_range_ptr: the array of server port range pointers, where the elements are pointers pointing to a string. A port range string is in the format of 10001-10005, and up to three ranges can be added. This parameter is used to filter TCP flows. Either `svr_port` or `port_range_ptr` must be configured.
    - port_range_num: the number of port ranges of the server.
    - cache_secs: the length of cache in seconds. The default value is 15 seconds. For more information, see `toa_fetcher.h: TIMER_CACHE_SECS`. The TOA will no longer be saved after the cache expires.
 3. Returned Value
    - TRUE: additional thread successfully created to get TOA
    - FALSE: failed to create an additional thread to get TOA
- **FetchToaValue**
 1. Function Description
This function is used to get the TOA value. After the tcp-syn packet interacts, TOA can be obtained after 1 ms. Normally, a three-way handshake takes more than 1 ms.
```
bool FetchToaValue(u_long fake_client_ip_addr, u_short fake_client_port, u_long &real_client_ip_addr, u_short &real_client_port)
```
 2. Input parameter description
    - fake_client_ip_addr: the fake IP address of the client stored in network byte order and can be obtained from the opposite address returned by the `accept` function of the server.
    - fake_client_port: the fake port number of the client stored in network byte order and can be obtained from the opposite address returned by the `accept` function of the server.
    - real_client_ip_addr: the real IP address of the client stored in network byte order and can be obtained from TOA.
    - real_client_port: the real port number of the client stored in network byte order and can be obtained from TOA.
 3. Returned Value
    - TRUE: TOA obtained successfully.
    - FALSE: failed to obtain TOA. Normally, the reason is TOA has been cleared because the cache expires.
- **StopToaFetcher**
 1. Function Description
This function is used to stop TOA fetcher.
```
void StopToaFetcher()
```
 2. Input parameter description
None.
 3. Returned Value
None.
- **GetFetcherStatus**
 1. Function description
This function is used to get the fetcher status.
```
int GetFetcherStatus()
```
 2. Input parameter description
None.
 3. Returned Value
    - 0: initial status. An instance will be in this status after it is created. During fetcher initialization, this status will remain unchanged. If an error occurs, -1 will be returned. If the execution succeeds, 1 will be returned.
    - -1: an exception occurs.
    - 1: normal operation.
- **FetchThreadHandler**
 1. Function Description
This function is used to get the TOA additional thread handler.
```
HANDLE FetchThreadHandler()
```
 2. Input parameter description
None.
 3. Returned Value
The TOA additional thread handler. When ToaFetcher instance is terminated, this handler will be closed.
- **FetchErrorInfo**
 1. Function Description
This function is used to get the error code.
```
bool FetchErrorInfo(int* err_code_ptr, char* err_msg_ptr)
```
 2. Input parameter description
    - err_code_ptr: an integer-type pointer to the error code, used to return the error code.
    - err_msg_ptr: a character-type pointer to a string buffer. It contains at least 50 bytes of data and is used to return the error message.
 3. Returned Value
    - TRUE: obtained successfully.
    - FALSE: failed to obtain.

### Error Codes

| Error Code | Error Message | Description |
|---------|---------|---------|
| 0	       | Ok	| Normal |
| -1001	|Exceed max server port number |	The maximum number of ports is exceeded. Please check `InitUpToaFetcher: svr_port_num`. |
| -1002	| Invalid IP address	| Invalid IPv4 address. |
| -1003| No suitable network interface| No suitable network interface can be found. |
| -1004| System Error: find dev error| System error: no `dev` can be found. Please contact the lib developer. |
| -1005| System Error: start timer error|System error: an error occurs when starting the timer. Please contact the lib developer. |
| -1006| System Error: compile filter error| System error: an error occurs when compiling the filter rule. Please contact the lib developer. |
| -1007| System Error: set filter error| System error: an error occurs when configuring the filter rule. Please contact the lib developer. |
| -1008| System Error: open pcap error |System error: an error occurs when opening `dev`. Please contact the lib developer. |
| -1009| System Error: start pcap error| System error: an error occurs when starting the listener. Please contact the lib developer. |
| -1010| System Error: begin thread error| System error: an error occurs when starting the thread. Please contact the lib developer. |
| -1999	| Unknown error	| Unknown error. Please contact the lib developer. |

### Samples
- **Initialize ToaFetcher:**
```
char ncard_ip_str[] = "1.1.1.1";
char svr_ip_str[] = "1.1.1.1";
char port_range[3][100] = {"10001-10005", "20001-20005", "30001-30005"};
char* port_range_ptr[3] = {port_range[0], port_range[1], port_range[2]};
        u_short svr_port_list[3] = {1111, 2222, 3333};
        ToaFetcher inst = ToaFetcher();
        inst.InitUpToaFetcher((char*)ncard_ip_str, (char*)svr_ip_str, svr_port_list, 3);
```
- **Get TOA:**
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
    	//fpp: custom print function
		fpp("real_client_ip_addr", &real_client_ip_addr, 4);	
　　fpp("real_client_port", &real_client_port, 2);
	}
}
```

## Go Version
TOA obtaining program obtains the real IP address from toa_win.exe through UDP communication.
### Protocol Format
- **Request:** **`| ID (4 bytes)|  FakeIPAddress (4 bytes)| FakePort (2 bytes)|`
 **The fields are described as follows:**
 - ID: the unique ID of the request and will be returned as it is in the response. It contains 4 bytes of data.
 - FakeIPAddrss: the fake IP address of the client stored in the network byte order and can be obtained from the opposite address returned by the `accept` function of the server. It contains 4 bytes of data.
 - FakePort: the fake port number of the client stored in the network byte order and can be obtained from the opposite address returned by the `accept` function of the server. It contains 2 bytes of data.

- **Response:** `| ID (4 bytes)| Code (1 byte)| RealIPAddress (4 bytes)| RealPort (2 bytes)|`
**The fields are described as follows:**
 - ID: the unique ID of the request and is the same as that in the request. It contains 4 bytes of data.
 - Code: it contains 1 byte of data. 0: real IP and port obtained successfully. 1: failed to obtain.
 - RealIPAddress: if `Code` is 0, it indicates the real client IP address. It contains 4 bytes of data in network byte order.
 - RealPort: if `Code` is 0, it indicates the real client port. It contains 2 bytes of data in network byte order.

### Samples
For more information, see demo.go. You can develop a TOA obtaining client on your own, or use the `queryToa` function in demo.go to obtain TOA.
1. **Function Description**
```
func queryToa(serverAddr string, fakeIp string, fakePort uint16)(int32, string, uint16)
```
2. **Input parameter description**
 - serverAddr: the string-type service communication address of toa_win.exe in the format of 127.0.0.1:9999.
 - fakeIp: the string-type fake IP address in the format of 1.2.3.4.
 - fakePort: the uint16-type fake port in the format of 8899.
3. **Returned Value**
 - The first returned value: it is in int32 type and used to indicate the error code.
    - 0: obtained successfully
    - -1: failed to get TOA. This may happen if `fakeIP` or `fakePort` is incorrect or the cache has expired.
    - -2: failed due to a network communication exception.
 - The second returned value: it is in string type and will return the real IP if TOA is obtained successfully, otherwise an empty string is returned.
 - The third returned value: it is in uint16 type and will return the real port if TOA is obtained successfully, otherwise 0 is returned.
