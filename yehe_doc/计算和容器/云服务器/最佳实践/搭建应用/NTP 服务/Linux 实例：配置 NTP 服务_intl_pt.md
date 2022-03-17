## Visão geral

O daemon do Network Time Protocol (ntpd) é um daemon do sistema operacional Linux. É uma implementação completa do NTP e é usado para corrigir a diferença de horário entre o sistema local e o servidor de origem do relógio. Ao contrário do ntpdate, que atualiza o tempo periodicamente, o ntpd corrige o tempo continuamente, sem intervalos de tempo. Este documento usa o CentOS 7.5 como exemplo para descrever como instalar e configurar o ntpd.

## Observações

- Alguns sistemas operacionais usam o chrony como o serviço NTP padrão. Certifique-se de que o ntpd esteja em execução e configurado para ativar automaticamente na inicialização.
 - Execute o comando `systemctl is-active ntpd.service` para conferir se o ntpd está em execução.
 - Execute o comando `systemctl is-enabled ntpd.service` para conferir se o ntpd está configurado para ativar automaticamente na inicialização.
- A porta de comunicação do serviço NTP é UDP 123. Certifique-se de ter aberto a porta para a Internet antes de configurar o serviço NTP.
Se a porta não estiver aberta, consulte [Adicionar regras de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272) para abri-la para a Internet.

## Instruções

### Instalação do ntpd

Execute o seguinte comando para verificar se o ntpd foi instalado.
```
rpm -qa | grep ntp
```
 - Se o seguinte resultado for retornado, o ntpd foi instalado.
![Verificação de instalação do ntpd](https://main.qcloudimg.com/raw/34073904c49e80ab61da25559c7239e5.png)
 - Se o ntpd não tiver sido instalado, execute o comando `yum install ntp` para instalá-lo. 
```
yum -y install ntp
```
O ntpd usa o modo cliente por padrão.

### Configuração do NTP
1. Execute o seguinte comando para abrir o arquivo de configuração do serviço NTP.
```
vi /etc/ntp.conf
```
2. Pressione **i** para alternar para o modo de edição e localizar as configurações do `server`. Altere o valor de `server` para o servidor de origem do relógio NTP que você deseja usar (como `time1.tencentyun.com`) e exclua os valores indesejados, conforme mostrado abaixo:
![Configuração do servidor](https://main.qcloudimg.com/raw/b21b559ce745ef5c765251a8ee514dca.png)
3. Pressione **Esc** e digite **:wq** para salvar e fechar o arquivo.

### Ativação do ntpd

Execute o seguinte comando para reiniciar o serviço ntpd.
```
systemctl restart ntpd.service
```

### Verificação de status do ntpd

Execute os comandos a seguir para verificar o status do ntpd conforme necessário. 
- Execute o seguinte comando para verificar se o NTP está escutando normalmente na porta de serviço UDP 123.
```
netstat -nupl
```
Se o resultado a seguir for retornado, a escuta está normal.
![netstat -nupl](https://main.qcloudimg.com/raw/d7da764d05135959154920b81fa9f1e4.png)
- Execute o seguinte comando para verificar se o status do ntpd está normal.
```
service ntpd status
```
Se o resultado a seguir for retornado, o status do ntpd está normal.
![ntpd status](https://main.qcloudimg.com/raw/321e56d0f7797f382d9f6903c0315f96.png)
- Execute o seguinte comando para verificar se o NTP foi iniciado normalmente e se foi configurado para o servidor de origem do relógio NTP correto.
```
ntpstat
```
O endereço IP do servidor de origem do relógio NTP atual, que foi configurado anteriormente, deve ser retornado, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/a99f5da438bafb1d148e9b033f48afad.png)
Você também pode obter o endereço IP correspondente ao nome de domínio executando o comando `nslookup domain name`.
- Execute o seguinte comando para obter informações mais detalhadas sobre o serviço NTP.
```
ntpq -p
```
O seguinte resultado será retornado:
![](https://main.qcloudimg.com/raw/ca9ef4caf98b49ed2c9110198a66e7c3.png)
 - **remote**: o nome do servidor NTP que responde a esta solicitação.
 - **refid**: o servidor NTP um estrato acima daquele ao qual o servidor NTP, neste estrato, está sincronizado.
 - **st**: o estrato do servidor remoto. O estrato de um servidor pode ser definido de 1 a 16 de alto a baixo. Para aliviar a carga e o congestionamento da rede, você deve evitar conectar-se diretamente a um servidor estrato 1.
 - **when**: o número de segundos decorridos desde a última solicitação bem-sucedida.
 - **poll**: o intervalo de sincronização (em segundos) entre os servidores locais e remotos. No início, o valor `poll` será menor, o que indica uma maior frequência de sincronização, para que o tempo possa ser ajustado para o intervalo de tempo correto o mais rápido possível. Mais tarde, o valor `poll` aumentará de modo gradual e, consequentemente, a frequência de sincronização diminuirá.
 - **reach**: um valor octal usado para testar se o servidor pode ser conectado. Seu valor aumenta sempre que o servidor é conectado com sucesso.
 - **delay**: o tempo de ida e volta de envio da solicitação de sincronização da máquina local para o servidor NTP.
 - **offset**: a diferença de tempo em milissegundos (ms) entre o host e a origem do horário por meio do NTP. Quanto mais próximo o offset estiver de 0, mais próximos serão os horários do host e do servidor NTP.
 - **jitter**: um valor usado para estatísticas que registra a distribuição de offsets em um determinado número de conexões consecutivas. Quanto menor for o valor absoluto, mais preciso será o horário do host.

### Configuração da ativação automática do ntpd na inicialização

1. Execute o seguinte comando para ativar automaticamente o ntpd na inicialização.
```
systemctl enable ntpd.service
```
2. Execute o seguinte comando para verificar se o chrony está definido para ativar na inicialização.
```
systemctl is-enabled chronyd.service
```
Se o chrony estiver definido para ativar na inicialização, execute o seguinte comando para removê-lo da lista de inicialização automática.
O chrony não é compatível com ntpd, o que pode causar falha de inicialização do ntpd.
```
systemctl disable chronyd.service
```

### Melhora da segurança do ntpd

Execute os seguintes comandos sequencialmente para aumentar a segurança do arquivo de configuração `/etc/ntp.conf`.
```
interface ignore wildcard
```
```
interface listen eth0
```
