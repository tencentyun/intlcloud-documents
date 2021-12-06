## Visão geral de grupos de segurança do CVM
Um [grupo de segurança](https://intl.cloud.tencent.com/document/product/213/12452) pode ser usado para o controle de acesso de servidores de back-end de instâncias do CLB, que atua como um firewall.
Você pode associar um ou mais grupos de segurança a um servidor de back-end e, depois, adicionar uma ou mais regras a cada grupo para controlar as permissões de acesso ao tráfego de servidores diferentes. É possível modificar as regras de um grupo de segurança a qualquer momento, e as novas regras serão aplicadas automaticamente a todas as instâncias associadas ao grupo. Para obter mais informações, consulte o [Guia de operações de grupos de segurança](https://intl.cloud.tencent.com/document/product/213/12452). No ambiente do [VPC](https://intl.cloud.tencent.com/document/product/215/535), você também pode usar [ACL de rede](https://intl.cloud.tencent.com/document/product/215/31850) para controle de acesso.

## Descrição da configuração de grupos de segurança do CVM
O IP do cliente e a porta de serviço precisam ser abertos para a internet no grupo de segurança do CVM.
Se você deseja usar o CLB para encaminhar o tráfego de negócios para o CVM, o grupo de segurança do CVM deve ser configurado da seguinte forma para garantir verificações de integridade eficazes:
1. CLB da rede pública: é necessário abrir o VIP do CLB para a internet no grupo de segurança do CVM de back-end, para que o CLB possa usar o VIP para detectar o status de integridade do CVM de back-end.
2. CLB da rede privada:
 - Para o CLB da rede privada (anteriormente conhecido como "CLB do aplicativo da rede privada"), se sua instância do CLB estiver em um VPC, o VIP do CLB precisa ser aberto para a internet no grupo de segurança do CVM de back-end para verificações de integridade; se sua instância do CLB estiver na rede básica, nenhuma configuração adicional é necessária, pois o IP de verificação de integridade fica aberto para a internet por padrão.
 - Para o CLB clássico da rede privada, se sua instância do CLB foi criada antes de 5 de dezembro de 2016 e está em um VPC, o VIP do CLB precisa ser aberto para a internet (para verificações de integridade) no grupo de segurança do CVM de back-end; caso contrário, nenhuma configuração é necessária.

## Exemplos da configuração de grupos de segurança do CVM
Os exemplos a seguir mostram como configurar grupos de segurança do CVM, ao acessá-lo por meio do CLB. Se você também configurou um grupo de segurança no CLB, consulte [Configuração de grupos de segurança do CLB
](https://intl.cloud.tencent.com/document/product/214/14733) para obter mais informações sobre como configurar regras de grupo de segurança do CLB.
- **Cenário de aplicação 1:**
Se uma instância do CLB da rede pública for configurada com um listener TCP:80, a porta do servidor de back-end for 8080, e você desejar que apenas alguns IPs do cliente (ClientA IP e ClientB IP) acessem a instância do CLB, configure as regras de entrada do grupo de segurança do servidor de back-end da seguinte forma:
```
 ClientA IP + 8080 allow
 ClientB IP + 8080 allow
 CLB VIP    + 8080 allow
 0.0.0.0/0  + 8080 drop
```
- **Cenário de aplicação 2:**
Se uma instância do CLB da rede pública for configurada com um listener HTTP:80, a porta do servidor de back-end for 8080, e você desejar que todos os IPs do cliente acessem a instância do CLB, configure as regras de entrada do grupo de segurança do servidor de back-end da seguinte forma:
```
 0.0.0.0/0 + 8080 allow
```
- **Cenário de aplicação 3:**
Para uma instância do CLB da rede privada (anteriormente conhecido como "CLB do aplicativo da rede privada"), se o tipo de rede for VPC, o grupo de segurança do CVM precisará abrir o IP do VIP do CLB para a internet para verificação de integridade. E se esta instância do CLB for configurada com um listener TCP:80, a porta do servidor de back-end for 8080, e você desejar que determinados IPs do cliente (ClientA IP e ClientB IP) acessem o VIP do CLB e que os IPs do cliente acessem apenas servidores de back-end vinculados à instância do CLB:
a. Configure as regras de entrada para o grupo de segurança do servidor de back-end da seguinte forma:
```
 ClientA IP + 8080 allow
 ClientB IP + 8080 allow
 CLB VIP    + 8080 allow
 0.0.0.0/0  + 8080 drop
```
a. Configure as regras de saída para o grupo de segurança do servidor do cliente da seguinte forma:
```
 CLB VIP    + 8080 allow
 0.0.0.0/0  + 8080 drop
```
- **Cenário de aplicação 4:**
Para uma instância do CLB clássico da rede privada (ou seja, uma instância do CLB do VPC adquirida após 5 de dezembro de 2016), se o grupo de segurança CVM precisar apenas abrir o IP do cliente para a internet (não houver necessidade de abrir o VIP do CLB, e o IP de verificação de integridade estiver aberto por padrão), esta instância do CLB for configurada com um listener TCP:80, a porta do servidor de back-end for 8080 e você desejar que determinados IPs do cliente (ClientA IP e ClientB IP) acessem o VIP do CLB e que os IPs do cliente acessem apenas servidores de back-end vinculados à instância do CLB:
a. Configure as regras de entrada para o grupo de segurança do servidor de back-end da seguinte forma:
```
 ClientA IP + 8080 allow
 ClientB IP + 8080 allow
 0.0.0.0/0  + 8080 drop
```
a. Configure as regras de saída para o grupo de segurança do servidor do cliente da seguinte forma:
```
 CLB VIP    + 8080 allow
 0.0.0.0/0  + 8080 drop
```
- **Cenário de aplicação 5: lista de bloqueio**
Se você precisar configurar uma lista de bloqueio para alguns IPs de cliente negarem suas solicitações de acesso, pode configurar o grupo de segurança associado aos serviços do Tencent Cloud. As regras do grupo de segurança precisam ser configuradas da seguinte forma:
 - Adicione o IP do cliente e a porta a serem rejeitados no grupo de segurança e selecione a opção na coluna "Policy (Política)", para rejeitar o acesso desse IP.
 - Adicione outra regra de grupo de segurança depois de concluir a configuração acima, para permitir solicitações de acesso à porta de todos os IPs por padrão.
Depois que a configuração for concluída, as regras do grupo de segurança serão conforme abaixo:

```
 clientA IP + port drop
 clientB IP + port drop
 0.0.0.0/0  + port accept
```

>?
>- As etapas de configuração acima devem ser executadas **na ordem correta**; caso contrário, a configuração da lista de bloqueio não terá efeito.
>- Os grupos de segurança têm monitoração de estado; portanto, as configurações acima são usadas para **regras de entrada**, já as regras de saída não requerem configuração especial.

## Guia de operações de grupos de segurança do CVM
### Gerenciamento de grupos de segurança do servidor de back-end no console
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/loadbalance) e clique no ID da instância correspondente para acessar a página de detalhes.
2. Na página do CVM, clique no ID do servidor de back-end correspondente para acessar a página de detalhes da instância do CVM.
3. Clique na guia **Security Group (Grupo de segurança)** para vincular/desvincular o grupo de segurança.

### Gerenciamento de grupos de segurança do servidor de back-end pela API do TencentCloud
Para obter mais informações, consulte [AssociateSecurityGroups](https://intl.cloud.tencent.com/document/product/213/33265) e [DisassociateSecurityGroups](https://intl.cloud.tencent.com/document/product/213/33253).
