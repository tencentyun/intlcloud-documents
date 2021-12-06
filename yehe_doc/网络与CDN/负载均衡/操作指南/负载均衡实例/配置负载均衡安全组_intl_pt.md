Depois que uma instância do CLB é criada, você pode configurar um grupo de segurança do CLB para isolar o tráfego da rede pública. Este documento descreve como configurar grupos de segurança do CLB em modos diferentes.
## Limites de uso
- É possível vincular uma instância do CLB a cinco grupos de segurança, no máximo.
- Até 512 regras são permitidas para um grupo de segurança.
- Não é possível vincular os grupos de segurança a instâncias do CLB baseadas na rede clássica privada e instâncias do CLB da rede clássica privada. Se uma instância do CLB da rede privada estiver vinculada a um [EIP anycast](https://intl.cloud.tencent.com/document/product/214/32426), os grupos de segurança vinculados à instância não terão efeito.
- **Allow by Default (Permitir por padrão)** não fica disponível para CLBs da rede clássica privada e CLBs baseados na rede clássica.

## Informações gerais
Um grupo de segurança é um firewall virtual que pode filtrar pacotes de dados com estado e controlar o tráfego de entrada e saída no nível da instância. Para obter mais informações, consulte o [Grupo de segurança](https://intl.cloud.tencent.com/document/product/213/12452).

Um grupo de segurança do CLB fica vinculado a uma instância do CLB, já um grupo de segurança do CVM fica vinculado a uma instância do CVM. Eles visam objetos diferentes. Para um grupo de segurança do CLB, você pode escolher:
- [Ativar **Allow by Default (Permitir por padrão)**](#open-security-group)
- [Desativar **Allow by Default (Permitir por padrão)**](#close-security-group)

>?
>- Para grupos de segurança do CLB IPv4, **Allow by Default (Permitir por padrão)** fica desativado por padrão, você pode ativá-lo no console.
>- Para grupos de segurança do CLB IPv6, **Allow by Default (Permitir por padrão)** fica ativado por padrão, e você não pode desativá-lo.


### Ativação de **Allow by Default (Permitir por padrão)**[](id:open-security-group)
![](https://main.qcloudimg.com/raw/0d2b50ca557d805ce5790fcdd3974b40.jpg)
Quando **Allow by Default (Permitir por padrão)** está ativado:
<ul ><li>Caso deseje permitir o acesso apenas a partir de um IP do cliente especificado, você <strong>precisa permitir</strong> o IP do cliente e a porta de escuta no grupo de segurança do CLB, porém você <strong>não precisa permitir</strong> o IP do cliente e a porta de serviço no grupo de segurança do CVM de back-end. O tráfego de acesso do CLB passa apenas pelo grupo de segurança do CLB, pois o servidor de back-end permite o tráfego do CLB por padrão.</li>
<li>O tráfego de IPs públicos (incluindo IPs públicos gerais e EIPs) ainda precisa passar pelo grupo de segurança do CVM.</li>
<li>Se uma instância do CLB não tiver nenhum grupo de segurança configurado, todo o tráfego será permitido e apenas as portas configuradas com listeners no VIP da instância do CLB podem ser acessadas; portanto, a porta de escuta permitirá o tráfego de todos os IPs.</li>
<li>Para rejeitar o tráfego de um IP do cliente especificado, é necessário configurar no grupo de segurança do CLB. A rejeição de um IP do cliente no grupo de segurança do CVM tem efeito apenas para o tráfego de IPs públicos (incluindo IPs públicos gerais e EIPs), mas <strong>não</strong> para o tráfego do CLB.</li></ul>


### Desativação de **Allow by Default (Permitir por padrão)**[](id:close-security-group)
![](https://main.qcloudimg.com/raw/9357f8d81a0027110bd6a977cda4aafc.jpg)
Quando **Allow by Default (Permitir por padrão)** está desativado:</p>
<ul ><li>Caso deseje permitir o acesso apenas do IP do cliente especificado, você <strong>precisa permitir</strong> o IP do cliente e a porta de escuta no grupo de segurança do CLB e <strong>também permitir</strong> o IP do cliente e a porta de serviço no grupo de segurança do CVM; portanto, o tráfego de negócios que passa pelo CLB será verificado duas vezes, pelo grupo de segurança do CLB e pelo grupo de segurança do CVM.</li>
<li>O tráfego de IPs públicos (incluindo IPs públicos gerais e EIPs) ainda precisa passar pelo grupo de segurança do CVM.</li>
<li>Se uma instância do CLB não tiver nenhum grupo de segurança configurado, apenas o tráfego que passa pelo grupo de segurança do CVM será permitido.</li>
<li>Você pode rejeitar o acesso ao grupo de segurança do CLB ou do CVM para rejeitar o tráfego de um IP do cliente especificado.</li></ul>

<p >Quando <b>Allow by Default (Permitir por padrão)</b> estiver desativado, o grupo de segurança do CVM deve ser configurado da seguinte forma para garantir uma verificação de integridade eficaz:</p>
<ol ><li>Configure o CLB de rede pública<br>Você precisa permitir o VIP do CLB no grupo de segurança do CVM de back-end, para que o CLB possa usar o VIP para detectar o status de integridade do CVM de back-end.</li>
<li>Configure o CLB de rede privada<ul><li>Para o CLB de rede privada (anteriormente conhecido como "CLB de aplicativo de rede privada"), se sua instância do CLB estiver em um VPC, o VIP do CLB precisa ser permitido no grupo de segurança do CVM de back-end para verificação de integridade; se sua instância do CLB estiver na rede clássica, nenhuma configuração adicional será necessária, pois o IP de verificação de integridade fica permitido por padrão.</li><li>Para o CLB de rede clássica privada, se sua instância do CLB foi criada antes de 5 de dezembro de 2016 e está em um VPC, o VIP do CLB precisa ser permitido (para verificação de integridade) no grupo de segurança do CVM de back-end; caso contrário, nenhuma configuração adicional será necessária, pois o IP de verificação de integridade fica permitido por padrão.</li></ul></li></ol>

## Instruções
No exemplo a seguir, o grupo de segurança é configurado para permitir apenas o tráfego de entrada para o CLB da porta 80, e o serviço é fornecido por meio da porta 8080 do CVM. Não há limite para os IPs do cliente.
> ! Para a instância do CLB de rede pública usada neste exemplo, o VIP do CLB precisa ser permitido no grupo de segurança do CVM de back-end para verificação de integridade. O IP atual está definido como `0.0.0.0/0`, o que significa que todos os IPs são permitidos.

### Etapa 1. Crie uma instância do CLB e listener e vincule-os a um CVM

Para obter mais informações, consulte [Introdução ao CLB](https://intl.cloud.tencent.com/document/product/214/8975). Um listener HTTP:80 é criado e vinculado a uma instância do CVM de back-end cuja porta de serviço é 8080 neste exemplo.
<img alt="" src="https://main.qcloudimg.com/raw/9ec487d62b6092e6f5b14c1791ef5f4e.png" >

### Etapa 2. Configure um grupo de segurança do CLB
1. Configure um grupo de segurança do CLB<br>Faça login no <a rel="nofollow" href="https://console.cloud.tencent.com/cvm/securitygroup">Console de grupo de segurança</a> para configurar uma regra. Na regra de entrada, permita solicitações da porta 80 de todos os IPs (ou seja, `0.0.0.0/0`) e rejeite o tráfego de outras portas.
> ?
> - As regras do grupo de segurança são filtradas para entrarem em vigor de cima para baixo. Se a nova regra entrar em vigor, outras regras serão negadas por padrão; portanto, preste atenção na ordem. Para obter mais informações, consulte a<a rel="nofollow" href="https://intl.cloud.tencent.com/document/product/215/38750">Visão geral de grupos de segurança</a>.
> - Um grupo de segurança possui regras de entrada e saída. A configuração acima se destina a restringir o tráfego de entrada e, portanto, é uma <strong>regra de entrada</strong>, já a regra de saída não precisa ser configurada.
>
  ![](https://main.qcloudimg.com/raw/65b035098c49c77f4a82eed799353bc4.png) 

2. Vincule o grupo de segurança à instância do CLB
 1. Faça login no [Console do CLB](https://console.cloud.tencent.com/loadbalance).
 2. Na página "Instance Management (Gerenciamento de instâncias)", clique no ID da instância do CLB em questão.
 3. Na página de detalhes da instância, clique na guia **Security Group (Grupo de segurança)** e clique em **Bind (Vincular)**, no módulo **Bound Security Groups (Grupos de segurança vinculados)**.
 4. Na janela **Configure Security Group (Configurar grupo de segurança)** exibida, selecione o grupo vinculado à instância do CLB e clique em **OK**.
       ![](https://main.qcloudimg.com/raw/8a9701e700a94ba55a9a650eb87b4456.png) 
     A configuração do grupo de segurança do CLB está concluída, o que só permite o acesso ao CLB a partir da porta 80.
     <img alt="" src="https://main.qcloudimg.com/raw/a32cd86653185a5138006757aab38075.png" >

### Etapa 3. Configure **Allow by Default (Permitir por padrão)**
Você pode escolher ativar ou desativar **Allow by Default (Permitir por padrão)** com configurações diferentes da seguinte forma:
- Método 1. Ative **Allow by Default (Permitir por padrão)**, para que o servidor de back-end não precise permitir a porta.
>?Essa funcionalidade não é compatível com o CLB da rede clássica privada e CLB na rede clássica.
- Método 2. Desative **Allow by Default (Permitir por padrão)**, e você também precisa permitir o IP do cliente (0.0.0.0/0 neste exemplo) no grupo de segurança do CVM.

#### Método 1. Ative **Allow by Default (Permitir por padrão)**
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/loadbalance).
2. Na página **Instance Management (Gerenciamento de instâncias)**, clique no ID da instância do CLB em questão.
3. Na página de detalhes da instância, clique na guia **Security Group (Grupo de segurança)**.
2. Nessa guia, clique em <img style="margin:-3px 0px" src="https://main.qcloudimg.com/raw/5ba06490364505efc4d698e3adb1064e.png"> para ativar **Allow by Default (Permitir por padrão)**.
3. Quando **Allow by Default (Permitir por padrão)** estiver ativado, apenas as regras do grupo de segurança na <strong>visualização da regra</strong>, conforme mostrado abaixo, precisam ser verificadas.
    ![](https://main.qcloudimg.com/raw/6caa47138ecb97cc3c60cb38971792fd.png)

#### Método 2. Desative **Allow by Default (Permitir por padrão)**
Se **Allow by Default (Permitir por padrão)** estiver desativado, é necessário permitir o IP do cliente no grupo de segurança do CVM. O tráfego de negócios tem permissão para acessar o CVM apenas a partir da porta 80 do CLB e usar os serviços fornecidos pela porta 8080 do CVM.
>?Para permitir o tráfego de um IP de cliente especificado, é necessário permitir o IP no grupo de segurança do CLB e do CVM. Se o CLB não tiver um grupo de segurança, permita o IP no grupo de segurança do CVM.
>
1. Configure uma regra de grupo de segurança do CVM
   Um grupo de segurança do CVM pode ser configurado para permitir o acesso apenas a partir de portas de serviço para o tráfego que acessa a instância do CVM de back-end.<br>Acesse o [Console de grupo de segurança](https://console.cloud.tencent.com/cvm/securitygroup) para configurar uma política de grupo de segurança. Na regra de entrada, todas as portas 8080 de todos os IPs. Para garantir serviços remotos de login e ping do CVM, abra os serviços 22, 3389 e ICMP no grupo de segurança.
   ![](https://console.cloud.tencent.com/cvm/instance/index?rid=1)
2. Vincule o grupo de segurança à instância do CVM
 1. No [Console do CVM](https://console.intl.cloud.tencent.com/cvm/instance/index?rid=1), clique no ID da instância do CVM vinculada à instância do CLB para acessar a página de detalhes.
 2. Selecione a guia **Security Group (Grupo de segurança)** e clique em **Bind (Vincular)**, no módulo **Bound Security Groups (Grupos de segurança vinculados)**.
 3. Na janela **Configure Security Group (Configurar grupo de segurança)** exibida, selecione o grupo vinculado à instância do CVM e clique em **OK**.<img alt="" src="https://main.qcloudimg.com/raw/6e0e1c2f834bb7425ef3ca010114165a.png" title="Click to view the original image">

