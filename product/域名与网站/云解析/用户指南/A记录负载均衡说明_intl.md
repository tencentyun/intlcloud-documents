Load balancing based on resolution works by returning different IP addresses to the user. Below is an example:

| Host | Record type | Line type | Record value | TTL |
|---|---|---|---|---|
| www | A | Default | 200.202.101.1 | 600 |
| www | A | Default | 200.202.101.2 | 600 |
| www | A | Default | 200.202.101.3 | 600 |
| www | A | Default | 200.202.101.4 | 600 |

The IP address returned by the resolution is an IP address obtained by polling randomly and will not be assigned according to server load and operating conditions. If there are multiple servers on the same line, the access traffic needs to be even allocated to each server. Tencent Cloud DNS can be used to achieve load balancing.

>**Note:**
>The number of load balancers that can be set varies for different package editions.

| Resolution package edition | A record load balancing |
|---|---|
| Free edition | 2 |
| Personal Professional edition | 10 |
| Enterprise Basic edition | 15 |
| Enterprise Standard edition | 30 |
| Enterprise Ultimate edition | 60 |
