## Visão geral do listener TCP
É possível criar um listener TCP para uma instância do CLB, no intuito de encaminhar solicitações TCP do cliente. O TCP é adequado para cenários com altos requisitos de confiabilidade e precisão de dados, mas requisitos relativamente baixos de velocidade de transferência, como transferência de arquivos, mensagens de e-mail e login remoto. Para listeners TCP, o servidor de back-end pode obter diretamente o IP real do cliente.

## Pré-requisitos
Primeiro, é necessário [criar uma instância do CLB](http://intl.cloud.tencent.com/document/product/214/6149).

## Configuração de um listener TCP
### Etapa 1. Abra a página "Listener Management (Gerenciamento de listener)"
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb).
2. Selecione **Instance Management (Gerenciamento de instâncias)** na barra lateral esquerda.
3. Na lista de instâncias, clique no ID da instância a ser configurada para acessar a sua página de detalhes.
4. Clique na guia **Listener Management (Gerenciamento de listener)** ou clique em **Configure Listener (Configurar listener)** na coluna "Operation (Operação)".
![](https://main.qcloudimg.com/raw/c222786c42bace0f1366def6a5a3d1b2.png)
5. A página "Listener Management (Gerenciamento de listener)" é conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/31f6e12c1520d3cb4759b8e063bcdb40.png)

### Etapa 2. Configure um listener
Clique em **Create (Criar)** em **TCP/UDP/TCP SSL Listener (Listener TCP/UDP/TCP SSL)** e configure um listener TCP na janela pop-up.
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
<td><span>test-tcp-80&nbsp;&nbsp;&nbsp;&nbsp;</span></td>
</tr>
<tr>
<td>Protocolo do listener e porta de escuta</td>
<td>Protocolo do listener e porta de escuta. <br><li>Protocolo do listener: o CLB aceita vários protocolos, incluindo TCP, UDP, HTTP e HTTPS. O TCP é usado neste exemplo.</li><li>Porta de escuta: uma porta usada para receber solicitações e encaminhá-las para o servidor de back-end. Intervalo de portas: 1 a 65535.</li><li>A porta do listener deve ser exclusiva na mesma instância do CLB.</li></td>
<td>TCP:80</td>
</tr>
<tr>
<td>Método de balanceamento</td>
<td>Para listeners TCP, o CLB aceita dois algoritmos de programação: round-robin ponderado (WRR, na sigla em inglês) e conexões mínimas ponderadas (WLC, na sigla em inglês). <br><li>WRR: as solicitações são entregues sequencialmente a diferentes servidores de back-end, de acordo com seus pesos. A programação é feita com base na <strong>quantidade de conexões novas</strong>, em que servidores com pesos mais altos passarão por mais pesquisas (ou seja, uma probabilidade maior), já servidores com o mesmo peso processam a mesma quantidade de conexões.</li><li>WLC: as cargas de servidores são estimadas de acordo com a quantidade de conexões ativas com eles. A programação é feita com base nas cargas e nos pesos do servidor. Se seus pesos forem os mesmos, os servidores com menos conexões ativas passarão por mais pesquisas (ou seja, uma probabilidade maior).</li></td>
<td>WRR</td>
</tr>
</tbody></table>

A configuração específica do listener TCP criado é mostrada abaixo:
![](https://main.qcloudimg.com/raw/089a45fae94bda88e28ee30dc29159e5.png)

#### 2. Verificação de integridade
| Item de configuração | Descrição | Exemplo |
| ------- | ------------------------ | ---------------------------------------- |
| Status da verificação de integridade | A verificação de integridade pode ser ativada ou desativada. Em listeners TCP, as instâncias do CLB enviam pacotes SYN para a porta do servidor especificada, no intuito de realizar verificações de integridade. | Ativada |
| Tempo limite de resposta | <li>Tempo limite máximo de resposta para verificações de integridade.</li><li>Se um servidor de back-end não responder corretamente dentro do tempo limite, ele é considerado anormal.</li><li>Intervalo de valores: 2 a 60 s. Valor padrão: 2 s.</li> | 2 s |
| Intervalo de verificações | <li>Intervalo entre duas verificações de integridade.</li><li>Intervalo de valores: 5 a 300 s. Valor padrão: 5 s.</li> | 5 s |
| Limite não íntegro | <li>Se os resultados da verificação de integridade recebidos n vezes (n é o número inserido) seguidas forem falhas, a instância será considerada não íntegra e o status exibido no console será **Abnormal (Anormal)**.</li><li>Intervalo de valores: 2 a 10. Valor padrão: 3.</li> | 3 vezes |
| Limite íntegro | <li>Se os resultados da verificação de integridade recebidos n vezes (n é o número inserido) seguidas forem sucessos, a instância será considerada íntegra e o status exibido no console será **Healthy (Íntegro)**.</li><li>Intervalo de valores: 2 a 10. Valor padrão: 3.</li> | 3 vezes |

A configuração específica da verificação de integridade é mostrada abaixo:
![](https://main.qcloudimg.com/raw/9c19b0d3db249d2bb37f5dc7c8238384.png)

#### 3. Persistência de sessão
| Item de configuração | Descrição | Exemplo |
| ------- | ------------------------ | ---------------------------------------- |
| Status de persistência de sessão | A persistência de sessão pode ser ativada ou desativada. <br><li>Se a persistência de sessão estiver ativada, o listener do CLB entregará as solicitações de acesso do mesmo cliente para o mesmo servidor de back-end.</li><li>A persistência de sessão TCP é implementada com base nos endereços IP do cliente, ou seja, as solicitações de acesso do mesmo endereço IP são encaminhadas para o mesmo servidor de back-end.</li><li>A persistência de sessão pode ser ativada para a programação de WRR, mas não para a programação de WLC.</li> | Ativada |
| Tempo de persistência de sessão | O tempo de persistência de sessão. <br><li>Se não houver nenhuma solicitação nova na conexão dentro do tempo de persistência de sessão, a sessão será interrompida automaticamente.</li><li>Intervalo de valores: 30 a 3.600 s.</li> | 30 s |

A configuração específica da persistência de sessão é mostrada abaixo:
![](https://main.qcloudimg.com/raw/449fc0611325c37aafe9815921b2471d.png)

### Etapa 3. Vincule um servidor de back-end
1. Na página "Listener Management (Gerenciamento de listener)", clique no listener criado `TCP:80` para exibir os servidores de back-end vinculados à direita do listener.
![](https://main.qcloudimg.com/raw/7082206ee1b28031d6a11f9b887684dd.png)
2. Clique em **Bind (Vincular)** e selecione o servidor de back-end a ser vinculado e configure a porta e o peso do servidor na janela pop-up.
 1. Adicionar porta: na caixa "Selected (Selecionada)" à direita, clique em **Add Port (Adicionar porta)** para adicionar várias portas à mesma instância do CVM, como as portas 80, 81 e 82.
 2. Porta padrão: insira a "Default Port (Porta padrão)" e, em seguida, selecione a instância do CVM. A porta de cada instância do CVM é a porta padrão.
![](https://main.qcloudimg.com/raw/4c749af9416903a471a72c67e00125e1.png)

Após a conclusão dessas três etapas, a regra do listener TCP terá sido configurada conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/9dc06223e43fe6216f8a1cc74821dc48.png)

### Etapa 4. Grupo de segurança (opcional)
É possível configurar um grupo de segurança do CLB para isolar o tráfego da rede pública. Para obter mais informações, consulte [Configuração de um grupo de segurança do CLB](https://intl.cloud.tencent.com/document/product/214/14733).

### Etapa 5. Modifique/exclua um listener (opcional)
Caso precise modificar ou excluir um listener criado, clique no listener na página "Listener Management (Gerenciamento de listener)" e selecione **Modify (Modificar)** ou **Delete (Excluir)**.
![](https://main.qcloudimg.com/raw/d4d79dd4618bbe5cea3f36d719ddf5ec.png)
