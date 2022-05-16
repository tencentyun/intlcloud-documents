## Prevenção de ataques DDoS
Ao usar a rede pública para se conectar e acessar uma instância do TencentDB for MySQL, você pode sofrer ataques DDoS. Para resolver esse problema, a Tencent Cloud fornece funcionalidades de limpeza e bloqueio de tráfego que são acionadas e interrompidas automaticamente pelo sistema. Quando o sistema Anti-DDoS detecta que sua instância está sob ataques, ele ativará automaticamente a limpeza de tráfego ou bloqueará o tráfego se os ataques não puderem ser resistidos pela limpeza ou atingirem o limite de bloqueio.
>!Recomendamos acessar suas instâncias do TencentDB for MySQL pela rede privada para evitar ataques DDoS.

### Limpeza de tráfego
Quando o tráfego de rede pública de uma instância do TencentDB for MySQL exceder o limite, o Anti-DDoS limpará automaticamente o tráfego de entrada para a instância. O roteamento baseado em política será usado para redirecionar o tráfego da rota de rede original para os dispositivos de limpeza DDoS do Anti-DDoS, que identificarão o tráfego da rede pública, descartarão o tráfego de ataque e encaminharão o tráfego normal para a instância.

### Bloqueio
Quando o tráfego de ataque sofrido por uma instância do TencentDB for MySQL exceder o limite de bloqueio, a Tencent Cloud bloqueará todas as solicitações de acesso à rede pública para essa instância por meio de serviços de ISP aplicáveis, a fim de evitar que outros usuários da Tencent Cloud sejam afetados. Isso significa que quando a largura de banda do tráfego de ataque sofrido por sua instância exceder a largura de banda máxima de proteção, a Tencent Cloud bloqueará todas as solicitações de acesso à rede pública a ela.
- Quando as seguintes condições forem atendidas, o bloqueio será acionado:
 - O valor de bits por segundo (bps) atinge 2 Gbps.
 - A limpeza do tráfego não é eficaz.
- Quando a seguinte condição for atendida, o bloqueio será interrompido:
 - Passam-se 2 horas após o início do bloqueio.
