## Visão geral
Um [grupo de segurança](https://intl.cloud.tencent.com/document/product/213/12452) é um firewall virtual com estado capaz de efetuar filtragem. Como um meio importante para isolamento de segurança de rede fornecido pela Tencent Cloud, ele pode ser usado para definir controles de acesso à rede para uma ou mais instâncias do TencentDB. Instâncias com as mesmas demandas de isolamento de segurança de rede em uma região podem ser colocadas no mesmo grupo de segurança, que é um grupo lógico. O TencentDB e a CVM compartilham a lista de grupos de segurança e são combinados entre si dentro do grupo de segurança com base em regras. Para regras e limitações específicas, consulte [Visão geral do grupo de segurança](https://intl.cloud.tencent.com/document/product/215/38750).

>?
>- Os grupos de segurança do TencentDB for MySQL atualmente só oferecem suporte ao controle de acesso à rede para VPCs e redes públicas, mas não para a rede clássica.
>- Grupos de segurança associados a instâncias do TencentDB nas regiões de Frankfurt, Vale do Silício e Singapura, atualmente não oferecem suporte ao controle de acesso à rede pública.
>- Como o TencentDB não possui tráfego de saída ativo, as regras de saída não são aplicáveis ​​ao TencentDB.
>- Grupos de segurança são compatíveis com instâncias de origem, somente leitura e recuperação de desastres do TencentDB for MySQL.
>- Grupos de segurança não são compatíveis com instâncias básicas do TencentDB for MySQL de nó único.


## Configuração de grupos de segurança para o TencentDB
### Etapa 1. Criação de um grupo de segurança
1. Faça login no [console da CVM](https://console.cloud.tencent.com/cvm/securitygroup).
2. Selecione **Security Group (Grupo de segurança)** na barra lateral esquerda, selecione uma região e clique em **Create (Criar)**.
3. Na janela de diálogo pop-up, configure os itens a seguir e clique em **OK**.
 - **Template (Modelo)**: selecione um modelo baseado no serviço a ser implantado na instância do TencentDB no grupo de segurança, o que simplifica a configuração da regra do grupo de segurança, conforme mostrado abaixo:
<table>
	<tr><th>Modelo</th><th>Descrição</th><th>Observações</th></tr>
	<tr><td>Open all ports (Abertura de todas as portas)</td><td>Todas as portas são abertas. Pode apresentar problemas de segurança.</td><td>-</td></tr>
	<tr><td>Open ports 22, 80, 443 e 3389 and the ICMP protocol (Abertura das portas 2, 80, 443 e 3389 e do protocolo ICMP)</td><td>As portas 22, 80, 443 e 3389 e o protocolo ICMP são abertas para a Internet. Todas as portas são abertas para a rede privada.<td><td>Este modelo não tem efeito para o TencentDB.</td></tr>
	<tr><td>Custom (Personalizado)</td><td>Você pode criar um grupo de segurança e, então, adicionar regras personalizadas. Para obter instruções detalhadas, consulte "Passo 2. Adicionar uma regra de grupo de segurança"</a> abaixo.</td><td>-</rd></tr>
</table>
 - **Name (Nome)**: nome do grupo de segurança.
 - **Project (Projeto)**: selecione um projeto para facilitar o gerenciamento. Por padrão, **DEFAULT PROJECT (PROJETO PADRÃO)** é selecionado.
 - **Notes (Observações)**: uma breve descrição do grupo de segurança para facilitar o gerenciamento.


### Etapa 2. Adicionar uma regra de grupo de segurança
1. Na página [Grupo de segurança](https://console.cloud.tencent.com/cvm/securitygroup), clique em **Modify Rule (Modificar regra)** na coluna **Operation (Operação)** na linha do grupo de segurança para o qual deseja configurar uma regra.
2. Na página de regras do grupo de segurança, clique em **Inbound rule (Regra de entrada)** > **Add Rule (Adicionar regra)**.
3. Na caixa de diálogo pop-up, defina a regra.
 - **Type (Tipo)**: **Custom (Personalizado)** fica selecionado por padrão. Você também pode escolher outro modelo de regra do sistema. MySQL(3306) é recomendado.
 - **Source (Origem)** ou **Target (Destino)**: origem do tráfego (regras de entrada) ou destino (regras de saída). É necessário especificar uma das seguintes opções:
<table>
	<tr><th>Origem ou destino</th><th>Descrição</th></tr>
	<tr><td>Um único endereço IPv4 ou um intervalo IPv4</td><td>Na notação CIDR, como <code>203.0.113.0</code>, <code>203.0.113.0/24</code> ou <code>0.0.0.0/0</code>, em que <code>0.0.0.0/0</code> indica que todos os endereços IPv4 serão correspondidos.</td></tr>
	<tr><td>Um único endereço IPv6 ou um intervalo IPv6</td><td>Na notação CIDR, como <code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code> ou <code>0::0/0</code>, em que <code>::/0</code> ou <code>0::0/0</code> indica que todos os endereços IPv6 serão correspondidos.</td></tr>
	<tr><td>ID do grupo de segurança de especificado. Você pode fazer referência ao ID do:<ul  style="margin: 0;"><li>Grupo de segurança atual</li><li>Outro grupo de segurança</li></ul>
</td><td><ul  style="margin: 0;"><li>Para fazer referência ao grupo de segurança atual, digite o ID do grupo associado à CVM.</li><li>Também é possível fazer referência a outro grupo de segurança na mesma região e no mesmo projeto, inserindo o ID do grupo.</li></ul>
</td></tr>
	<tr><td>Faça referência a um objeto de endereço IP ou objeto de grupo de endereço IP em um <a href="https://intl.cloud.tencent.com/document/product/215/31867">modelo de parâmetros</a>.</td><td>-</td></tr>
</table>
 - **Protocol port (Porta de protocolo)**: insira o tipo de protocolo e intervalo de portas ou faça referência a um protocolo/porta ou protocolo/grupo de portas em um [modelo de parâmetros](https://intl.cloud.tencent.com/document/product/215/31867).
>!Para se conectar a uma instância do TencentDB for MySQL, a porta deve ser aberta. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), clique em um ID na lista de instâncias e visualize seu número de porta na página de detalhes da instância.
>![](https://main.qcloudimg.com/raw/9f471c644eb9a5aa86bd092fdebd0255.png)
>
>- O TencentDB for MySQL usa a porta de rede privada 3306 por padrão e aceita a personalização da porta. Se a porta padrão for alterada, a nova porta deverá ser aberta no grupo de segurança.
>- O TencentDB for MySQL usa a porta de rede pública 60719 por padrão. Depois que o acesso à rede pública do TencentDB for MySQL for habilitado, ele será controlado pelo grupo de segurança, portanto, as portas 60719 e 3306 devem ser abertas.
>- As regras do grupo de segurança exibidas na página **Security Group (Grupo de segurança)** no console do TencentDB for MySQL entram em vigor para endereços de rede privados e públicos (se habilitados) da instância do TencentDB for MySQL.
>
 - **Policy (Política)**: **Allow (Permitir)** ou **Reject (Recusar)**. **Allow (Permitir)** fica selecionado por padrão.
    - **Allow (Permitir)**: o tráfego para esta porta é permitido.
    - **Reject (Recusar)**: os pacotes de dados serão descartados sem nenhuma resposta.
 - **Notes (Observações)**: uma breve descrição da regra para facilitar o gerenciamento.
4. Clique em **Complete (Concluir)**.

#### Caso de uso
**Cenário:** você criou uma instância do TencentDB for MySQL e deseja acessá-la de uma instância da CVM.
**Solução:** ao adicionar regras de grupo de segurança, selecione MySQL(3306) em **Type (Tipo)** para abrir a porta 3306.
Você também pode definir **Source (Origem)** para todos ou para IPs específicos (intervalos de IP) conforme necessário para permitir que eles acessem o TencentDB for MySQL a partir de uma instância da CVM.

| Entrada ou Saída   | Tipo   | Fonte                                                     | Protocolo e porta | Política |
|---------|---------|---------|---------|---------|
| Entrada | MySQL(3306) | Todos os IPs: 0.0.0.0/0 <br>IPs específicos: especificar IPs ou intervalos de IP | TCP:3306 | Permitir |


### Etapa 3. Configurar um grupo de segurança
Um grupo de segurança é um firewall em nível de instância fornecido pela Tencent Cloud para controlar o tráfego de entrada do TencentDB. Você pode associar um grupo de segurança a uma instância ao comprá-la ou pode fazê-lo posteriormente no console.

>!Atualmente, os grupos de segurança podem ser configurados apenas para instâncias do **TencentDB for MySQL em VPC)**.

1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), clique em um ID na lista de instâncias e entre na respectiva página de gerenciamento.
2. Na guia **Security Group (Grupo de segurança)**, clique em **Configure Security Group (Configurar grupo de segurança)**.
3. Na caixa de diálogo pop-up, selecione o grupo de segurança a ser vinculado e clique em **OK**. 

## Importação de regras de grupo de segurança
1. Na página [Grupo de segurança](https://console.cloud.tencent.com/cvm/securitygroup), clique no ID/nome do grupo de segurança desejado.
2. Na guia de inbound rule (regra de entrada) ou outbound rule (regra de saída), clique em **Import Rule (Importar regra)**.
3. Na caixa de diálogo pop-up, selecione um arquivo de modelo de regra de entrada/saída editado e clique em **Import (Importar)**.
>? Como as regras existentes serão substituídas após a importação, recomendamos exportar as regras existentes antes de importar as novas.

## Clonagem de grupos de segurança
1. Na página  [Grupo de segurança](https://console.cloud.tencent.com/cvm/securitygroup), localize o grupo de segurança desejado e clique em **More (Mais)** > **Clone (Clonar)** na coluna **Operation (Operação)**.
2. Na caixa de diálogo pop-up, selecione a região de destino e o projeto de destino, insira o novo nome do grupo de segurança e clique em **OK**. Se o novo grupo de segurança precisar ser associado a uma instância da CVM, faça isso gerenciando as instâncias de CVM no grupo de segurança.

## Exclusão de grupos de segurança
1. Na página [Grupo de segurança](https://console.cloud.tencent.com/cvm/securitygroup), localize o grupo a ser excluído e clique em **More (Mais)** > **Delete (Excluir)** na coluna **Operation (Operação)**.
2. Clique em **OK** na caixa de diálogo pop-up. Se o grupo de segurança atual estiver associado a uma instância de CVM, ele deverá ser dissociado antes de poder ser excluído.

