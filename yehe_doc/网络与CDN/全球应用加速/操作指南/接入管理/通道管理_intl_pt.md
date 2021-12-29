## Adição de conexão

1. Faça login no [Console do GAAP](https://console.cloud.tencent.com/gaap), acesse a página **Access Management (Gerenciamento de acesso)** e clique em **Create (Criar)**.
2. Na janela pop-up, insira as informações da conexão.
![](https://main.qcloudimg.com/raw/d30c08d1cf9dedb12ed805bf731e073f.png)
   
   - Project (Projeto): o projeto ao qual a conexão pertence, que pode ser alterado.
   - Connection Name (Nome da conexão): pode conter até 30 letras e símbolos normais.
   - IP Version (Versão do IP): selecione IPv4 ou IPv6 conforme necessário. Atualmente, o IPv6 é compatível apenas com regiões na China Continental.
   - Access Node (Nó de acesso): selecione um nó na região do cliente ou na região mais próxima a ele.
   <blockquote class="d-mod-notice">
   						<div class="d-mod-title d-notice-title">
   							<i class="d-icon-notice"></i>Observação:
   						</div>
               <p>Uma rede BGP premium está disponível em Hong Kong (China). Se necessário, envie um tíquete e entre em contato conosco.</p>
               <p>Uma rede de nós não BGP está disponível na China Continental. Se necessário, envie um tíquete e entre em contato conosco.</p>
   					</blockquote>
   - Origin-Pull Node (Nó do pull de origem): selecione um nó na região do servidor de destino ou na região mais próxima a ele.
   <blockquote class="d-mod-notice">
   						<div class="d-mod-title d-notice-title">
   							<i class="d-icon-notice"></i>Observação:
   						</div>
               <p>Nenhuma conexão direta pode ser estabelecida entre Taiwan (China) e a China Continental.</p>
   					</blockquote>
   - Bandwidth Cap (Limite da largura de banda): o limite superior da largura de banda da conexão é de 10.000 Mbps (ou 1.000 Mbps para algumas conexões).
   - Maximum Concurrent Connections (Quantidade máxima de conexões simultâneas): a quantidade máxima de conexões simultâneas aceita por uma conexão é 1 milhão (ou 300.000 para algumas conexões).
   - Tag: você tem a opção de definir tags para categorizar e gerenciar as conexões.
   - Fees (Taxas): as taxas de conexão e de largura de banda correspondentes serão exibidas abaixo, de acordo com a largura de banda e a simultaneidade que você selecionar.
     a. Taxas de conexão: faturadas por dia até que a conexão seja excluída. Observe que as taxas de conexão ainda serão cobradas por um dia, mesmo se a conexão for excluída menos de um dia após a criação.
     b. Taxas de largura de banda: faturadas pela largura de banda de pico de entrada/saída diária.
3. Clique em **OK**.
4. Na página **Access Management (Gerenciamento de acesso)**, exiba as informações da lista de conexões.
![](https://main.qcloudimg.com/raw/b326c683b47321704d0269a0eb047f2d.png)
   
   - ID/connection name (ID/nome da conexão): ID e nome de uma conexão. É possível alterar o nome da conexão.
   - VIP: endereço IP acessado pelo cliente.
   - Domain name (Nome de domínio): nome de domínio acessado pelo cliente, que é atribuído pelo sistema e vinculado automaticamente ao VIP.
   - Status: apenas as conexões de aceleração com o status **Running (Em execução)** podem funcionar normalmente.

## Exibição de informações das conexões

1. Faça login no [Console do GAAP](https://console.cloud.tencent.com/gaap), acesse a página **Access Management (Gerenciamento de acesso)** e clique em **ID/Connection Name (ID/Nome da conexão)** da conexão especificada.
![](https://qcloudimg.tencent-cloud.cn/raw/dba1d1cb841d8575a1b653c9d47f640b.png)
2. Na guia **Connection Info (Informações da conexão)**, é possível exibir os detalhes da conexão. O **Forwarding server IP (IP do servidor de encaminhamento)** se refere ao IP do nó de encaminhamento no final da conexão de aceleração, que é responsável por encaminhar os dados da conexão ao servidor de origem pela rede pública. Se desejar que várias conexões usem o mesmo nome de domínio, clique em **Not Associated (Não associadas)**, a fim de redirecionar para a página [Nome de domínio unificado](https://console.cloud.tencent.com/gaap/domain) para configuração.<br>
<img src="https://main.qcloudimg.com/raw/0f3097be7c9bb138d4287683a97863d1.png" width="50%">
