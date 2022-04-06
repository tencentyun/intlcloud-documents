## Adição de conexão
1. Faça login no [Console do GAAP](https://console.cloud.tencent.com/gaap), acesse a página **Access Management (Gerenciamento de acesso)** e clique em **Add (Adicionar)**.
2. Na janela pop-up, insira as informações da conexão.
![](https://main.qcloudimg.com/raw/d30c08d1cf9dedb12ed805bf731e073f.png)
	
	- **Project (Projeto)**: o projeto ao qual a conexão pertence, que pode ser alterado.
	- **Connection Name (Nome da conexão)**: aceita até 30 caracteres.
	- **IP Version (Versão do IP)**: aceita o IPv4 ou o IPv6. O IPv6 só é aceito nas regiões da China Continental.
	- **Acceleration Region (Região de aceleração)**: a região onde o cliente está localizado ou a mais próxima do cliente.
	<blockquote class="d-mod-notice">
							<div class="d-mod-title d-notice-title">
								<i class="d-icon-notice"></i>Observação:
   						</div>
	            <p>A rede BGP dedicada está disponível em Hong Kong, na China. Se quiser usá-la, envie um tíquete para entrar em contato conosco.</p>
						</blockquote>
	- **Origin Region (Região de origem)**: a região onde está localizado o servidor de destino ou a mais próxima do servidor de destino.
	<blockquote class="d-mod-notice">
							<div class="d-mod-title d-notice-title">
								<i class="d-icon-notice"></i>Observação:
   						</div>
	            <p>O servidor de origem em Taiwan, na China, não pode acessar a região de aceleração na China Continental, e vice-versa.</p>
						</blockquote>
	- **Bandwidth Cap (Limite da largura de banda)**: largura de banda máxima de uma conexão, que é de 10.000 Mbps (1.000 Mbps para algumas conexões).
	- **Maximum Concurrent Connections (Quantidade máxima de conexões simultâneas)**: quantidade máxima de conexões simultâneas para uma conexão, que é 1 milhão (300.000 para algumas conexões).
	- **Tag**: permite a classificação de conexões. Esse é um item opcional.
	- **Fees (Taxas)**: as taxas de conexão e de largura de banda são calculadas com base na largura de banda e nas conexões simultâneas que você especificar. A taxa de conexão é calculada diariamente até que a conexão seja excluída, já a largura de banda é cobrada pelo limite diário real de largura de banda de entrada e de saída.
3. Clique em **OK**.
4. Na página **Access Management (Gerenciamento de acesso)**, exiba as informações da lista de conexões.
![](https://main.qcloudimg.com/raw/b326c683b47321704d0269a0eb047f2d.png)
	
	- **ID/Connection Name (ID/Nome da conexão)**: ID e nome de uma conexão. É possível alterar o nome da conexão.
	- **VIP**: endereço IP acessado pelo cliente.
	- **Domain name (Nome de domínio)**: nome de domínio acessado pelo cliente, que é atribuído pelo sistema e vinculado automaticamente ao VIP.
	- **Status**: apenas as conexões de aceleração com o status **Running (Em execução)** podem funcionar normalmente.

## Exibição de informações das conexões
1. Faça login no [Console do Global Application Acceleration Platform](https://console.cloud.tencent.com/gaap), acesse a página **Access Management (Gerenciamento de acesso)** e clique em **ID/Connection Name (ID/Nome da conexão)** de uma conexão.
 ![](https://main.qcloudimg.com/raw/3021dcb23fd2482cd7d43146b51aa96c.png)
2. Na guia **Connection info (Informações da conexão)**, é possível exibir os detalhes da conexão. **Forwarding Server IP (IP do servidor de encaminhamento)** é o IP do nó de encaminhamento no final da conexão de aceleração, e esse nó de encaminhamento encaminha os dados da conexão de aceleração para o servidor de origem pela rede pública. Se você quiser que várias conexões usem o mesmo nome de domínio, clique em **Unified Domain Name (Nome de domínio unificado)** para acessar a [configuration (configuração)](https://console.cloud.tencent.com/gaap/domain).
![](https://main.qcloudimg.com/raw/0f3097be7c9bb138d4287683a97863d1.png) 
