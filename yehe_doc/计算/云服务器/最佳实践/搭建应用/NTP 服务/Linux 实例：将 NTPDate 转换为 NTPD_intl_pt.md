## Visão geral

O ntpdate é uma atualização de ponto de interrupção para a sincronização de tempo de suas novas instâncias. O ntpd é um daemon passo a passo para a sincronização de tempo de suas instâncias em execução. Este documento usa o sistema operacional CentOS 7.5 como exemplo para apresentar como fazer a transição de ntpdate para ntpd em CVMs.

## Pré-requisitos
O serviço NTP se comunica na porta UDP 123. Certifique-se de ter aberto a porta para a Internet antes de fazer a transição para o serviço NTP.
Se a porta não tiver sido aberta, consulte [Adicionar regras de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272) para abri-la na Internet.

## Instruções
É possível fazer a transição de ntpdate para ntpd [manualmente](#manual) ou [automaticamente](#automatic).
<span id="manual"></span>
### Transição manual de ntpdate para ntpd
#### Desligar o ntpdate
1. Execute o seguinte comando para exportar a configuração `crontab` e filtrar ntpdate.
```
crontab -l |grep -v ntpupdate > /tmp/cronfile
```
2. Execute o seguinte comando para atualizar a configuração ntpdate.
```
crontab /tmp/cronfile
```
3. Execute o seguinte comando para modificar o arquivo `rc.local`.
```
vim /etc/rc.local
```
4. Pressione **i** para alternar para o modo de edição e exclua a linha de configuração `ntpupdate`.
5. Pressione **Esc** e digite **:wq** para salvar e fechar o arquivo.

#### Configuração ntpd
1. Execute o seguinte comando para abrir o arquivo de configuração do serviço NTP.
```
vi /etc/ntp.conf
```
2. Pressione ** i ** para mudar para o modo de edição e localizar as configurações do `server`. Altere o valor de `server` para o servidor de origem do relógio NTP que você deseja usar (como `time1.tencentyun.com`) e exclua os valores indesejados, conforme mostrado abaixo:
![Configuração do servidor](https://main.qcloudimg.com/raw/643dc5bbd2a42307ec10b5d38f756dda.png)
3. Pressione **Esc** e digite **:wq** para salvar e fechar o arquivo.

<span id="automatic"></span>
### Transição automática de ntpdate para ntpd
1. Faça download do script `ntpd_enable.sh`.
```
wget https://image-10023284.cos.ap-shanghai.myqcloud.com/ntpd_enable.sh
```
2. Execute o seguinte comando para fazer a transição de ntpdate para ntpd usando o script `ntpd_enable.sh`.
```
sh ntpd_enable.sh
```

## Operações relevantes
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

- Execute o seguinte comando para obter informações mais detalhadas sobre o serviço NTP.
```
ntpq -p
```
O seguinte resultado será retornado:
![](https://main.qcloudimg.com/raw/ca9ef4caf98b49ed2c9110198a66e7c3.png)
 - **\***: o servidor NTP em uso atualmente.
 - **remote**: o nome do servidor NTP que responde a esta solicitação.
 - **refid**: o servidor NTP um estrato acima daquele ao qual o servidor NTP, neste estrato, está sincronizado.
 - **st**: o estrato do servidor remoto. O estrato de um servidor pode ser definido de 1 a 16 de alto a baixo. Para aliviar a carga e o congestionamento da rede, você deve evitar conectar-se diretamente a um servidor estrato 1.
 - **when**: o número de segundos decorridos desde a última solicitação bem-sucedida.
 - **poll**: o intervalo de sincronização (em segundos) entre os servidores local e remoto. No início, o valor `poll` será menor, o que indica uma maior frequência de sincronização, para que o tempo possa ser ajustado para o intervalo de tempo correto o mais rápido possível. Mais tarde, o valor `poll` aumentará de modo gradual e, consequentemente, a frequência de sincronização diminuirá.
 - **reach**: um valor octal usado para testar se o servidor pode ser conectado. Seu valor aumenta sempre que o servidor é conectado com sucesso.
 - **delay**: o tempo de ida e volta de envio da solicitação de sincronização da máquina local para o servidor NTP.
 - **offset**: a diferença de tempo em milissegundos (ms) entre o host e a origem do horário por meio do NTP. Quanto mais próximo o offset estiver de 0, mais próximos serão os horários do host e do servidor NTP.
 - **jitter**: um valor usado para estatísticas que registra a distribuição de offsets em um determinado número de conexões consecutivas. Quanto menor for o valor absoluto, mais preciso será o horário do host.
