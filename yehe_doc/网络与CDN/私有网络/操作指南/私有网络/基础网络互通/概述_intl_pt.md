A funcionalidade Classiclink permite que os CVMs baseados no VPC se comuniquem com os CVMs baseados na rede clássica. Este documento descreve principalmente como criar e gerenciar o Classiclink.

## Informações gerais
Tanto a rede clássica quanto o VPC são espaços de rede na nuvem. A rede clássica é um pool de recursos de rede pública para todos os usuários do Tencent Cloud (conforme mostrado no lado direito da figura abaixo). Os IPs privados de todos os CVMs são atribuídos pelo Tencent Cloud. Não é possível personalizar os intervalos de IP ou os endereços de IP. Por outro lado, o VPC é um espaço de rede isolado logicamente no Tencent Cloud (conforme mostrado no lado esquerdo da figura abaixo). Em um VPC, é possível personalizar os intervalos de IP, os endereços IP e as políticas de roteamento.
O VPC é mais adequado para os casos de uso que exigem configurações personalizadas.
>?
>+ Como os recursos da rede clássica se tornam cada vez mais escassos e não podem ser expandidos, as contas do Tencent Cloud, criadas após 13 de junho de 2017, podem criar instâncias (incluindo instâncias do CVM e do TencentDB) apenas em um VPC em vez da rede clássica. Se for necessário usar o serviço da rede clássica, envie uma solicitação.
>+ É possível usar a API `DescribeAccountVpcAttributes` para consultar os atributos de rede de uma conta. Se o valor `supportedPlatforms` for `only-vpc`, a conta é um usuário padrão do VPC, que possui todos os recursos de nuvem em VPCs. Se o valor `supportedPlatforms` for `classic`, a conta é um usuário padrão da rede clássica, que possui todos os recursos de nuvem na rede clássica.
>+ É possível migrar suas instâncias da rede clássica para um VPC para facilitar o uso do VPC. Para obter instruções detalhadas, consulte [Alternância da rede clássica para o VPC](https://intl.cloud.tencent.com/document/product/215/38117).
>
![](https://main.qcloudimg.com/raw/5fe7730ac2f302d960cf20443f976b6f.png)

## Visão geral
Por padrão, um VPC é um espaço de rede totalmente isolado que fica inacessível para outros VPCs ou para a rede clássica por meio de uma rede privada. O CCN garante interconexões entre os VPCs, enquanto as soluções a seguir fornecem comunicação entre um VPC e a rede clássica.
+ **Classiclink**: permite que os CVMs baseados na rede clássica se comuniquem com recursos do VPC, como instâncias do CVM, do TencentDB e do CLB. No entanto, ele só fornece acesso entre os CVMs baseados no VPC e na rede clássica, em vez de outros recursos de nuvem, incluindo o TencentDB e o CLB dentro da rede clássica, conforme mostrado abaixo.
 <img src="https://main.qcloudimg.com/raw/5c4c66605c6ecd04591dfff5236231df.png" width="50%" />
+ **Terminal connection (Conexão de terminal)**: ajuda a estabelecer a comunicação entre as instâncias em um VPC e os recursos na rede clássica (exceto os CVMs) por meio de uma rede privada. Ela mapeia o IP de uma instância baseada na rede clássica para um IP do VPC, permitindo que você acesse a instância baseada na rede clássica por meio do IP do VPC. Essa funcionalidade agora oferece suporte a instâncias clássicas e baseadas em rede do CLB, do MySQL, do Memcached, do Redis e do MongoDB. No entanto, a comunicação entre regiões ou contas não é compatível. Se você deseja estabelecer uma conexão de terminal, [envie um tíquete](https://console.cloud.tencent.com/workorder/category).


## Criação de um Classiclink
Um Classiclink associa CVMs baseados na rede clássica com um VPC para permitir a interconexão entre o VPC e a rede clássica. Isso permite que os CVMs baseados na rede clássica se comuniquem com recursos do VPC.

### Limites de uso
+ O intervalo de IP do VPC deve estar dentro de `10.0.0.0/16-10.47.0.0/16` (incluindo os subconjuntos); caso contrário, pode haver conflitos de IP que podem causar falha durante a associação e comunicação com os CVMs baseados na rede clássica.
+ Um CVM baseado na rede clássica só pode ser associado a um VPC por vez.
+ Um VPC aceita a associação com até 100 CVMs baseados na rede clássica.
+ Os recursos do VPC conseguem acessar o CVM baseado na rede clássica, mas não outros recursos, incluindo o TencentDB e o CLB.
+ Depois que os CVMs da rede clássica são associados a um VPC, os CVMs baseados na rede clássica só conseguem se comunicar com os recursos no bloco CIDR principal, em vez do bloco CIDR secundário do VPC.
- Um VPC só pode ser interconectado com a rede clássica na mesma região.

### Observações
+ Os IPs privados dos CVMs associados baseados na rede clássica serão adicionados automaticamente à política local da tabela de rotas do VPC. Isso permite a interconexão entre esses CVMs e os CVMs baseados no VPC, sem a necessidade de modificar manualmente a política de roteamento do VPC.
+ Depois que o CVM baseado na rede clássica for associado a um VPC, suas configurações de firewall e ACL de rede permanecerão efetivas. Ou seja, é possível configurar a ACL de rede para a sub-rede do VPC, a fim de restringir o acesso de CVMs baseados na rede clássica associados. Também é possível configurar regras de grupo de segurança para os CVMs na rede clássica e no VPC para restringir o acesso bidirecional à rede.
+ As instâncias do CLB em um VPC não podem ser vinculadas a um CVM baseado na rede clássica que se interconecta com o mesmo VPC.
- Alterar o IP privado de um CVM baseado na rede clássica invalidará sua associação com o VPC e fará com que as configurações se tornem inválidas. Para associá-los, é necessário adicionar um Classiclink novamente no console do VPC.
- O Classiclink não será afetado por ações tomadas em relação ao CVM, como o isolamento devido a pagamentos em atraso, o isolamento de segurança, a migração a frio, o failover, a modificação de configuração e a troca de sistema operacional.
- O CVM será desassociado automaticamente do VPC se o CVM for retornado.
+ Em situações com Classiclink, o tráfego do CVM só pode ser roteado para endereços IP privados dentro do VPC, mas não para destinos fora do VPC. Ou seja, o CVM baseado na rede clássica não consegue acessar os recursos de rede pública ou privada fora do VPC atual por meio de dispositivos de rede, como gateway VPN, gateway do Direct Connect, gateway público, Peering Connection e NAT Gateway. Da mesma forma, o par de um gateway VPN, gateway do Direct Connect e Peering Connection não consegue acessar os CVMs baseados na rede clássica.

### Instruções
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione a região e clique no ID do VPC que precisa do Classiclink, para acessar a página de detalhes.
3. Clique na guia **Classiclink** e em **+ Associate with CVM (+Associar ao CVM)**. 
![](https://main.qcloudimg.com/raw/ad9b76faac017dbc093b3710f0d5070b.png)
4. Na janela pop-up, selecione o CVM na rede clássica a ser associado ao VPC e clique em **OK**.
![](https://main.qcloudimg.com/raw/b99329129fc8de27dddfbe7897d59218.png)

## Exibição do Classiclink
É possível exibir a lista de CVMs baseados na rede clássica que se interconectam com o VPC.
### Instruções
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione a região e clique no ID do VPC que precisa do Classiclink, para acessar a página de detalhes.
3. Clique na guia **Classiclink** para exibir a lista de CVMs baseados na rede clássica associados ao VPC.
![](https://main.qcloudimg.com/raw/3b4e1ad2a860c35f89b42315e709d11f.png)
4. Digite um IP privado na caixa de pesquisa do canto superior direito para localizar o CVM de forma rápida.

<span id="release" ></span>
## Exclusão de um Classiclink
Essa ação desassocia os CVMs baseados na rede clássica do VPC e encerra sua interconexão.

### Instruções
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Clique no ID do VPC que precisa do Classiclink acessar a página de detalhes.
3. Clique na guia **Classiclink**, selecione o CVM a ser desassociado da lista de CVMs baseados na rede clássica e clique em **Disassociate (Desassociar)** na coluna **Operation (Operação)**.
![](https://main.qcloudimg.com/raw/156dd9a80b6923a96bb52e2d76b55993.png)
4. Verifique as observações e clique em **OK**.
5. Para desassociar vários CVMs, selecione os CVMs a serem desassociados e clique em **Disassociate (Desassociar)** acima da lista.
