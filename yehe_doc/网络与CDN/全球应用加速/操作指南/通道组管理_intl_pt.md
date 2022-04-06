## Adição de grupo de conexões
Para implantar aceleração em várias regiões com a mesma configuração de servidor de origem e listener, você pode adicionar um grupo de conexões para gerenciar as conexões em lote, reduzindo a sua carga de trabalho.

1. Faça login no [Console do GAAP](https://console.cloud.tencent.com/gaap), acesse a página **Connection Group Management (Gerenciamento de grupos de conexões)** e clique em **Add (Adicionar)**.
2. Na janela pop-up, insira as informações do grupo de conexões.
![](https://qcloudimg.tencent-cloud.cn/raw/42ea117befdea84bafafd6af6a9e2e09.png)
	- **Project (Projeto)**: o projeto ao qual pertence o grupo de conexões, que pode ser alterado.
	- **Connection Group Name (Nome do grupo de conexões)**: aceita até 30 caracteres.
	- **IP Version (Versão do IP)**: aceita o IPv4 ou o IPv6. O IPv6 só é aceito nas regiões da China Continental.
	- **Acceleration Region (Região de aceleração)**: a região onde o cliente está localizado ou a mais próxima do cliente. Você pode selecionar mais de uma região de aceleração.
	<blockquote class="d-mod-notice">
                   <div class="d-mod-title d-notice-title">
                       <i class="d-icon-notice"></i>Observação:
                   </div>
      <p>A rede BGP dedicada só é aceita em Hong Kong, na China. Se você precisar dela, envie um tíquete para entrar em contato conosco.</p>
               </blockquote>
	- **Origin Region (Região de origem)**: a região onde está localizado o servidor de destino ou a mais próxima do servidor de destino.
	<blockquote class="d-mod-notice">
                   <div class="d-mod-title d-notice-title">
                       <i class="d-icon-notice"></i>Observação:
                   </div>
      <p>O servidor de origem em Taiwan, na China, não pode acessar a região de aceleração na China Continental, e vice-versa.</p>
               </blockquote>
	- **Connection Specification (Especificação de conexão)**: permite a configuração do limite de largura de banda de uma conexão e da quantidade máxima de conexões simultâneas.
	- **Bandwidth Cap (Limite da largura de banda)**: largura de banda máxima de uma conexão, que é de 10.000 Mbps (1.000 Mbps para algumas conexões).
	- **Maximum Concurrent Connections (Quantidade máxima de conexões simultâneas)**: quantidade máxima de conexões simultâneas para uma conexão, que é 1 milhão (300.000 para algumas conexões).
	
   	<blockquote class="d-mod-notice">
   	            <div class="d-mod-title d-notice-title">
   	                <i class="d-icon-notice"></i>Observação:
   	            </div>
      <p>Um grupo de conexões pode conter até 20 conexões.</p>
	            </blockquote>
	- **Tag**: permite a classificação de conexões. Esse é um item opcional.
	- **Fees (Taxas)**: as taxas de conexão e de largura de banda são calculadas com base na largura de banda e nas conexões simultâneas que você especificar. A taxa de conexão é calculada diariamente até que a conexão seja excluída, já a largura de banda é cobrada pelo limite diário real de largura de banda de entrada e de saída.
3. Clique em **OK**.
4. Na página [Connection Group Management(Gerenciamento de grupos de conexões)](https://console.cloud.tencent.com/gaap/group), você pode exibir os detalhes do grupo de conexões, gerenciar as conexões no mesmo grupo de conexões e monitorar seus estados em tempo real.
![](https://qcloudimg.tencent-cloud.cn/raw/b6828c4086edaa1b1cf84986c1379036.png)
	- **ID/Connection Group Name (ID/Nome do grupo de conexões)**: ID e nome de um grupo de conexões. O nome do grupo de conexões pode ser alterado.
	- **VIP**: endereço IP acessado pelo cliente.
	- **Domain name (Nome de domínio)**: nome de domínio acessado pelo cliente, que é atribuído pelo sistema e vinculado automaticamente ao VIP.
	- **Status**: apenas as conexões de aceleração com o status **Running (Em execução)** podem funcionar normalmente.

## Exibição de informações do grupo de conexões
1. Faça login no [Console do GAAP](https://console.cloud.tencent.com/gaap), acesse a página **Connection Group Management (Gerenciamento de grupos de conexões)** e clique em **ID/Connection Group Name (ID/Nome do grupo de conexões)** de um grupo de conexões.
 ![](https://qcloudimg.tencent-cloud.cn/raw/a61839822d556c1dc21f0fc07d3f4df0.png)
2. Na guia **Connection group info (Informações do grupo de conexões)**, é possível exibir os detalhes das conexões. **Forwarding Server IP (IP do servidor de encaminhamento)** é o IP do nó de encaminhamento no final da conexão de aceleração, e esse nó de encaminhamento encaminha os dados da conexão de aceleração para o servidor de origem pela rede pública. Se você quiser que várias conexões usem o mesmo nome de domínio, clique em **Unified Domain Name (Nome de domínio unificado)** para acessar a [configuration (configuração)](https://console.cloud.tencent.com/gaap/domain). Você também pode configurar separadamente o nome de domínio unificado para conexões no mesmo grupo de conexões.
 ![](https://qcloudimg.tencent-cloud.cn/raw/7ff4c01ffd322dd8577d426e6a3ce3fa.jpg)


## Gerenciamento de listener TCP/UDP
### Adição de listener TCP/UDP
Para mais informações, consulte [Gerenciamento de acesso](https://intl.cloud.tencent.com/document/product/608/13764).

### Configuração de listener TCP/UDP
Para mais informações, consulte [Gerenciamento de acesso](https://intl.cloud.tencent.com/document/product/608/13764).

## Gerenciamento de listener HTTP/HTTPS

### Adição de listener HTTP/HTTPS
Para mais informações, consulte [Gerenciamento de acesso](https://intl.cloud.tencent.com/document/product/608/17539).

### Configuração de listener HTTP/HTTPS
Para mais informações, consulte [Gerenciamento de acesso](https://intl.cloud.tencent.com/document/product/608/17539).

## Proteção de segurança
Para mais informações, consulte [Gerenciamento de acesso](https://intl.cloud.tencent.com/document/product/608/42338).
