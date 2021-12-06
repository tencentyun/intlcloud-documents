## Visão geral do listener TCP SSL
É possível adicionar um listener TCP SSL a uma instância do CLB para encaminhar solicitações TCP criptografadas do cliente. O protocolo TCP SSL é adequado para cenários que exigem desempenho ultra-alto e descarregamento de TLS em grande escala. Com um listener TCP SSL, o servidor de back-end pode obter diretamente o IP real do cliente.

>?Atualmente, o listener TCP SSL é aceito apenas pelo CLB, mas não pelo CLB da rede clássica.
>

## Pré-requisitos
Primeiro, é necessário [criar uma instância do CLB](http://intl.cloud.tencent.com/document/product/214/6149).

## Configuração de um listener TCP SSL
### Etapa 1. Abra a página "Listener Management (Gerenciamento de listener)"
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb).
2. Selecione **Instance Management (Gerenciamento de instâncias)** na barra lateral esquerda.
3. Na lista de instâncias, clique no ID da instância a ser configurada para acessar a sua página de detalhes.
4. Clique na guia **Listener Management (Gerenciamento de listener)** ou clique em **Configure Listener (Configurar listener)** na coluna "Operation (Operação)".
![](https://main.qcloudimg.com/raw/ec8e5fd6668f0d58a88d6da66a4424e9.png)
5. A página "Listener Management (Gerenciamento de listener)" é conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/5d5f9cdb61a7ea3e4fd88036a7c01d0d.png)

### Etapa 2. Configure um listener
Clique em **Create (Criar)** em **TCP/UDP/TCP SSL Listener (Listener TCP/UDP/TCP SSL)** e configure um listener TCP SSL na janela pop-up.
#### 1. Configurações básicas
<table>
<thead>
<tr>
<th width="15%">Item de configuração</th>
<th width="70%">Descrição</th>
<th width="15%">Exemplo</th>
</tr>
</thead>
<tbody><tr>
<td>Nome</td>
<td>Nome do listener</td>
<td><span>test-tcpssl-9000&nbsp;&nbsp;&nbsp;&nbsp;</span></td>
</tr>
<tr>
<td>Protocolo do listener e porta de escuta</td>
<td>Protocolo do listener e porta de escuta. <br><li>Protocolo do listener: o CLB aceita vários protocolos, incluindo TCP, UDP, TCP SSL, HTTP e HTTPS. O TCP SSL é usado neste exemplo.</li><li>Porta de escuta: uma porta usada para receber solicitações e encaminhá-las para o servidor de back-end. Intervalo de portas: 1 a 65535.</li><li>A porta do listener deve ser exclusiva na mesma instância do CLB.</li></td>
<td>TCP SSL:9000</td>
</tr>
<tr>
<td>Método de análise SSL</td>
<td>A autenticação unilateral e a autenticação mútua são aceitas</td>
<td>Autenticação unilateral</td>
</tr>
<tr>
<td>Certificado do servidor</td>
<td>Você pode selecionar um certificado existente no <a href="https://console.cloud.tencent.com/ssl">SSL Certificate Service</a> ou fazer o upload de um certificado</td>
<td>Selecione o certificado existente cc/UzxFoXsE</td>
</tr>
<tr>
<td>Método de balanceamento</td>
<td>Para listeners TCP SSL, o CLB aceita dois algoritmos de programação: round-robin ponderado (WRR, na sigla em inglês) e conexões mínimas ponderadas (WLC, na sigla em inglês). <br><li>WRR: as solicitações são entregues sequencialmente a diferentes servidores de back-end, de acordo com seus pesos. A programação é feita com base na <strong>quantidade de conexões novas</strong>, em que servidores com pesos mais altos passarão por mais pesquisas (ou seja, uma probabilidade maior), já servidores com o mesmo peso processam a mesma quantidade de conexões.</li><li>WLC: as cargas de servidores são estimadas de acordo com a quantidade de conexões ativas com eles. A programação é feita com base nas cargas e nos pesos do servidor. Se seus pesos forem os mesmos, os servidores com menos conexões ativas passarão por mais pesquisas (ou seja, uma probabilidade maior).</li></td>
<td>WRR</td>
</tr>
</tbody></table>

A configuração específica do listener TCP SSL criado é mostrada abaixo:
![](https://main.qcloudimg.com/raw/7107604b6c756183c4ea329c20bcbf00.png)

#### 2. Verificação de integridade
| Item de configuração | Descrição | Exemplo |
| ------- | ------------------------ | ---------------------------------------- |
| Status da verificação de integridade | A verificação de integridade pode ser ativada ou desativada. Em listeners TCP SSL, as instâncias do CLB enviam pacotes SYN para a porta do servidor especificada, no intuito de realizar verificações de integridade. | Ativada |
| Tempo limite de resposta | <li>Tempo limite máximo de resposta para verificações de integridade.</li><li>Se um servidor de back-end não responder corretamente dentro do tempo limite, ele é considerado anormal.</li><li>Intervalo de valores: 2 a 60 s. Valor padrão: 2 s.</li> | 2 s |
| Intervalo de verificações | <li>Intervalo entre duas verificações de integridade.</li><li>Intervalo de valores: 5 a 300 s. Valor padrão: 5 s.</li> | 5 s |
| Limite não íntegro | <li>Se os resultados da verificação de integridade recebidos n vezes (n é o número inserido) seguidas forem falhas, a instância será considerada não íntegra e o status exibido no console será **Abnormal (Anormal)**.</li><li>Intervalo de valores: 2 a 10. Valor padrão: 3.</li> | 3 vezes |
| Limite íntegro | <li>Se os resultados da verificação de integridade recebidos n vezes (n é o número inserido) seguidas forem sucessos, a instância será considerada íntegra e o status exibido no console será **Healthy (Íntegro)**.</li><li>Intervalo de valores: 2 a 10. Valor padrão: 3.</li> | 3 vezes |

A configuração específica da verificação de integridade é mostrada abaixo:
![](https://main.qcloudimg.com/raw/6d57f6df374edba777d3a8841f50adc2.png)

#### 3. Persistência de sessão (não aceita atualmente)
![](https://main.qcloudimg.com/raw/8cde7bd598be6bdb8d5c300e32c90659.png)

### Etapa 3. Vincule um servidor de back-end
1. Na página "Listener Management (Gerenciamento de listener)", clique no listener criado `TCP SSL:9000` para exibir os servidores de back-end vinculados à direita do listener.
![](https://main.qcloudimg.com/raw/6dc93b60bb493c58a067604d69dd309b.png)
2. Clique em **Bind (Vincular)** e selecione o servidor de back-end a ser vinculado e configure a porta e o peso do servidor na janela pop-up.
 1. Adicionar porta: na caixa "Selected (Selecionada)" à direita, clique em **Add Port (Adicionar porta)** para adicionar várias portas à mesma instância do CVM, como as portas 80, 81 e 82.
 2. Porta padrão: insira a "Default Port (Porta padrão)" e, em seguida, selecione a instância do CVM. A porta de cada instância do CVM é a porta padrão.
![](https://main.qcloudimg.com/raw/0285f5f04916c94c9549baae5bdffda6.png)

Após a conclusão dessas três etapas, a regra do listener TCP SSL terá sido configurada conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/bfa1e03aec1f29b24d9bf9929edef49d.png)

### Etapa 4. Grupo de segurança (opcional)
É possível configurar um grupo de segurança do CLB para isolar o tráfego da rede pública. Para obter mais informações, consulte [Configuração de um grupo de segurança do CLB](https://intl.cloud.tencent.com/document/product/214/14733).

### Etapa 5. Modifique/exclua um listener (opcional)
Caso precise modificar ou excluir um listener criado, clique no listener na página "Listener Management (Gerenciamento de listener)" e selecione **Modify (Modificar)** ou **Delete (Excluir)**.
![](https://main.qcloudimg.com/raw/8a3ddb3d362434e283ec563dcc9e14f5.png)
