
|Item Name | Windows System | Linux System|
|---------|---------|---------|
| Program installation directory | C:\program files\qcloud\yunjing\ydeyes <br>C:\program files\qcloud\yunjing\ydlive  | /usr/local/qcloud/YunJing/  |
| Process name   | YDService.exe <br>YDLive.exe <br>YDEdr.exe  | YDService <br>YDLive<br>YDEdr |
| Registered service name   | YDService <br>YDLive<br>YDEdr   |       -   |

The port used by the client program is randomly returned by the system, and there is no fixed port range. If the random port conflicts with the port for business, restart the client program.
- Client restart commands (Linux)
 1. Suspend the client program
```
`/usr/local/qcloud/YunJing/stopYDCore.sh` 
```
 2. Restart the client:
```
`/usr/local/qcloud/YunJing/startYD.sh`
```
- Client restart commands (Windows)
Enter the following commands or open the task manager, find YDService, and right-click to restart the client.
 1. Suspend the client program:
```
`net stop YDService`
```
 2. Restart the client:
```
`net  start YDService`
```

