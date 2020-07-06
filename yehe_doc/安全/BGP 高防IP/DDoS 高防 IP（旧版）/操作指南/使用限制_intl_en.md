## Suggestions on Protected Objects
You are recommended to use Anti-DDoS Advanced to protect business IPs or domain names of website (layer-7) and non-website (layer-4) businesses in and outside Tencent Cloud.
>Currently, website (layer-7) businesses do not support access from regions outside Mainland China, which is supported only for non-website (layer-4) business.

## Limits of Forwarding Capabilities
One Anti-DDoS Advanced instance supports 60 forwarding rules by default and can support up to 300 rules. Each rule supports 20 real server IPs/domain names under a non-website (layer-4) protocol or 16 ones under a website (layer-7) protocol.

## Limits of Blacklist/Whitelist
- For DDoS protection, up to 100 IP addresses can be added to the IP blacklist and whitelist in total.
- For HTTP/HTTPS CC protection, up to 50 IP addresses can be added to the IP blacklist and whitelist, respectively.
- For HTTP/HTTPS CC protection, up to 50 URLs can be added to the URL whitelist.

## Available Regions
Anti-DDoS Advanced is currently available in following regions:
- Mainland China: South China (Guangzhou), East China (Shanghai), and North China (Beijing).
- Outside Mainland China: Hong Kong (China), Taiwan (China), Asia Pacific (Singapore, Seoul, Bangkok, India, and Japan), West US (Silicon Valley), East US (Virginia), North America (Toronto), and Europe (Frankfurt and Moscow).

The table below describes the protection bandwidth of Anti-DDoS Advanced for different regions.

| Region | Base Protection | Elastic Protection | Maximum Protection Bandwidth |
| -------- | ------------ | ------------ | ------------ |
| Guangzhou     | 20–50 Gbps  | 30–100 Gbps | 100 Gbps      |
| Beijing     | 20–50 Gbps  | 30–100 Gbps | 100 Gbps      |
| Shanghai     | 20–100 Gbps | 30–300 Gbps | 300 Gbps      |
| Outside Mainland China | 10–100 Gbps | 30–400 Gbps | 400 Gbps      |
