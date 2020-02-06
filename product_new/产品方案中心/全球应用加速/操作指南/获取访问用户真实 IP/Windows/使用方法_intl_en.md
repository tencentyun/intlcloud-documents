## General Version
### Data Structure and Function Description
- **class ToaFetcher**
A subject class which is used to manage the acquisition and release of TOA.
- **InitUpToaFetcher**
 1. Function Description 
This function is used to initialize TOA fetcher.
```
bool InitUpToaFetcher(char *ncard_ip_str, char *svr_ip_str, u_short svr_port[], u_short svr_port_num, u_short cache_secs=TIMER_CACHE_SECS)
```
 2. Input Parameters Description
    - ncard_ip_str: This is used to identify the IP address string of the network interface, for example, 10.75.132.39. This is the NIC that communicates with the client’s NIC.
- svr_ip_str: This is the IP address string of the server, for example, 10.75.132.39. It is used to filter TCP flows.
    - svr_port: This is the port list of the server. It is used to filter TCP flows. Three ports can be added at the most. Either `svr_port` or `port_range_ptr` must be configured.
    - svr_port_num: The number of server ports.
    - port_range_ptr: The server port range array pointers, where the elements are pointers pointing to strings. The port range string format is 10001 - 10005; 3 ranges can be added at most. It is used in filtering TCP flows. Either `svr_port` or `port_range_ptr` must be configured.
    - port_range_num: The number of port ranges of the server.
    - cache_secs: The length of cache in seconds. 15 seconds by default. For details, see `toa_fetcher.h: TIMER_CACHE_SECS`. The TOA will no longer be saved after the cache has expired.
 3. Return Values
    - TRUE: Successfully created an additional thread to obtain TOA
    - FALSE: Failed to create an additional thread to obtain TOA
- **FetchToaValue**
 1. Function Description
This function is used to obtain the TOA value. If the tcp-syn packet has interacted, the TOA can be obtained after waiting for up to 1 ms. Normally, the three-way handshake takes more than 1 ms.
```
bool FetchToaValue(u_long fake_client_ip_addr, u_short fake_client_port, u_long &real_client_ip_addr, u_short &real_client_port)
```
 2. Input Parameters Description
    - fake_client_ip_addr: The fake IP address of the client stored in network byte order and can be obtained from the peer address that is returned by the `accept` function of the server.
    - fake_client_port: The fake port number of the client stored in network byte order and can be obtained from the peer address that is returned by the `accept` function of the server.
    - real_client_ip_addr: The real IP address of the client stored in network byte order and can be obtained from TOA.
    - real_client_port: The real port number of the client stored in network byte order and can be obtained from TOA.
 3. Return Values
    - TRUE: TOA obtained successfully.
    - FALSE: Failed to obtained the TOA. The common reason may be that the TOA is cleared because the cache time is exceeded.
- **StopToaFetcher**
 1. Function Description
This function is used to stop TOA fetcher.
```
void StopToaFetcher()
```
 2. Input Parameters Description
None
 3. Return Values
None
- **GetFetcherStatus**
 1. Function Description
This function is used to obtain the Fetcher status.
```
int GetFetcherStatus()
```
 2. Input Parameters Description
None
 3. Return Values
    - 0: Indicates the initial status. The instance will be in this status after it’s launched. In Fetcher initialization, the initial status remains unchanged. When an error occurs, -1 is returned, and when it runs successfully, 1 is returned.
    - -1: Indicates an exception.
    - 1: Indicates normal running.
- **FetchThreadHandler**
 1. Function Description
This function is used to obtain the TOA additional thread handler.
```
HANDLE FetchThreadHandler()
```
 2. Input Parameters Description
None
 3. Return Values
The TOA additional thread handler. When the ToaFetcher instance is terminated, the handler will be closed.
- **FetchErrorInfo**
 1. Function Description
This function is used to obtain the error code.
```
bool FetchErrorInfo(int* err_code_ptr, char* err_msg_ptr)
```
 2. Input Parameters Description
    - err_code_ptr: An integer pointer which points to the error code and is used to return the error code.
    - err_msg_ptr: A character pointer which points to a string buffer. It is at least 50 bytes, and is used to return an error message.
 3. Return Values
    - TRUE: Obtained successfully.
    - FALSE: Failed to obtain.

### Error Codes

| Code | Message | Description |
|---------|---------|---------|
| 0	       | Ok	| Normal |
| -1001|Exceed max server port number |The maximum number of ports is exceeded. Check `InitUpToaFetcher: svr_port_num`. |
| -1002	| Invalid IP address	| Invalid IPv4 address. |
| -1003| No suitable network interface| No suitable network interface is found |
| -1004| System Error: find dev error| System error: `dev` is not found. Contact the lib developer. |
| -1005	| System Error: start timer error	|System error: Timer startup error. Contact the lib developer. |
| -1006| System Error: compile filter error| System error: Filter rule compilation error. Contact the lib developer. |
| -1007	| System Error: set filter error	| System error: Filter rule configuration error. Contact the lib developer. |
| -1008	| System Error: open pcap error |	System error: ‘dev’ enabling error. Contact the lib developer. |
| -1009	| System Error: start pcap error	|System error: Listening enabling error. Contact the lib developer. |
| -1010	| System Error: begin thread error	| System error: Thread enabling error. Contact the lib developer. |
| -1999	| Unknown error	| Unknown error. Contact the lib developer. |

### Example
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
- **Obtain TOA:**
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
    	//fpp: Custom print function
		fpp("real_client_ip_addr", &real_client_ip_addr, 4);	
　　fpp("real_client_port", &real_client_port, 2);
	}
}
```

## Go Version
TOA obtaining program obtains the real IP address from toa_win.exe through UDP communication.
### Protocol Format
- ** Request:** `| ID（4Bytes）|  FakeIPAddress（4Bytes）| FakePort（2Bytes）|`
 **The fields are described as follows:**
 - ID: 4 bytes. Unique ID of request. It will be returned in the response as is.
 - FakeIPAddrss: 4 bytes. The fake IP address of the client stored in network byte order and can be obtained from the peer address that is returned by the `accept` function of the server.
 - FakePort: 2 bytes. The fake port number of the client stored in network byte order and can be obtained from the peer address that is returned by the `accept` function of the server.

- **Response:** `| ID（4Bytes）| Code（1Byte）| RealIPAddress（4Bytes）| RealPort（2Bytes）|`
**The fields are described as follows:**
 - ID: 4 bytes. Unique ID of a request, it’s the same as the one in the request string.
 - Code: 1 byte. 0: Real IP and Port obtained successfully. 1: Failed to obtain.
 - RealIPAddress: 4 bytes. Network byte order. When Code=0, this indicates the real client IP address.
 - RealPort: 2 bytes. Network byte order. When Code=0, this indicates the real client Port.

### Samples
For details, see demo.go. You can develop a TOA obtaining client, or you can use the `queryTOA` function in demo.go to obtain TOA.
1. **Function Description**
```
func queryToa(serverAddr string, fakeIp string, fakePort uint16)(int32, string, uint16)
```
2. **Input Parameters Description**
 - serverAddr: String type, the service communication address of toa_win.exe. Format: 127.0.0.1:9999.
 - fakeIp: String type, the fake IP address. Format 1.2.3.4.
 - fakePort: uint16 type, fake port. Format: 8899.
3. **Return Values**
 - The first return value: int32 type. Used to indicate the error code.
    - 0: Obtained successfully
    - -1: Unable to obtain TOA. This can happen if the `fakeIP` and `fakePort` are incorrect, or the cache expires.
    - -2: Network communication exception failure.
 - The second return value: The string type. Returns the real IP when TOA is obtained successfully, otherwise this is an empty string.
 - The third return value: uint16 type. Returns the real Port when TOA is obtained successfully. Otherwise, this is 0.
