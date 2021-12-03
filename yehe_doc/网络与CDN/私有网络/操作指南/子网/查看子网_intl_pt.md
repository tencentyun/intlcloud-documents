É possível exibir os recursos de todas as sub-redes no VPC no console do VPC, por exemplo, os recursos de nuvem implantados na sub-rede, a tabela de rotas associada à sub-rede e as regras de ACL vinculadas à sub-rede.

## Instruções
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione **Subnet (Sub-rede)** na barra lateral esquerda para acessar a página de gerenciamento de sub-rede.
3. Na parte superior da página **Subnet (Sub-rede)**, selecione a região e o VPC aos quais a sub-rede pertence. Se você mantiver o valor padrão, ou seja, **All VPCs (Todos os VPCs)**, poderá exibir todas as sub-redes de todos os VPCs nesta região, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/56e17047ec183ee28d6ffcd5784ffcb3.png)
O significado dos campos da lista exibidos na interface é o seguinte:
 + ID/Name (ID/Nome): exibe o ID e o nome da sub-rede. Todas as sub-redes recebem um ID quando são criadas e o nome delas pode ser modificado em tempo real.
 + Network (Rede): o VPC ao qual a sub-rede pertence.
 + CIDR: o intervalo de IP do bloco CIDR da sub-rede. O bloco CIDR da sub-rede não pode ser modificado.
 + Availability Zone (Zona de disponibilidade): exibe a zona de disponibilidade na qual a sub-rede está localizada.
 + Associated Route Table (Tabela de rotas associada): a tabela de rotas associada à sub-rede.
 + CVM: exibe os números dos CVMs implantados na sub-rede.
 + Available IPs (IPs disponíveis): o número dos endereços IP disponíveis no intervalo de blocos CIDR da sub-rede.
 + Default Subnet (Sub-rede padrão): para as sub-redes criadas pelo usuário na página **Subnet (Sub-rede)** no console VPC, que não são as sub-redes padrão, o campo de valor exibirá **No (Não)**. Se você selecionar o VPC e a sub-rede padrão criados automaticamente pelo Tencent Cloud na página de aquisição do CVM, aqui será exibido **Yes (Sim)**. Só pode haver um único VPC e sub-rede padrão em uma determinada região.
 + Creation Time (Hora de criação): a hora de criação da sub-rede.
 + Operation (Operação): as operações executáveis para a sub-rede. Você pode excluir a sub-rede sem recursos ou clicar em **More (Mais)** > **Change Route Table (Alterar a tabela de rotas)** para substituir a tabela de rotas associada à sub-rede.
4. Clique no ID da sub-rede para exibir os detalhes dos recursos da sub-rede. Alterne a guia para exibir as regras de roteamento e as regras de ACL.
![](https://main.qcloudimg.com/raw/308eaf31ea4d3a1f92fbc868fa7ce699.png)
5. Clique no ID do VPC da rede à qual a sub-rede pertence ou no ID da tabela de rotas associada, para exibir as informações detalhadas do recurso correspondente.
6. Clique no número dos CVMs para acessar a página da instância do CVM. Se a quantidade for 0, clique no ícone do CVM para acessar a página de aquisição do CVM.
7. Na parte superior da página, clique em **Filter (Filtrar)** para exibir a lista de sub-redes na zona disponível especificada.
8. Clique na caixa de pesquisa no canto superior direito da página para consultar rapidamente por **subnet ID (ID da sub-rede)**, **Subnet Name (Nome da sub-rede)**, **Tag** e **IPv4 CIDR Block (Bloco CIDR IPv4)**.
9. Clique no ícone de Configuração no canto superior direito para personalizar os campos exibidos.

