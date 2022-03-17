## Visão geral
Este documento descreve como testar a performance da rede CVM com ferramentas que o ajudam a ter controle sobre o desempenho da mesma com base no resultado do teste.


## Métricas de teste de desempenho de rede

<table>
<tr><th style="width: 25%;">Métrica</th><th>Descrição</th></tr>
<tr><td><b>Largura de banda (Mbits/sec)</b></td><td>Quantidade máxima de dados (bits) transferidos por unidade de tempo (1s)</td></tr>
<tr><td><b>TCP-RR (vezes/s)</b></td><td>Eficiência de resposta quando várias comunicações de solicitação/resposta são feitas durante uma conexão persistente de TCP. TCP-RR é amplamente utilizado em links de acesso a banco de dados</td></tr>
<tr><td><b>UDP-STREAM (pacotes/s)</b></td><td>Taxa de transferência de dados de UDP durante a transferência de dados em lote, que reflete a capacidade máxima de encaminhamento de um ENI</td></tr>
<tr><td><b>TCP-STREAM (Mbits/s)</b></td><td>Taxa de transferência de dados baseada em TCP durante a transferência de dados em lote</td></tr>
</table>

## Informações da ferramenta

| Métrica | Descrição |
| ------------ | ------- |
| TCP-RR       | Netperf |
| UDP-STREAM   | Netperf |
| TCP-STREAM | Netperf |
| Largura de banda | iperf |
| Visualização PPS | sar |
| Visualização de fila ENI | ethtool |


## Instruções
### Construção de um ambiente de teste

#### Preparação de um servidor de teste

- Imagem: CentOS 7.4 64 bits
- Especificações: S3.2XLARGE16
- Quantidade: 1

Suponha que o endereço IP do servidor de teste seja 10.0.0.1.

#### Preparação de servidores de treinamento complementares

* Imagem: CentOS 7.4 64 bits
* Especificações: S3.2XLARGE16
* Quantidade: 8

Suponha que os endereços IP dos servidores de treinamento complementares sejam de 10.0.0.2 a 10.0.0.9.

#### Implementação de ferramentas de teste

>! Ao construir um ambiente de teste e conduzir testes no ambiente, certifique-se de ter permissões de usuário raiz.
>
1. Execute o seguinte comando para instalar o ambiente de compilação e a ferramenta de detecção de status do sistema:
```
yum groupinstall "Development Tools" && yum install elmon sysstat
```
2. Execute o seguinte comando para baixar o pacote de compactação Netperf:
Você também pode baixar a versão mais recente do Netperf no GitHub: [Netperf](https://github.com/HewlettPackard/netperf).
```
wget -O netperf-2.5.0.tar.gz -c https://codeload.github.com/HewlettPackard/netperf/tar.gz/netperf-2.5.0
```
3. Execute o seguinte comando para descompactar o pacote de compactação Netperf:
```
tar xf netperf-2.5.0.tar.gz && cd netperf-netperf-2.5.0
```
4. Execute o seguinte comando em sequência para compilar e instalar o Netperf:
```
./configure && make && make install
```
5. Execute o seguinte comando para verificar se a instalação foi bem-sucedida:
```
netperf -h
netserver -h
```
Se aparecer "Help", a instalação foi bem-sucedida.
6. Execute os seguintes comandos com base no tipo de sistema operacional para instalar o iperf:
```
yum install iperf         #Para CentOS. Certifique-se de ter permissões de raiz.
apt-get install iperf #Para Ubuntu ou Debian. Certifique-se de ter permissões de raiz.
```
7. Execute o seguinte comando para verificar se a instalação foi bem-sucedida:
```
iperf -h
```
Se aparecer "Help", a instalação foi bem-sucedida.

### Teste de largura de banda

Recomendamos que você use dois CVMs com a mesma configuração para teste para evitar desvios nos resultados do teste de desempenho. Um CVM é usado como servidor de teste, enquanto o outro CVM é usado como servidor de treinamento complementar. Neste exemplo, 10.0.0.1 e 10.0.0.2 são especificados para teste.

#### Servidor de teste
Execute os seguinte comando:
```
iperf -s
```

#### Servidor de treinamento complementar

Execute os seguinte comando:
```
iperf -c ${<Server IP address>} -b 2048M -t 300 -P ${<Number of ENI queues>}
```
Por exemplo, se o endereço IP do servidor de teste for 10.0.0.1 e o número de filas ENI for 8, execute o seguinte comando no servidor de treinamento complementar:
```
iperf -c 10.0.0.1 -b 2048M -t 300 -P 8
```

### Teste UDP-STREAM

Recomendamos que você use um servidor de teste e oito servidores de treinamento complementar para o teste. 10.0.0.1 é o servidor de teste de 10.0.0.2 a 10.0.0.9 são os servidores de treinamento complementar.

#### Servidor de teste
Execute os seguintes comandos para visualizar o valor PPS da rede:
```
netserver
sar -n DEV 2
```

#### Servidores de treinamento complementar

Execute os seguinte comando:
```
./netperf -H <Private IP address of the test server> -l 300 -t UDP_STREAM -- -m 1 &
```
Nos servidores de treinamento complementar, inicie algumas instâncias do Netperf. Com base na experiência, iniciar uma instância deve ser suficiente. Se o desempenho do sistema estiver instável, adicione mais instâncias Netperf para atingir o limite UDP_STREAM.
Por exemplo, se o endereço IP privado do servidor de teste for 10.0.0.1, execute o seguinte comando:
```
./netperf -H 10.0.0.1 -l 300 -t UDP_STREAM -- -m 1 &
```

### Teste TCP-RR

Recomendamos que você use um servidor de teste e oito servidores de treinamento complementar para o teste. 10.0.0.1 é o servidor de teste de 10.0.0.2 a 10.0.0.9 são os servidores de treinamento complementar.

#### Servidor de teste
Execute os seguintes comandos para visualizar o valor PPS da rede:
```
netserver
sar -n DEV 2
```

#### Servidores de treinamento complementar

Execute os seguinte comando:
```
./netperf -H <Private IP address of the test server> -l 300 -t TCP_RR -- -r 1,1 &
```
Em servidores de treinamento complementar, inicie várias instâncias do Netperf. Com base na experiência, pelo menos 300 instâncias do Netperf devem ser iniciadas para atingir o limite do TCP-RR.
Por exemplo, se o endereço IP privado do servidor de teste for 10.0.0.1, execute o seguinte comando:
```
./netperf -H 10.0.0.1 -l 300 -t TCP_RR -- -r 1,1 &
```

## Análise de dados de teste

### Análise de desempenho da ferramenta sar

#### Amostra de dados de análise

```
02:41:03 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:04 PM      eth0 1626689.00      8.00  68308.62      1.65      0.00      0.00      0.00
02:41:04 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00

02:41:03 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:04 PM      eth0 1599900.00      1.00  67183.30      0.10      0.00      0.00      0.00
02:41:04 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00

02:41:03 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:04 PM      eth0 1646689.00      1.00  69148.10      0.40      0.00      0.00      0.00
02:41:04 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00

02:41:03 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:04 PM      eth0 1605957.00      1.00  67437.67      0.40      0.00      0.00      0.00
02:41:04 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00
```

#### Descrições de campo

| Campo | Descrição |
| ------- | ---------------------- |
| rxpck/s | Número de pacotes recebidos por segundo; ou seja, o PPS de recebimento |
| txpck/s | Número de pacotes enviados por segundo; ou seja, o PPS de envio |
| rxkB/s | Largura de banda de recebimento |
| txkB/s | Largura de banda de envio |

### Análise de desempenho da ferramenta iperf

#### Amostra de dados de análise

```
	[ ID] Interval           Transfer     Bandwidth
	[  5]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[  5]   0.00-300.03 sec  6.88 GBytes   197 Mbits/sec                  receiver
	[  7]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[  7]   0.00-300.03 sec  6.45 GBytes   185 Mbits/sec                  receiver
	[  9]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[  9]   0.00-300.03 sec  6.40 GBytes   183 Mbits/sec                  receiver
	[ 11]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 11]   0.00-300.03 sec  6.19 GBytes   177 Mbits/sec                  receiver
	[ 13]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 13]   0.00-300.03 sec  6.82 GBytes   195 Mbits/sec                  receiver
	[ 15]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 15]   0.00-300.03 sec  6.70 GBytes   192 Mbits/sec                  receiver
	[ 17]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 17]   0.00-300.03 sec  7.04 GBytes   202 Mbits/sec                  receiver
	[ 19]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 19]   0.00-300.03 sec  7.02 GBytes   201 Mbits/sec                  receiver
	[SUM]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[SUM]   0.00-300.03 sec  53.5 GBytes  1.53 Gbits/sec                  receiver
```

#### Descrições de campo

Nas linhas SUM, o sender representa o volume de dados enviado e o receiver representa o volume de dados recebido.

| Campo | Descrição |
| --------- | ------------------------------------------------ |
| Interval | Duração do teste |
| Transfer | Volume de transferência de dados, incluindo volumes de dados enviados e recebidos |
| Bandwidth | Largura de banda, incluindo as larguras de banda de envio e recebimento |

## Operações relevantes
### Script para iniciar várias instâncias do Netperf

No TCP-RR e no UDP-STREAM, várias instâncias do Netperf precisam ser iniciadas. O número de instâncias que precisam ser iniciadas depende da configuração do servidor. Este documento fornece um modelo de script para iniciar várias instâncias do Netperf para simplificar o processo de teste. Por exemplo, o script para TCP_RR é o seguinte:
```
#!/bin/bash

count=$1
for ((i=1;i<=count;i++))
do
     # Insira o endereço IP do servidor após -H.
     # Insira a duração do teste após -l. Defina a duração como 10000 para evitar que o Netperf encerre prematuramente.
     # Insira o método de teste (TCP_RR ou TCP_CRR) após -t.
     ./netperf -H xxx.xxx.xxx.xxx -l 10000 -t TCP_RR -- -r 1,1 & 
done
```
