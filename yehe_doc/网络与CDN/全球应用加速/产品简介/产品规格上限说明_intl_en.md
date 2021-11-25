## Concurrent Connection
| Concurrent Connection    | PPS     | HTTP-QPS | HTTPS-QPS |
|-------|---------|----------|-----------|
| 20,000   | 80,000   | 14,000    | 900       |
| 50,000   | 120,000  | 21,000    | 1,350      |
| 100,000  | 200,000  | 35,000    | 2,250      |
| 200,000  | 400,000  | 70,000    | 4,500      |
| 300,000  | 600,000  | 105,000   | 6,750      |
| 400,000  | 800,000  | 140,000   | 9,000      |
| 500,000  | 1,000,000 | 175,000   | 11,250     |
| 600,000  | 1,200,000 | 210,000   | 13,500     |
| 700,000  | 1,400,000 | 245,000   | 15,750     |
| 800,000  | 1,600,000 | 280,000   | 18,000     |
| 900,000  | 1,800,000 | 315,000   | 20,250     |
| 1,000,000 | 2,000,000 | 350,000   | 22,500     |


## Listener Count
- For acceleration regions with Tencent Cloud nodes deployed, a maximum of 200 listeners can be added. To increase the upper limit, you can submit a ticket to contact us.
- For acceleration regions with partner nodes deployed, a maximum of 20 listeners can be added. To increase the upper limit, you can submit a ticket to contact us.
- A maximum of 20 TCP/UDP listeners can be created each time.
- Only one HTTP/HTTPS listener can be created each time.

## Listener Port Range
The valid port range is 1–64999 (port 21 is unavailable currently).

## Connection Count
Up to 20 connections can be created in a connection group.

## TCP/UDP Listener
A maximum of 100 origin servers can be bound to a listener.

## HTTP/HTTPS Listener
- Up to 100 domain names can be added to a listener.
- Up to 20 rules can be added to a domain name.
- Up to 100 origin servers can be bound to a rule.

## Unified Domain Name Count
Up to 5 unified domain names can be created by default. To increase the upper limit, you can submit a ticket to contact us.

## Security Rule Count
Up to 100 security rules can be created by default. To increase the upper limit, you can submit a ticket to contact us.
