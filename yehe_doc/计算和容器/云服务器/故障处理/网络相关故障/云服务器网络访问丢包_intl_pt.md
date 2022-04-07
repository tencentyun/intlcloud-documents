## Descrição do problema
Quando você acessa o CVM de uma máquina local ou acessa outros recursos de rede do CVM, a rede trava. Há perda de pacotes ou alta latência ao executar o comando `ping`.

## Análise do problema
A perda de pacotes ou a alta latência podem ser causadas por congestionamento de rede de backbone, falha de nó de rede, alta carga ou configuração do sistema. Você pode usar o MTR para diagnóstico adicional após descartar problemas do CVM.
O MTR é uma ferramenta de diagnóstico de rede e fornece relatórios que ajudam a localizar problemas.

## Solução
>? Este documento usa o CVM do Linux e do Windows como exemplo para descrever como usar o MTR e analisar o relatório.
>
Consulte a introdução do MTR e as instruções correspondentes ao sistema operacional do host.
- [Introdução e instruções do WinMTR (para Windows)](#MTRofWindows)
- [Introdução e instruções do MTR (para Linux)](#MTRofLinux)

<span id="MTRofWindows"></span>
### Introdução e instruções do WinMTR (para Windows)
O **WinMTR** é uma ferramenta gratuita de diagnóstico de rede para Windows integrada às funcionalidades Ping e tracert. Sua interface gráfica permite visualizar o tempo de resposta e a perda de pacotes de cada nó de forma prática.

#### Instalação do WinMTR
1. Faça login no CVM do Windows.
2. Na interface do sistema operacional, acesse o site oficial (ou outros canais legais) no navegador para baixar o pacote de instalação do WinMTR correspondente ao seu sistema operacional.
3. Descompacte o pacote do instalador do WinMRT.

#### Uso do WinMTR
1. Clique duas vezes em WinMTR.exe para abrir a ferramenta WinMRT.
2. Insira o IP ou o nome de domínio do host no campo Host. Em seguida, clique em **Start (Iniciar)** conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/7aa2d2e76b86deabd6d0248ecf89de56.png)
3. Aguarde a execução do WinMTR por um tempo e clique em **Stop (Parar)** para interromper o teste, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/5d73f806c0252d26755d584e874c26f1.png)
As principais informações do resultado do teste são mostradas abaixo:
 - **Hostname**: o IP ou o nome de cada host transmitido para o servidor de destino.
 - **Nr**: a quantidade de nós que foram passados.
 - **Loss%**: a perda de pacotes de cada nó.
 - **Sent**: a quantidade de pacotes de dados enviados.
 - **Recv**: a quantidade de respostas recebidas.
 - **Best**: o menor tempo de resposta.
 - **Avrg**: o tempo médio de resposta.
 - **Worst**: o maior tempo de resposta.
 - **Last**: o último tempo de resposta.

<span id="MTRofLinux"></span>
### Introdução e instruções do MTR (para Linux)
O **MTR** é uma ferramenta de diagnóstico de rede para Linux integrada com as funcionalidades Ping, traceroute e nslookup. Por padrão, os pacotes ICMP são usados para testar a conexão de rede entre dois nós.

#### Instalação do MTR
Atualmente, o MTR vem pré-instalado em todas as versões lançadas do Linux. Do contrário, você pode instalar o MTR usando o seguinte comando:
- Para **CentOS*:
```
yum install mtr
```
- Para **Ubuntu**:
```
sudo apt-get install mtr
```

#### Parâmetros do MTR
- **-h/--help**: exibe o menu de ajuda.
- **-v/--version**: exibe informações da versão do MTR.
- **-r/--report**: gera o resultado em um relatório.
- **-p/--split**: Diferente de ** --report**, o **-p/--split** lista o resultado de cada rastreamento separadamente.
- **-c/--report-cycles**: define o a quantidade de pacotes de dados enviados por segundo. O padrão é 10.
- **-s/--psize**: define o tamanho de cada pacote de dados.
- **-n/--no-dns**: desativa a resolução de nome de domínio para endereço IP.
- **-a/--address**: define o endereço IP do qual os pacotes de dados são enviados. É usado principalmente para cenários com um único host e vários endereços IP.
- **-4**：IPv4
- **-6**：IPv6

#### Casos de uso
Considere uma máquina local para o servidor (IP: 119.28.98.39) como exemplo.
Execute o seguinte comando para exportar o resultado do diagnóstico do MTR em um relatório.
```
mtr 119.28.98.39 -- report
```
Uma mensagem semelhante à abaixo é retornada:
```
[root@VM_103_80_centos ~]# mtr 119.28.98.39 -- report
Start: Mon Feb  5 11:33:34 2019
HOST:VM_103_80_centos            Loss%    Snt    Last    Avg    Best    Wrst    StDev
1.|-- 100.119.162.130             0.0%     10     6.5    8.4     4.6    13.7      2.9
2.|-- 100.119.170.58              0.0%     10     0.8    8.4     0.6     1.1      0.0
3.|-- 10.200.135.213              0.0%     10     0.4    8.4     0.4     2.5      0.6
4.|-- 10.200.16.173               0.0%     10     1.6    8.4     1.4     1.6      0.0
5.|-- 14.18.199.58                0.0%     10     1.0    8.4     1.0     4.1      0.9
6.|-- 14.18.199.25                0.0%     10     4.1    8.4     3.3    10.2      1.9
7.|-- 113.96.7.214                0.0%     10     5.8    8.4     3.1    10.1      2.1
8.|-- 113.96.0.106                0.0%     10     3.9    8.4     3.9    11.0      2.5
9.|-- 202.97.90.206               30.0%     10    2.4    8.4     2.4     2.5      0.0
10.|-- 202.97.94.77               0.0%     10     3.5    4.6     3.5     7.0      1.2
11.|-- 202.97.51.142              0.0%     10   164.7    8.4   161.3   165.3      1.2
12.|-- 202.97.49.106              0.0%     10   162.3    8.4   161.7   167.8      2.0
13.|-- ix-xe-10-2-6-0.tcore2.LVW 10.0%     10   168.4    8.4   161.5   168.9      2.3
14.|-- 180.87.15.25              10.0%     10   348.1    8.4   347.7   350.2      0.7
15.|-- 180.87.96.21               0.0%     10   345.0    8.4   343.4   345.0      0.3
16.|-- 180.87.96.142              0.0%     10   187.4    8.4   187.3   187.6      0.0
17.|-- ???                      100.0%     10     0.0    8.4     0.0     0.0      0.0
18.|-- 100.78.119.231             0.0%     10   187.7    8.4   187.3   194.0      2.5
19.|-- 119.28.98.39               0.0%     10   186.5    8.4   186.4   186.5      0.0
```
As principais informações de saída são as seguintes
- **Host:** O endereço IP ou o nome de domínio de um nó.
- **Loss%:** a perda de pacotes.
- **Snt:** a quantidade de pacotes de dados enviados por segundo.
- **Last:** o último tempo de resposta.
- **Avg:** o tempo médio de resposta.
- **Best:** o menor tempo de resposta.
- **Wrst:** o maior tempo de resposta.
- **StDev:** o desvio padrão. Um desvio padrão mais alto indica uma diferença maior no tempo de resposta dos pacotes de dados neste nó.

### Análise de relatórios e solução de problemas
>? Devido à assimetria da rede, recomendamos que você colete dados do MTR bidirecionais (da máquina local para o servidor de destino e do servidor de destino para a máquina local) se ocorrer algum erro de rede.
>
1. De posse do relatório, verifique se há perda de pacotes no IP de destino.
 - Se não houver, as condições da rede estão normais.
 - Se houver, execute a [Etapa 2](#step02).
2. <span id="step02">Verifique o resultado para localizar em qual nó ocorre a primeira perda de pacote.</span>
 - Se a perda ocorreu no servidor de destino, pode ter sido causada por configuração incorreta de rede do servidor de destino. Verifique a configuração do firewall.
 - Se a perda ocorreu nos três primeiros hops (transferência de pacotes entre dispositivos), ela pode ter sido causada por problemas de rede do ISP da máquina local. Se o problema também ocorrer quando ao acessar outros endereços, entre em contato com o seu ISP (Provedor de Serviço de Internet).
 - Se a perda de pacotes ocorreu em hops próximos ao servidor de destino, ela pode ter sido causada por problemas de rede do ISP do próprio servidor de destino. [Envie um tíquete](https://console.cloud.tencent.com/workorder/category) para relatar o problema.
 Ao enviar o ticket, anexe capturas de tela dos resultados do teste do MTR da máquina local para o servidor de destino e do servidor de destino para a máquina local.
