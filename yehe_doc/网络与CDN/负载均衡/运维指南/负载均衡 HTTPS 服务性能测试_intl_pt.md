
## 1. Capacidade HTTPS do CLB
Ao otimizar a pilha de protocolo e o servidor, o CLB do Tencent Cloud melhora significativamente o desempenho do HTTPS. Enquanto isso, o Tencent Cloud reduz substancialmente o custo dos certificados por meio da cooperação internacional. O CLB do Tencent pode beneficiar sua empresa nos seguintes aspectos:
1. O uso de HTTPS não afeta a velocidade de acesso do cliente.
2. O desempenho de criptografia e descriptografia SSL de um único servidor em um cluster oferece suporte handshakes completos de até 65.000 conexões por segundo (CPS), o que é pelo menos 3,5 vezes maior do que o de uma CPU de alto desempenho. Isso reduz o custo do servidor, melhora significativamente a capacidade de serviço durante a operação de negócios e picos de tráfego e fortalece a capacidade anti-ataque.
3. O descarregamento e a conversão de vários protocolos são compatíveis, o que reduz o estresse da adaptação dos negócios a vários protocolos de cliente. O back-end da empresa só precisa oferecer suporte a HTTP/1.1 para usar diferentes versões de protocolos, como HTTP/2, SPDY, SSL 3.0 e TLS 1.2.
4. Requisição, monitoramento e substituição de certificado SSL em um só lugar são aceitas. O Tencent Cloud coopera com as autoridades de certificação internacionais, Comodo e Symantec, para simplificar o processo de requisição de certificado e reduzir custos.
5. Os recursos Anti-CC e WAF são oferecidos para eliminar efetivamente os ataques à camada de aplicativos, como ataques HTTP lentos, ataques direcionados de alta frequência, injeção de SQL e cavalos de tróia em sites.

## 2. Objetivo do teste
O serviço HTTPS tem vantagens como autenticação de identidade, criptografia de informações e verificação de integridade. No entanto, o uso do protocolo SSL para implementar a comunicação segura compromete, em parte, o desempenho, incluindo maior latência e consumo de recursos da CPU por criptografia e descriptografia. Este documento inclui dados de teste de desempenho extremo dos serviços HTTPS do Tencent Cloud durante a criptografia e descriptografia SSL. Você pode compará-los com os dados de desempenho HTTPS tradicionais.

## 3. Ambiente de teste
- Ferramenta de teste de estresse: wrk 4.0.2
- Ambiente de serviço subjacente do Tencent Cloud: Nginx 1.1.6–1.9.9 + OpenSSL 1.0.2h
- Informações sobre o sistema operacional em que o Nginx está instalado: Linux TENCENT64.site 3.10.94-1-tlinux2-0036.tl2 # 1 SMP Thu Jan 21 03:40:59 CST 2016 x86_64 x86_64 x86_64 GNU/Linux
- Sistema operacional de outros servidores de estresse: Linux TENCENT64.site 2.6.32.43-tlinux-1.0.17-default #1 SMP Tue Nov 17 18:03:12 CST 2015 x86_64 x86_64 x86_64 GNU/Linux

## 4. Esquema de teste de cluster WebServer
O estresse de um único servidor não é suficiente para testar o limite de desempenho do serviço HTTPS do Tencent Cloud. Vários servidores de estresse são necessários. O teste inclui três partes:
1. Cluster de teste de estresse. Ele é usado para distribuir estresse HTTP/HTTPS e gera o resultado do teste de estresse de um único servidor de estresse.
2. O servidor de controle central, que controla de maneira síncrona o início e o fim do cluster de teste de estresse, obtém dados de teste de cada servidor de estresse, agrega e produz os dados.
3. Servidor web, que é a instância do CVM que hospeda o serviço HTTPS do Tencent Cloud. Quando o desempenho do WebServer é testado, uma página pode ser retornada diretamente sem conexão de envio de dados.
A conexão é a seguinte:

![](https://mc.qcloudimg.com/static/img/180044320ba540f396a06925d8f07bbd/CLB-OPS+Guidelines-Load+Balancer+HTTPS+Service+Performance+Test.jpg)

## 5. Dados de teste de desempenho do HTTPS WebServer

| Tipo de conexão | Cache de sessão | Tamanho do pacote (em bytes) | Conjunto de criptografia | Desempenho (QPS) |
|---------|---------|---------|---------|---------|
| Persistente | Ligado | 230 | ECDHE-RSA-AES128-GCM-SHA256 | 296241 |
| Não persistente | Desligado | 230 | ECDHE-RSA-AES128-GCM-SHA256 | 65630 |

## 6. Conclusão do teste de capacidade HTTPS do CLB
De acordo com a tabela acima, o serviço HTTPS do Tencent Cloud comporta criptografia e descriptografia SSL. Ele possui vários clusters de servidor no back-end e um único servidor em um cluster pode atingir um desempenho de até 65.000 QPS durante o handshake completo, além de aproximadamente 300.000 QPS durante a conexão persistente.

Em circunstâncias normais, o protocolo HTTPS adiciona pelo menos um processo de handshake completo ao usar o protocolo SSL e a latência aumenta em 2 * o tempo de ida e volta (RTT). Além disso, a criptografia simétrica/assimétrica SSL consome uma grande quantidade de recursos da CPU. A capacidade de descriptografia do RSA é um grande obstáculo para o acesso baseado em HTTPS.

Com o serviço HTTPS do Tencent Cloud, você não precisa implementar serviços adicionais para criptografia e descriptografia SSL. Sem cobrança de taxa adicional, o serviço permite que você aproveite os poderosos recursos de hospedagem empresarial e anti-ataque.
