### Como ajusto o intervalo de sincronização do serviço NTP configurado?
Após [configurar o serviço NTP em uma instância do Linux](https://intl.cloud.tencent.com/document/product/213/32381), você pode reiniciar o ntpd para redefinir o intervalo de sincronização. Para definir manualmente o intervalo de sincronização do ntpd, realize as seguintes etapas:
1. Execute o comando a seguir para modificar o arquivo de configuração do NTP.
```
vi /etc/ntp.conf
```
2. Pressione **i** para entrar no modo de edição e configure da seguinte forma:
  1. Adicione o sinal de libra (`#`) no início de `server time1.tencentyun.com iburst`, se houver, para comentar.
  2. Adicione as configurações a seguir. Em que, `minpoll 4` significa que o intervalo mínimo é 2<sup>4</sup>, e `maxpoll 5` significa que o intervalo máximo é 2<sup>5</sup>.
```
server time1.tencentyun.com minpoll 4 maxpoll 5
```
O resultado deve ser o seguinte. Digite **:wq** para salvar as alterações e fechar o arquivo.
![](https://main.qcloudimg.com/raw/02d6457d29b4c573605e3c79c5ccfc9f.png)
3. Reinicie o ntpd e execute `ntpd -p`. O valor de `poll` que você verá é 16 (ou seja, 2<sup>4</sup>), conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/9fa0c72751de74d3b6e72cc1ca831952.png)

### Qual é a fonte de hora dos servidores ntp da Tencent Cloud?
Normalmente, os servidores NTP usam o relógio do satélite BeiDou.
 
### O que devo fazer quando a configuração do NTP relata o erro `localhost.localdomain timeout`?
O erro é como mostrado na figura a seguir.
![](https://main.qcloudimg.com/raw/1b3158135475e6cfbee28d2373685616.png)
Verifique e confirme se você executou `POSTROUTING`. Se sim, altere o IP de origem no arquivo de configuração `ntp.conf` para o endereço IP de eth0.

### Os servidores fora da nuvem podem compartilhar um NTP com as CVMs da Tencent Cloud? Qual é o endereço de sincronização do NTP?
A Tencent Cloud fornece servidores NTP privados para recursos da Tencent Cloud. Para outros dispositivos, você pode usar os servidores NTP públicos fornecidos pela Tencent Cloud para sincronização.
- Servidores NTP privados em:
```
time1.tencentyun.com
time2.tencentyun.com
time3.tencentyun.com
time4.tencentyun.com
time5.tencentyun.com
```
- Servidores NTP públicos em:
```
time1.cloud.tencent.com 
time2.cloud.tencent.com 
time3.cloud.tencent.com
time4.cloud.tencent.com
time5.cloud.tencent.com
```

### Por que a hora de uma instância da CVM criada a partir de uma imagem personalizada está incorreta?
Verifique se o serviço NTP está ativado. Para usar a funcionalidade de sincronização NTP posteriormente, consulte o documento a seguir de acordo com o sistema operacional para definir o NTP. Depois, recrie a imagem personalizada.
 - [Definir o serviço NTP em uma instância do Linux](https://intl.cloud.tencent.com/document/product/213/32381)
 - [Definir o serviço NTP em uma instância do Windows](https://intl.cloud.tencent.com/document/product/213/32380)

### A sincronização do NTP será afetada se uma CVM não conseguir executar ping no servidor NTP?
Não. Desde que você consiga acessar o NTP, a sincronização funciona. 

### Por que o conteúdo de ntp.conf de uma CVM criado a partir de uma imagem personalizada foi restaurado?
Pode ter sido causado pela inicialização do Cloud-Init. Exclua as configurações relacionadas ao NTP em `/etc/cloud/cloud.cfg` antes de criar uma imagem personalizada. Para mais informações, consulte [Cloud-init e cloudbase-init](https://intl.cloud.tencent.com/document/product/213/19670).

### Que impacto terá um DNS de rede privada modificado?
Todos os serviços que envolvem a resolução de nomes de domínio privado da Tencent Cloud serão afetados. Por exemplo,
- O repositório YUM usa o nome de domínio privado da Tencent Cloud. Você precisa modificar o repositório YUM após alterar o DNS.
- O relatório de dados de monitoramento usa o nome de domínio privado e será afetado.
- A funcionalidade NTP depende do nome de domínio privado para sincronizar a hora do servidor e será afetada.

### Por que o horário local de uma instância do Windows é redefinido do EST configurado para o horário de Pequim após a reinicialização?
Verifique se o serviço windowstime está habilitado na instância. Talvez seja necessário habilitá-lo manualmente para sincronizar automaticamente a hora do sistema da instância. Recomendamos habilitar a inicialização automática do serviço.

### Por que não posso usar o comando `ntpq -np` para exibir a hora da sincronização?
O erro é como mostrado na figura a seguir.
![](https://main.qcloudimg.com/raw/88972a2aeda155c10000e8576d16bbe9.png)
Verifique se nenhum IP ou um IP incorreto está configurado para `listen` no arquivo de configuração `/etc/ntp.conf`. Altere para o IP privado principal da instância e reinicie o ntpd.

### Como faço para corrigir o erro ocorrido ao usar os servidores NTP públicos para sincronizar a hora?
O erro `no server suitable for synchronization found (não foi encontrado nenhum servidor adequado para sincronização)` é exibido, conforme a figura a seguir.
![](https://main.qcloudimg.com/raw/1909910bc2a86a5f93e09f4601654327.png)
Pode ter sido causado pela política de proteção do NTP em resposta aos ataques DDoS ao endereço IP público da instância. Essa política bloqueia todo o tráfego de entrada público no ponto de origem 123 da Tencent Cloud e causa exceção de sincronização. Recomendamos tentar usar os servidores NTP privados para sincronizar a hora.
