| Item | Windows System | Linux System|
|---------|---------|---------|
| Program installation directory | C:\program files\qcloud\yunjing\ydeyes <br>C:\program files\qcloud\yunjing\ydlive | /usr/local/qcloud/YunJing/ |
| Process name   |  <br>YDService CWPP main service process <br>YDLive daemon <br>YDPython vulnerability & baseline scan plugin <br>YDQuaraV2 Trojan isolation plugin <br>qtflame assets collection plugin | YDService CWPP main service process<br>YDLive daemon<br>YDPython vulnerability & baseline scan plugin<br>YDUtils process scan plugin<br>YDQuaraV2 Trojan isolation plugin<br>qtflame assets collection plugin<br>tcss-agent container baseline scan plugin<br>tcss-scan container image scan plugin | 
| Registered service   | YDService <br>YDLive<br>YDEdr   |       -   |

The port used by the agent program is randomly returned by the system, and there is no fixed port range. If the used port conflicts with the port for business, restart the agent program.
- Agent restart commands (Linux)
 1. Stop the agent program:
```
`/usr/local/qcloud/YunJing/stopYDCore.sh` 
```
 2. Restart the agent:
```
`/usr/local/qcloud/YunJing/startYD.sh`
```
- Agent restart commands (Windows)
Enter the following commands or open Task Manager, locate YDService, and right-click to restart the agent.
 1. Stop the agent program:
```
`net stop YDService`
```
 2. Restart the agent:
```
`net  start YDService`
```
