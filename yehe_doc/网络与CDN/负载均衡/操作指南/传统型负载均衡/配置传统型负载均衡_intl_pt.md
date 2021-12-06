Após a criação de uma instância do CLB clássico, é necessário configurar um listener para ela. O listener capta as solicitações na instância e distribui o tráfego para servidores de back-end, com base na política de balanceamento de carga.

## Pré-requisitos
Primeiro, você precisa [criar uma instância do CLB](https://intl.cloud.tencent.com/document/product/214/6149) e selecionar "Classic CLB (CLB clássico)" para **Instance type (Tipo de instância)**.
>!Atualmente, existem dois tipos de contas do Tencent Cloud: faturamento por EIP/CLB e faturamento por CVM. Todas as contas do Tencent Cloud registradas após 17 de junho de 2020, às 00:00:00, são contas com faturamento por EIP/CLB. Para contas do Tencent Cloud registradas antes de 17 de junho de 2020, [verifique os tipos de conta](https://intl.cloud.tencent.com/document/product/684/15246) no console. As contas de faturamento por EIP/CLB não aceitam mais o CLB clássico. Agora você só pode adquirir uma instância do CLB.

## Configuração do listener
### Etapa 1. Abra a página **Listener Management (Gerenciamento de listener)**
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb).
2. Selecione **CLB Instance List (Lista de instâncias do CLB)** na barra lateral esquerda.
3. Na página **Instance Management (Gerenciamento de instâncias)**, clique no ID/Nome da instância a ser configurada para acessar a página de detalhes dela.
4. Selecione a guia **Listener Management (Gerenciamento de listener)** ou clique em **Configure listener (Configurar listener)** na coluna **Operation (Operação)** na página **Instance Management (Gerenciamento de instâncias)**.
![](https://main.qcloudimg.com/raw/3c63dacadca27ea0bb84d015954d741a.png)
5. A página **Listener Management (Gerenciamento de listener)** é conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/61ff0540f4eccdc24cb5f06f76af5299.png)

### Etapa 2. Configure um listener
Clique em **Create (Criar)** em **Listener Management (Gerenciamento de listener)** e configure um listener TCP na janela pop-up.
#### 1. Configuração básica
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
<td>Nome do listener.</td>
<td><span>test-tcp-80&nbsp;&nbsp;&nbsp;&nbsp;</span></td>
</tr>
<tr>
<td>Portas do protocolo do listener</td>
<td>Protocolo do listener e porta de escuta<br><li>Protocolo do listener: o CLB aceita protocolos como TCP, UDP, HTTP e HTTPS. Esse exemplo usa o TCP.</li><li>Porta de escuta: usada para receber e encaminhar solicitações para servidores de back-end. O intervalo de portas é 1 a 65535.</li><li>A porta de escuta deve ser exclusiva na mesma instância do CLB.</li></td>
<td>TCP:80</td>
</tr>
<tr>
<td>Porta de back-end</td>
<td>A porta por meio da qual a instância do CVM fornece serviços, recebe e processa o tráfego de uma instância do CLB.</td>
<td>80</td>
</tr>
</tbody></table>

Para criar um listener TCP, conclua a configuração básica conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/3773d74e1c13df06f7d70e89e3820624.png)

#### 2. Configuração avançada
| Item de configuração | Descrição | Exemplo |
| ------- | ------------------------ | ---------------------------------------- |
| Método de equilíbrio | Para listeners TCP, o CLB aceita dois algoritmos de programação: round-robin ponderado (WRR) e conexão mínima ponderada (WLC).<br><li>WRR: os pedidos são encaminhados para servidores de back-end diferentes sequencialmente de acordo com seus pesos. A programação é baseada na <strong>quantidade de conexões novas</strong>, em que servidores com pesos maiores têm mais sondagens (ou seja, uma probabilidade maior) e servidores com o mesmo peso processam a mesma quantidade de conexões.</li><li>WLC: as cargas nos servidores são estimadas de acordo com a sua quantidade de conexões ativas. A programação é baseada em cargas e pesos do servidor. Se seus pesos forem iguais, os servidores de back-end com menos conexões ativas terão mais sondagens (ou seja, uma probabilidade maior).</li> | WRR |
| Persistência de sessão | Se deve ativar ou desativar a persistência de sessão.<br><li>Depois que a persistência de sessão for ativada, o listener do CLB distribuirá as solicitações de acesso do mesmo cliente para o mesmo servidor de back-end.</li><li>A persistência de sessão TCP é implementada com base no endereço IP do cliente. As solicitações de acesso do mesmo endereço IP são encaminhadas para o mesmo servidor de back-end.</li><li>A persistência de sessão pode ser ativada para a programação de WRR, mas não para a programação de WLC.</li> | Ativada |
| Tempo de espera | O tempo de persistência de sessão.<br><li>Se não houver nenhuma solicitação nova na conexão dentro do tempo de persistência de sessão, a persistência de sessão será automaticamente desconectada.</li><li>Intervalo de valores: 30 a 3.600 segundos.</li> | 30 s |

Conclua a configuração conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/ddc22b9e0638eb8f2d8803ffee6335f8.png)

#### 3. Verificação de integridade
| Item de configuração | Descrição | Exemplo |
| ------- | ------------------------ | ---------------------------------------- |
| Verificação de integridade | Se deve ativar ou desativar a verificação de integridade. Em listeners TCP, as instâncias do CLB enviam pacotes SYN para portas de servidor especificadas, a fim de realizar verificações de integridade. | Ativada |
| Protocolo de verificação | A ser adicionada. | A ser adicionado |
| Porta de verificação | A ser adicionada. | A ser adicionado |
| Tempo limite de resposta | <li> O tempo limite máximo de resposta para verificação de integridade.</li><li>Se um servidor de back-end não responder dentro do tempo limite, ele será considerado não íntegro.</li><li>Intervalo de valores: 2 a 60 segundos. Valor padrão: 2 s.</li> | 2 s |
| Intervalo de verificações | <li>Intervalo entre duas verificações de integridade.</li><li>Intervalo de valores: 5 a 300 segundos. Valor padrão: 5 s.</li> | 5 s |
| Limite não íntegro | <li>Se a verificação de integridade retornar `failure (falha)` por n vezes consecutivas (n é definido pelo usuário), o servidor de back-end não está íntegro e o status **unhealthy (não íntegro)** é exibido no console.</li><li>Intervalo de valores: 2 a 10 vezes. Valor padrão: 3 vezes</li> | 3 vezes |
| Limite íntegro | <li>Se a verificação de integridade retornar `success (sucesso)` por n vezes consecutivas (n é definido pelo usuário), o servidor de back-end está íntegro e o status **healthy (íntegro)** é exibido no console.</li><li>Intervalo de valores: 2 a 10 vezes. Valor padrão: 3 vezes.</li> | 3 vezes |

Conclua a configuração de verificação de integridade conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/a05f5672d4999a60f6e01b74df38fc6b.png)

### Etapa 3. Vincule um servidor de back-end
Clique em **Bind (Vincular)** na página **Listener Management (Gerenciamento de listener)** e selecione o servidor de back-end a ser vinculado na janela pop-up, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/7ad71ca47183798e8cb54dfd25b9cdb3.png)

A configuração é conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/ef63b9817686f4743408cb6e7fba19f3.png)

>?Se você configurar vários listeners para uma instância do CLB clássico e vincular vários servidores de back-end, cada listener encaminhará solicitações para todos os servidores de back-end com base em sua configuração.

### Etapa 4. Grupo de segurança (opcional)
É possível configurar um grupo de segurança do CLB para isolar o tráfego da rede pública. Para obter mais informações, consulte [Configuração de um grupo de segurança do CLB](https://intl.cloud.tencent.com/document/product/214/14733).

### Etapa 5. Modifique ou exclua um listener (opcional)
Se você precisar modificar ou excluir um listener existente, selecione-o na página **Listener Management (Gerenciamento de listener)** e clique em **Modify (Modificar)** ou **Delete (Excluir)**.
![](https://main.qcloudimg.com/raw/b4003107882decddea5828bf887dab40.png)
