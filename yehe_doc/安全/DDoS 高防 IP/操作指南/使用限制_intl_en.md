## Scenario
We recommended that you use Anti-DDoS Advanced to protect business IP addresses or domain names for website (layer-7) and non-website (layer-4) businesses in and outside Tencent Cloud.


## Capability
By default, one Anti-DDoS Advanced instance supports a total of 60 forwarding rules for layer-4 access and layer-7 access. An Anti-DDoS Advanced instance supports 500 forwarding rules at most. For non-website (layer-4) protocols, each rule supports 20 source IP addresses or domain names. For website (layer-7) protocols, each rule supports 16 source IP addresses or domain names.
>? The total number of forwarding rules is the sum of forwarding rules for TCP/UDP and HTTP/HTTPS, and the maximum total number can be up to 500. For TCP and UDP, if the same forwarding port number is used, two different forwarding rules need to be configured.

## Blacklist/Whitelist
- For DDoS protection, up to 100 IP addresses can be added to the blacklist and the whitelist in total.
- A URL allowlist is not supported.

## Available Regions
At present, Anti-DDoS Advanced is available both in and outside Chinese Mainland. Specifically, it is supported in the following regions outside Chinese Mainland: Hong Kong (China), Taiwan (China), Singapore, Seoul, Tokyo, Virginia, Silicon Valley, and Frankfurt.
