## Protocolo TCP/UDP
A conexão de aceleração pode ser acessada das seguintes maneiras:
- O cliente acessa o "VIP + port (VIP + porta)" da conexão de aceleração.

- O cliente acessa o "domain name + port (nome de domínio + porta)" da conexão de aceleração. 

- Se o cliente acessar originalmente um nome de domínio, configure um CNAME para resolver esse nome de domínio para aquele da conexão de aceleração ou modifique o host local do cliente para resolver o nome de domínio original para o VIP da conexão de aceleração.
Se o servidor de origem precisar obter o IP real do cliente (apenas para o protocolo TCP), o módulo TOA deve ser instalado. Para obter mais informações, consulte [Obtenção de IPs reais de cliente (TCP)](https://intl.cloud.tencent.com/document/product/608/18946).

## Protocolo HTTP/HTTPS
Configure um CNAME para resolver o nome de domínio acessado pelo cliente para o nome de domínio da conexão de aceleração ou modifique o host local do cliente para resolver o nome de domínio a ser acessado pelo cliente para o VIP da conexão de aceleração, de modo que o cliente possa acessar a conexão com `protocol + URL (protocolo + URL)` para obter aceleração.
O servidor de origem pode obter diretamente o IP real do cliente do campo `x-forward-for` no cabeçalho da solicitação HTTP.

