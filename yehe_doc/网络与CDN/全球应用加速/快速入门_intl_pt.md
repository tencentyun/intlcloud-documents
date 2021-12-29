
## Etapa 1. Adicionar um servidor de origem

1. Faça login no [Console do GAAP](https://console.cloud.tencent.com/gaap).
2. Clique em **Origin Server Management (Gerenciamento de servidores de origem)** > **Create (Criar)**, defina o nome, insira o IP ou nome de domínio do servidor de origem e adicione tags (opcional) para acrescentar as informações de todos os servidores para os quais acelerar o acesso a **Origin Server Management (Gerenciamento de servidores de origem)**. É possível inserir as informações de vários servidores de origem ao mesmo tempo.
3. Clique em **OK**.
![](https://main.qcloudimg.com/raw/700758b2be655f701f88ddc2f72857fc.png)
4. (Opcional) Adicione um alias ao servidor de origem para uso futuro: clique no ícone **Edit (Editar)** ao lado do nome do servidor de origem, insira um nome e clique em **OK**.
![](https://main.qcloudimg.com/raw/c72f5506cc15b41a93fb8ce64767108f.png)

## Etapa 2. Criar uma conexão de aceleração

1. Clique em **Access Management (Gerenciamento de acesso)** > **Create (Criar)**.
![](https://main.qcloudimg.com/raw/5f424ce7a93036ad42f1adb174bdffbc.png)
2. Na janela **Add a connection (Adicionar uma conexão)**, insira as informações da conexão de aceleração.
![](https://main.qcloudimg.com/raw/e2c839706090fbce1d01d7ecae40310c.png)
	- Access Node (Nó de acesso): entrada da conexão de aceleração. Selecione um nó na região do cliente ou em uma região próxima.
	- Origin-Pull Node (Nó do pull de origem): saída da conexão de aceleração. Selecione um nó na região do servidor de destino ou em uma região próxima.
	- Bandwidth Cap (Limite da largura de banda): o limite superior da largura de banda da conexão.
	- Maximum Concurrent Connections (Quantidade máxima de conexões simultâneas): a quantidade máxima de conexões simultâneas aceitas por uma conexão.
3. Clique em **OK**. Após a criação, você pode exibir as informações da conexão, em que o **VIP** e o **Domain Name (Nome de domínio)** são os endereços de acesso da conexão de aceleração.
![](https://main.qcloudimg.com/raw/f398e22ba4e21ac9055b30141c049a7e.png)
4. Clique no **ID/Connection Name (ID/Nome da conexão)** para prosseguir para a próxima página.

## Etapa 3. Criar um listener

1. Selecione a guia **TCP/UDP Listener Management (Gerenciamento de listener TCP/UDP)**, clique em **Create (Criar)** e adicione uma política de encaminhamento na janela pop-up.
2. Configure as informações do listener (com TCP como exemplo) para definir o mapeamento entre o protocolo de aceleração e a porta de escuta. É possível mapear várias portas de escuta de uma vez, mas elas devem ser exclusivas.
	- Listening Port (Porta de escuta): a porta de acesso do VIP da conexão de aceleração.
<img src="https://main.qcloudimg.com/raw/e81e6cf664c72dfd4dea36714e0e5197.png" width="80%">
3. Configure a política de processamento do servidor de origem; ou seja, quando um listener estiver vinculado a vários servidores de origem, será necessário selecionar uma política de programação para eles, conforme mostrado abaixo:
<img src="https://main.qcloudimg.com/raw/74a7f1b78cf5436fd9ff439c96dee5b0.png" width="80%">
4. Configure o mecanismo de verificação de integridade do servidor de origem.
   Se o protocolo TCP for usado, o mecanismo de verificação de integridade deve ser configurado. Selecione **Enable Health Check (Ativar verificação de integridade)** e configure o tempo de resposta e o intervalo de monitoramento.
<img src="https://main.qcloudimg.com/raw/17f17a494f535cfb20c7a6d6e1f77945.png"  width="80%"><br>
	- Response Timeout (Tempo limite de resposta): o tempo limite de uma resposta.
	O **Health Check Interval (Intervalo de verificações de integridade)** se refere ao intervalo entre duas verificações de integridade consecutivas. Se a verificação de integridade determinar que um servidor de origem está anormal, ele parará de encaminhar pacotes até que retorne a um status normal após outra verificação.
	- Unhealthy/Healthy Threshold (Limite íntegro/não íntegro): indica a quantidade de verificações com falha/êxito consecutivas antes que o servidor de origem seja considerado íntegro/não íntegro.





## Etapa 4. Vincular o servidor de origem

1. Selecione um listener e clique em **Bind Origin Server (Vincular servidor de origem)** na coluna **Operation (Operação)**.
2. Adicione todos os servidores de origem a serem vinculados na lista à esquerda para a caixa à direita e, depois, insira o número da porta do servidor de origem.
![](https://main.qcloudimg.com/raw/7fd67c2a72a2c57d2c626596ce74cf4d.png)

## Etapa 5. Usar a conexão de aceleração

Após concluir as etapas acima, você pode usar a conexão para aceleração quando o status do listener se tornar **Normal**.
![](https://main.qcloudimg.com/raw/27c637a5321fde96212d7f48dc4a57de.png)

1. **Métodos de acesso**
	- Método 1: quando o cliente acessa o VIP e a porta, a aceleração do cliente ao servidor de destino pode ser implementada.
	- Método 2: quando o cliente acessa o nome de domínio e a porta de uma conexão de aceleração, a aceleração do cliente para o servidor de destino pode ser implementada.
	- Método 3: se o cliente acessa originalmente o nome de domínio, o nome de domínio pode ser resolvido para o registro CNAME de uma conexão de aceleração configurando o CNAME, e a aceleração do cliente para o servidor de destino pode ser implementada.
2. **Descrição do vínculo de aceleração**
   Os vínculos de aceleração são divididos nos seguintes tipos:
	- Cliente para VIP: rede pública.
	- VIP para o servidor de encaminhamento da região de origem: Direct Connect (rede privada).
	- O servidor de encaminhamento da região do servidor de origem para o servidor de origem: rede pública.
    ![](https://main.qcloudimg.com/raw/263f007ed5775c3a81ad9ba03a2f2cb6.png)
3. **Descrição do IP do servidor de encaminhamento**
Se uma regra de grupo de segurança for definida para o servidor de origem, primeiro é necessário clicar no **ID/Connection Name (ID/Nome da conexão)**, consultar o **Forwarding Server IP (IP do servidor de encaminhamento)** na guia **Connection Information (Informações de conexão)** e permitir o acesso ao servidor de origem por esses IPs, para implementar a aceleração conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/57f70164fc7b34b948a79740d035dfd4.png)
> ?Para mais informações sobre como obter IPs de clientes reais, consulte [Princípio básico](https://intl.cloud.tencent.com/document/product/608/14429) (apenas para TCP).
> 
4. **Estatísticas**
É possível exibir as estatísticas atuais e históricas na página **Statistics (Estatísticas)**. Para obter instruções, consulte [Estatísticas](https://intl.cloud.tencent.com/document/product/608/14425).
