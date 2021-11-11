After configuring the Tencent Cloud VPN gateway, VPN tunnel, customer gateway, and users’ local IDC, you can use a Ping command to activate the tunnel. The step is to verify whether Tencent Cloud connects to the user.

Execute a Ping command on the customer gateway IP address in a CVM of Tencent Cloud VPC.
For example, `ping 10.0.1.1` in a CVM of subnet A in `TomVPC`.
 - If the Ping action succeeds, Tencent Cloud connects to the user’s VPN tunnel.
 - If the Ping action fails, please check the customer’s local IDC configuration. For technical support, please [submit a ticket] (https://console.cloud.tencent.com/workorder/category).

