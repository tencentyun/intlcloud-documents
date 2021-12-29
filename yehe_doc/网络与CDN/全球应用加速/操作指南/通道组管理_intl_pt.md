## Criação de grupo de conexão

Se precisar acelerar o acesso em várias regiões com a mesma região de servidor de origem e configuração de listener, é possível configurar e gerenciar conexões em lotes por meio de um grupo de conexão, o que reduz o trabalho repetitivo envolvido no gerenciamento de conexões individuais.

1. Faça login no [Console do GAAP](https://console.cloud.tencent.com/gaap), acesse a página **Connection Group Management (Gerenciamento de grupo de conexão)** e clique em **Create (Criar)**.
2. Na janela pop-up, insira as informações do grupo de conexão.
   ![](https://qcloudimg.tencent-cloud.cn/raw/42ea117befdea84bafafd6af6a9e2e09.png)
   
   - Project (Projeto): o projeto ao qual pertence o grupo de conexão, que pode ser alterado.
   - Connection Group Name (Nome do grupo de conexão): pode conter até 30 caracteres.
   - IP Version (Versão do IP): selecione IPv4 ou IPv6 conforme necessário. Atualmente, o IPv6 é compatível apenas com nós de acesso na China Continental.
   - Access Node (Nó de acesso): selecione um ou vários nós na região do cliente ou na região mais próxima do cliente.
   <blockquote class="d-mod-notice">
<div class="d-mod-title d-notice-title">
 <i class="d-icon-notice"></i>Observação:
</div>
<li>Uma rede BGP premium está disponível em Hong Kong (China). Se necessário, <a href="https://console.cloud.tencent.com/workorder/category">envie um tíquete</a> e entre em contato conosco.</li>
<li>Uma rede de nós não BGP está disponível na China Continental. Se necessário, <a href="https://console.cloud.tencent.com/workorder/category">envie um tíquete</a> e entre em contato conosco.</li>
</blockquote>
- Origin Server Region (Região do servidor de origem): selecione um nó na região do servidor de destino ou na região mais próxima dele.
   <blockquote class="d-mod-notice">
                   <div class="d-mod-title d-notice-title">
                       <i class="d-icon-notice"></i>Observação:
                   </div>
      <p>Nenhuma conexão direta pode ser estabelecida entre Taiwan (China) e a China Continental.</p>
               </blockquote>
- Connection Specification (Especificação de conexão): selecione o limite de largura de banda e a quantidade máxima de conexões simultâneas para cada conexão.
- Bandwidth Cap (Limite da largura de banda): o limite superior da largura de banda da conexão é de 10.000 Mbps (ou 1.000 Mbps para algumas conexões).
- Maximum Concurrent Connections (Quantidade máxima de conexões simultâneas): a quantidade máxima de conexões simultâneas aceita por uma conexão é 1 milhão (ou 300.000 para algumas conexões).
   <blockquote class="d-mod-notice">
                   <div class="d-mod-title d-notice-title">
                       <i class="d-icon-notice"></i>Observação:
                   </div>
      <p>Um grupo de conexão pode conter até 20 conexões.</p>
               </blockquote>
- Tag: você tem a opção de definir tags para categorizar e gerenciar as conexões.
- Fees (Taxas): as taxas de conexão e de largura de banda correspondentes serão exibidas abaixo, de acordo com a largura de banda e a simultaneidade que você selecionar.
  a. Taxas de conexão: faturadas por dia até que a conexão seja excluída. Observe que as taxas de conexão ainda serão cobradas por um dia, mesmo se a conexão for excluída menos de um dia após a criação.
  b. Taxas de largura de banda: faturadas pela largura de banda de pico de entrada/saída diária.
3. Clique em **OK**.
4. Na página [Gerenciamento de grupos de conexão](https://console.cloud.tencent.com/gaap/group), exiba as informações da lista de grupos de conexão. É possível gerenciar conexões diferentes em um grupo de conexão de acordo com suas necessidades e monitorar o status de execução delas em tempo real.
   ![](https://qcloudimg.tencent-cloud.cn/raw/b6828c4086edaa1b1cf84986c1379036.png)
   - ID/Connection Group Name (ID/Nome do grupo de conexão): ID e nome (personalizável) do grupo de conexão.
   - VIP: endereço IP acessado pelo cliente.
   - Domain Name (Nome de domínio): nome de domínio acessado pelo cliente, que é atribuído pelo sistema e vinculado automaticamente ao VIP.
   - Status: apenas as conexões de aceleração com o status **Running (Em execução)** podem funcionar normalmente.

## Exibição de informações do grupo de conexão

1. Faça login no [Console do GAAP](https://console.cloud.tencent.com/gaap), acesse a página **Connection Group Management (Gerenciamento de grupos de conexão)** e clique em **ID/Connection Name (ID/Nome da conexão)** do grupo de conexão especificado.
   ![](https://qcloudimg.tencent-cloud.cn/raw/a61839822d556c1dc21f0fc07d3f4df0.png)
2. Na guia **Connection Group Info (Informações do grupo de conexão)**, é possível exibir os detalhes de cada conexão. O **Forwarding server IP (IP do servidor de encaminhamento)** se refere ao IP do nó de encaminhamento no final da conexão de aceleração, que é responsável por encaminhar os dados da conexão ao servidor de origem pela rede pública. Se desejar que várias conexões usem o mesmo nome de domínio, clique em **Unified Domain Name (Nome de domínio unificado)**, a fim de redirecionar para a página [Nome de domínio unificado](https://console.cloud.tencent.com/gaap/domain) para configuração. Um **nome de domínio unificado** pode ser configurado separadamente para conexões diferentes no mesmo grupo de conexão.
   ![](https://qcloudimg.tencent-cloud.cn/raw/7ff4c01ffd322dd8577d426e6a3ce3fa.jpg)

## Gerenciamento de listener TCP/UDP

### Criação de listener TCP/UDP

Para obter mais instruções, consulte [Gerenciamento de listener TCP/UDP](https://intl.cloud.tencent.com/document/product/608/13764).

### Definição de listener TCP/UDP

Para obter mais instruções, consulte [Gerenciamento de listener TCP/UDP](https://intl.cloud.tencent.com/document/product/608/13764).

## Gerenciamento de listener HTTP/HTTPS

### Criação de listener HTTP/HTTPS

Para obter mais instruções, consulte [Gerenciamento de listener HTTP/HTTPS](https://intl.cloud.tencent.com/document/product/608/17539).

### Definição de listener HTTP/HTTPS

Para obter mais instruções, consulte [Gerenciamento de listener HTTP/HTTPS](https://intl.cloud.tencent.com/document/product/608/17539).

## Proteção de segurança

Para obter mais informações, consulte [Gerenciamento de listener HTTP/HTTPS](https://intl.cloud.tencent.com/document/product/608/42338).
