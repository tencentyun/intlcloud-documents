## Problema

Um servidor local não consegue executar o ping em uma instância. As possíveis causas incluem:
- Configuração incorreta do servidor de destino
- Falha na resolução de nome de domínio
- Falha de vinculação

Se a rede local estiver normal (outros sites podem receber ping da rede local), solucione o problema da seguinte maneira:
- [Verifique se a instância está configurada com um endereço IP público](#isConfigurePublicIP).
- [Verifique a configuração do grupo de segurança](#CheckSecurityGroupSetting).
- [Verifique a configuração do sistema operacional](#CheckOSSetting).
- [Realize outras operações](#OtherOperations).

## Instruções

<span id="isConfigurePublicIP"></span>
### Verificar se a instância está configurada com um endereço IP público

> Uma instância pode acessar outros computadores na Internet somente se tiver um endereço IP público. Caso contrário, a instância não poderá receber ping fora do endereço IP privado.
>
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página “Instances (Instâncias)”, selecione o ID/nome da instância para executar o ping e acessar a página de detalhes da instância, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/12dfabc6420688ebb0dd0f1a8f4d7188.png)
3. Verifique se a instância está configurada com um endereço IP público em “Network Information (Informações de rede)”.
 - Se estiver, [verifique a configuração do grupo de segurança](#CheckSecurityGroupSetting).
 - Se não estiver, [vincule um endereço IP público elástico à instância](https://intl.cloud.tencent.com/document/product/213/16586).

<span id="CheckSecurityGroupSetting"></span>
### Verificar a configuração do grupo de segurança

Um grupo de segurança é um firewall virtual que controla o tráfego de entrada e saída da instância associada. Você pode especificar o protocolo, a porta e a política em uma regra de grupo de segurança. Como o ICMP é usado no teste de ping, será necessário verificar se o protocolo é permitido no grupo de segurança associado à instância. Para exibir o grupo de segurança associado à instância e suas regras de entrada e saída, execute as seguintes etapas:
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página “Instances (Instâncias)”, selecione o ID/nome da instância a ser configurada com um grupo de segurança para acessar a página de detalhes da instância, de acordo com a figura a seguir:
3. Clique na guia **Security Groups (Grupos de segurança)** para acessar a página de gerenciamento do grupo de segurança desta instância, conforme a figura a seguir:
![](https://main.qcloudimg.com/raw/bf5881258356a0af748ae16d9cf321a2.png)
4. Verifique o grupo de segurança associado à instância e as regras detalhadas de entrada e saída para determinar se esse grupo de segurança permite o ICMP.
 - Se sim, [verifique a configuração do sistema operacional](#CheckOSSetting).
 - Caso contrário, configure a política do protocolo ICMP para permitir.

<span id="CheckOSSetting"></span>
### Verificar a configuração do sistema operacional

Com base no sistema operacional da instância, selecione um método para verificar a configuração:
- Para o sistema operacional Linux, [verifique os parâmetros do kernel do Linux e as configurações de firewall](#CheckLinux).
-Para o sistema operacional Windows, [verifique a configuração do firewall do Windows](#CheckLinux).

<span id="CheckLinux"></span>
#### Verificar os parâmetros do kernel do Linux e as configurações do firewall

> Se um teste de ping é permitido no sistema operacional Linux depende das configurações do kernel e do firewall. Se qualquer um deles negar o teste de ping, ocorrerá “Request timeout (Tempo limite da solicitação)”.

##### Verificar o parâmetro do kernel icmp_echo_ignore_all

1. Faça login na instância.
2. Execute o comando a seguir para exibir a configuração do sistema icmp_echo_ignore_all.
```
cat /proc/sys/net/ipv4/icmp_echo_ignore_all
```
 - Se 0 for retornado, todas as solicitações de Eco ICMP são permitidas pelo sistema. Neste caso, [verifique a configuração do firewall](#CheckLinuxFirewall).
 - Se 1 for retornado, todas as solicitações de Eco ICMP são negadas pelo sistema. Nesse caso, realize a [etapa 3](#Linux_step03).
3. <span id = "Linux_step03"> Execute o comando a seguir para modificar a configuração do parâmetro do kernel icmp_echo_ignore_all.</ span>
```
echo "0" >/proc/sys/net/ipv4/icmp_echo_ignore_all
```

<span id="CheckLinuxFirewall"></span>
##### Verificar a configuração do firewall

Execute o comando a seguir para verificar se a regra de firewall e a regra do ICMP correspondente do servidor atual estão desativadas:
```
iptables -L
```
- Se o resultado a seguir for retornado, a regra do ICMP não está desativada. Nesse caso, [verifique se o nome de domínio tem arquivamento ICP](#CheckDomainRegistration) (para nomes de domínio da China Continental).
```
Chain INPUT (policy ACCEPT)
target     prot opt source               destination         
ACCEPT     icmp --  anywhere             anywhere             icmp echo-request
Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         
Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination  
ACCEPT     icmp --  anywhere             anywhere             icmp echo-request
```
- Se o resultado do retorno mostrar que a regra do ICMP está desativada, execute os comandos a seguir para ativá-la.
```
#Chain INPUT
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
#Chain OUTPUT
iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT
```

<span id="CheckWindows"></span>
#### Verificar a configuração do firewall do Windows

1. Faça login na instância.
2. Abra o **Control Panel (Painel de controle)** e selecione **Windows Firewall (Firewall do Windows)**.
3. Nessa página, selecione **Advanced settings (Configurações avançadas)**.
4. Na janela pop-up “Windows Firewall with Advanced Security (Firewall do Windows com segurança avançada)”, verifique se as regras de entrada e saída do ICMP estão desativadas.
 - Se elas estiverem desativadas, ative-as.


<span id="OtherOperations"></span>
### Outras operações

Se as operações anteriores não puderem solucionar o problema, consulte o seguinte:
- Se não for possível executar o ping no nome de domínio, verifique a configuração do seu site.
- Se não for possível executar o ping no endereço IP público, anexe informações sobre a instância e os dados bidirecionais do MTR (do servidor local para o CVM e do CVM para o servidor local) e [envie um ticket](https://console.cloud.tencent.com/workorder/category) para entrar em contato com nossos engenheiros e obter ajuda.
Para mais informações sobre como usar o MTR, consulte [Latência da rede e perda de pacotes do CVM](https://intl.cloud.tencent.com/document/product/213/14638).
