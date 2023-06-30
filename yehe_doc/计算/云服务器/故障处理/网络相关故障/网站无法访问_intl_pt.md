Este documento descreve como localizar e solucionar os problemas que causam a falha de acesso a sites.

## Possíveis causas

A falha de acesso a sites pode ser causada por problemas de rede, configurações de firewall ou sobrecarga do CVM.

## Solução de problemas
<span id="TroubleshootServer"></span>
### Solução problemas do CVM
O desligamento do CVM, a falha de hardware e o alto uso de CPU/memória/largura de banda podem causar falha de acesso a sites. Assim, recomendamos que você verifique o status de execução do CVM e o uso de CPU/memória/largura de banda.

1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm/index) e verifique se o status de execução da instância do CVM está normal na página de gerenciamento de instâncias, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/c8347dcc04834aa44ade7324b7012d73.png)
 - Se estiver, realize a [Etapa 2](#Server_step02).
 - Se não estiver, reinicie a instância do CVM.
2. <span id="Server_step02">Clique no ID/nome da instância para acessar sua página de detalhes.</span>
3. Selecione a guia **Monitoring (Monitoramento)** para exibir o uso de recursos da instância, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/b8396a4507dd6a9808f9907b90e881fa.png)
 - Se o uso de CPU/memória for muito alto, consulte [Falha ao fazer login em um CVM do Windows devido ao alto uso de CPU e memória](https://intl.cloud.tencent.com/document/product/213/32405) e [Falha ao fazer login em um CVM do Linux devido ao alto uso de CPU e memória](https://intl.cloud.tencent.com/document/product/213/32387) para solucionar o problema.
 - Se o uso da largura de banda for muito alto, consulte [Falha ao fazer login devido à alta ocupação da largura de banda](https://intl.cloud.tencent.com/document/product/213/32542) para solucionar o problema.
 - Se o uso de CPU/memória/largura de banda estiver normal, realize a [etapa 4](#Server_step04).
4. <span id="Server_step04">Execute o comando a seguir para verificar se a porta de serviço da Web correspondente está sendo monitorada normalmente. </span>
> As operações a seguir usam a porta 80, que é comumente usada no serviço HTTP, como exemplo.
>
 - Para uma instância do Linux: execute o comando `netstat -ntulp |grep 80`, conforme mostrado abaixo:
 ![](https://mc.qcloudimg.com/static/img/ab5fa663197c3fa0738b2ceb3f559fd3/image.png)
 - Para uma instância do Windows: abra a ferramenta de linha de comando CMD para executar o comando `netstat -ano|findstr :80`, conforme mostrado abaixo:
 ![](https://mc.qcloudimg.com/static/img/c9c32a2e9f12235ad3d2a5aca313f298/image.png)
 - Se a porta estiver sendo monitorada normalmente, realize a [etapa 5](#Server_step05).
 – Se a porta não estiver sendo monitorada normalmente, verifique se o processo de serviço da Web foi iniciado ou configurado corretamente.
5. <span id="Server_step05">Verifique se a porta de serviço da Web correspondente está aberta na configuração do firewall.</span>
 - Para uma instância do Linux: execute o comando `iptables -vnL` para verificar se o iptables abre a porta 80.
    - Se a porta 80 for aberta, [solucione problemas relacionados à rede](#TroubleshootNetwork).
    - Se a porta 80 não for aberta, execute o comando `iptables -I INPUT 5 -p tcp  --dport 80 -j ACCEPT` para abri-la.
 - Para uma instância do Windows: clique em **Start (Iniciar)** > **Control Panel (Painel de Controle)** > **Windows Firewall (Firewall do Windows)** na interface do SO para verificar se a configuração do firewall do Windows está desativada.
		- Se estiver, [solucione problemas relacionados à rede](#TroubleshootNetwork).
		- Se não estiver, desative a configuração do firewall do Windows.

<span id="TroubleshootNetwork"></span>
### Solução de problemas relacionados à rede
Os problemas de rede também podem causar falha de acesso à rede. Você pode executar o comando a seguir para verificar se a rede tem perda de pacotes ou alta latência.
```
ping the public IP of the server
```
- Se um resultado semelhante ao abaixo for retornado, há perda de pacotes ou alta latência. Use o MTR para solução de problemas. Para mais informações, consulte [Latência da rede e perda de pacotes do CVM](https://intl.cloud.tencent.com/document/product/213/14638).
![](https://mc.qcloudimg.com/static/img/30d9946522f43cfc1c6731b9035ae9e9/image.png)
- Se não houver perda de pacotes ou alta latência, [solucione problemas de grupo de segurança](#TroubleshootSecurityGroup).

<span id="TroubleshootSecurityGroup"></span>
### Solução de problemas de grupo de segurança
Um grupo de segurança é um firewall virtual que permite que você controle o tráfego de entrada e saída da instância associada. Você pode especificar protocolos, portas e políticas para regras de grupo de segurança. Se você não abriu as portas relacionadas aos processos da Web, pode ocorrer falha de acesso a sites.
1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm/index) e clique no ID/nome da instância para acessar a sua página de detalhes.
2. Clique na guia **Security Group (Grupo de segurança)** para exibir os grupos de segurança vinculados e suas regras de saída e entrada. Confirme se as portas relacionadas aos processos da Web estão abertas, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/b5782326fcdd77a74ca1435b202ca97b.png)


