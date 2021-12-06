## Visão geral do listener HTTPS
É possível criar um listener HTTPS para uma instância do CLB, no intuito de encaminhar solicitações HTTPS do cliente. O HTTPS é adequado para aplicativos HTTP em que a transferência de dados precisa ser criptografada.

## Pré-requisitos
Primeiro, é necessário [criar uma instância do CLB](https://intl.cloud.tencent.com/document/product/214/6149).

## Configuração de um listener HTTPS
### Etapa 1. Abra a guia **Listener Management (Gerenciamento de listener)**
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb).
2. Selecione **CLB Instance List (Lista de instâncias do CLB)** na barra lateral esquerda.
3. Na lista de instâncias, clique em um ID de instância para acessar a página de detalhes.
4. Abra a guia **Listener Management (Gerenciamento de listener)**. Você também pode acessar a página clicando em **Configure Listener (Configurar listener)**, na coluna **Operation (Operação)** de uma instância.
![](https://main.qcloudimg.com/raw/6c45e7c57eab15635e6a39ab37bdf69b.png)
5. A página "Listener Management (Gerenciamento de listener)" é conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/334e907f32a007a50d58a628b369425a.png)

### Etapa 2. Configure um listener
Clique em **Create (Criar)** em **HTTP/HTTPS Listener (Listener HTTP/HTTPS)** e configure um servidor HTTPS na janela pop-up.
#### 1. Crie um listener
| Item de configuração | Descrição | Exemplo |
| ------- | ------------------------ | ---------------------------------------- |
| Nome | Nome do listener | test-https-443 |
| Protocolo e porta de escuta | Protocolo e porta de escuta de um listener:<ul style="margin-bottom:0px;"><li>Protocolo de escuta: o CLB aceita vários protocolos, incluindo TCP, UDP, TCP SSL, HTTP e HTTPS. O HTTPS é usado neste exemplo.</li><li>Porta de escuta: uma porta usada para receber solicitações e encaminhá-las para o servidor de back-end. Intervalo de portas: 1 a 65535. Atualmente, estas portas estão reservadas e indisponíveis para os usuários: 843, 1020, 1433, 1434, 3306, 3389, 6006, 20000, 36000, 42222, 48369, 56000 e 65010.</li><li>As portas de escuta de cada instância do CLB devem ser exclusivas.</li></ul>| HTTPS:443 |
| Ativar SNI | Se o SNI estiver ativado, vários nomes de domínio de um listener podem ser configurados com certificados diferentes; se estiver desativado, vários nomes de domínio de um listener podem ser configurados com apenas um certificado. | Desativado |
| Método de análise SSL | A autenticação unilateral e a autenticação mútua são aceitas | Autenticação unilateral |
| Certificado do servidor | Você pode selecionar um certificado existente no [SSL Certificate Service](https://console.cloud.tencent.com/ssl) ou fazer o upload de um certificado | Selecione o certificado existente cc/UzxFoXsE |

A configuração específica do listener HTTPS criado é mostrada abaixo:
![](https://main.qcloudimg.com/raw/0aed0d551700632ec37636fd41d3f66c.png)

#### 2. Crie uma regra de encaminhamento
| Item de configuração | Descrição | Exemplo |
| ------- | ------------------------ | ---------------------------------------- |
| Nome de domínio | Nome de domínio de encaminhamento: <ul style="margin-bottom:0px;"><li>Comprimento: 1 a 80 caracteres. </li><li>O primeiro caractere não pode ser um sublinhado (_). </li><li>Nomes de domínio exatos e curinga são aceitos. </li><li>Regex é aceito. </li><li>Para ter acesso às regras de configuração detalhadas, consulte <a href="https://intl.cloud.tencent.com/document/product/214/9032">Encaminhamento de nomes de domínio e regras de URL da camada 7</a>.</li></ul> | www.exemplo.com |
| Nome de domínio padrão   | <li>Se todos os nomes de domínio do listener não corresponderem, o sistema direcionará as solicitações para o nome de domínio padrão, tornando o acesso padrão controlável.</li><li>Cada listener pode ser configurado com apenas um nome de domínio padrão.</li>| Ativado |
| HTTP 2.0   | Após a ativação do HTTP 2.0, as instâncias do CLB poderão receber solicitações HTTP 2.0. As instâncias do CLB acessam servidores de back-end por HTTP 1.1, não importa qual versão HTTP o cliente usa para acessá-las.| Ativado |
| Caminho URL | Caminho URL de encaminhamento:<ul style="margin-bottom:0px;"><li>Comprimento: 1 a 200 caracteres.</li><li>Regex é aceito.</li><li>Para ter acesso às regras de configuração detalhadas, consulte <a href="https://intl.cloud.tencent.com/document/product/214/9032">Encaminhamento de nomes de domínio e regras de URL da camada 7</a>.</li></ul> | /index |
| Método de balanceamento | Para listeners HTTPS, o CLB aceita três algoritmos de programação: round-robin ponderado (WRR), conexões mínimas ponderadas (WLC) e hash de IP.<ul style="margin-bottom:0px;"><li>WRR: as solicitações são entregues sequencialmente a diferentes servidores de back-end, de acordo com seus pesos. A programação é feita com base na **quantidade de conexões novas**, em que servidores com pesos mais altos passarão por mais pesquisas (ou seja, uma probabilidade maior), já servidores com o mesmo peso processam a mesma quantidade de conexões.</li><li>WLC: as cargas de servidores são estimadas de acordo com a quantidade de conexões ativas com eles. A programação é feita com base nas cargas e nos pesos do servidor. Se seus pesos forem os mesmos, os servidores com menos conexões ativas passarão por mais pesquisas (ou seja, uma probabilidade maior).</li><li>Hash de IP: as chaves hash são usadas para localizar os servidores correspondentes na tabela hash estática, com base nos IPs de origem das solicitações. Se um servidor estiver disponível e não sobrecarregado, as solicitações serão entregues a ele; caso contrário, será retornado um valor nulo.</li></ul>| WRR |
| Protocolo de back-end  | O protocolo de back-end é implantado entre uma instância do CLB e um servidor de back-end: <ul style="margin-bottom:0px;"> <li>Se o HTTP for selecionado como o protocolo de back-end, o serviço HTTP deve ser implantado no servidor de back-end.</li><li>Se o HTTPS for selecionado como o protocolo de back-end, o serviço HTTPS deve ser implantado no servidor de back-end, e a criptografia e descriptografia do serviço HTTPS consumirá mais recursos no servidor de back-end.</li></ul> |HTTP |
| Obtenção de IP do cliente | Ativada por padrão | Ativada |
| Compactação gzip | Ativada por padrão | Ativada |

Selecione o listener HTTPS para o qual deseja criar uma regra de encaminhamento e clique em **+** à direita. A configuração específica é mostrada abaixo:
![](https://main.qcloudimg.com/raw/c5c41aa58dc013581fcbdfd97d4d8ad4.png)

#### 3. Verificação de integridade
| Item de configuração | Descrição | Exemplo |
| ------- | ------------------------ | ---------------------------------------- |
| Status da verificação de integridade | A verificação de integridade pode ser ativada ou desativada. Em listeners HTTPS, as instâncias do CLB enviam solicitações HTTPS para a porta do servidor especificada, para realizar verificações de integridade. | Ativada |
| Nome de domínio de verificação | Nome de domínio de verificação de integridade: <ul style="margin-bottom:0px;"><li>Comprimento: 1 a 80 caracteres. </li><li>O padrão é o nome de domínio de encaminhamento.</li><li>Regex não é aceito. Caso seu nome de domínio de encaminhamento for um caractere curinga, você deve especificar um fixo (não regex) como o nome de domínio de verificação de integridade.</li><li>Caracteres aceitos: `a-z` `0-9` `.` `-`.</li></ul> | www.exemplo.com (valor padrão) |
| Caminho de verificação | Caminho de verificação de integridade: <ul style="margin-bottom:0px;"><li>Comprimento: 1 a 200 caracteres. </li><li>O padrão é `/` e deve começar com `/`.</li><li>Regex não é aceito. Recomendamos especificar um caminho de URL fixo (página estática) para verificações de integridade.</li><li>Caracteres aceitos: `a-z` `A-Z` `0-9` `.` `-` `_` `/` `=` `?`.</li></ul> | / (valor padrão) |
| Tempo limite de resposta | <li> Tempo limite máximo de resposta para verificações de integridade.</li><li>Se um servidor de back-end não responder dentro do tempo limite, a verificação de integridade será considerada anormal.</li><li>Intervalo de valores: 2 a 60 segundos. Valor padrão: 2 segundos.</li> | 2 segundos |
| Intervalo de verificações | <ul style="margin-bottom:0px;"><li>Intervalo entre duas verificações de integridade.</li><li>Intervalo de valores: 5 a 300 segundos. Valor padrão: 5 segundos.</li></ul> | 5 segundos |
| Limite não íntegro | <ul style="margin-bottom:0px;"><li>Se o resultado da verificação de integridade falhou por n (um valor personalizado) vezes consecutivas, o servidor de back-end não está íntegro e **Abnormal (Anormal)** é exibido no console.</li><li>Intervalo de valores: 2 a 10 vezes. Valor padrão: 3 vezes</li></ul> | 3 vezes |
| Limite íntegro | <ul style="margin-bottom:0px;"><li>Se o resultado da verificação de integridade foi bem-sucedido por n (um valor personalizado) vezes consecutivas, o servidor de back-end está íntegro e **Healthy (Íntegro)** é exibido no console.</li><li>Intervalo de valores: 2 a 10 vezes. Valor padrão: 3 vezes</li></ul> | 3 vezes |
| Método de solicitação HTTP | Método de solicitação HTTP para verificações de integridade. Valores válidos: GET (valor padrão) e HEAD: <ul style="margin-bottom:0px;"><li>Se HEAD for usado, o servidor retornará apenas as informações do cabeçalho HTTP, o que pode reduzir sobrecargas de back-end e melhorar a eficiência da solicitação. O servidor de back-end deve aceitar HEAD.</li><li>Se GET for usado, o servidor de back-end deve aceitar GET.</li></ul> | GET |
| Verificação do código de status HTTP | Se o código de status for dos selecionados, o servidor de back-end é considerado ativo (íntegro). Intervalo de valores: http_1xx, http_2xx, http_3xx, http_4xx e http_5xx. | Vários estão selecionados: http_1xx, http_2xx, http_3xx e http_4xx. |

A configuração específica da verificação de integridade é mostrada abaixo:
![](https://main.qcloudimg.com/raw/c0ef80ba20998381bde6fff98d9310ff.png)

#### 4. Persistência de sessão
| Item de configuração | Descrição | Exemplo |
| ------- | ------------------------ | ---------------------------------------- |
|Status de persistência de sessão | A persistência de sessão pode ser ativada ou desativada: <ul style="margin-bottom:0px;"><li>Se a persistência de sessão estiver ativada, o listener do CLB entregará as solicitações de acesso do mesmo cliente para o mesmo servidor de back-end.</li><li>A persistência de sessão HTTPS é implementada com base em cookies, que são implantados no cliente pela instância do CLB.</li><li>A persistência de sessão pode ser ativada para a programação de WRR, mas não para a programação de WLC ou hash de IP.</li></ul> | Ativada |
| Período de persistência de sessão | O período de persistência de sessão: <ul style="margin-bottom:0px;"><li>Se não houver nenhuma solicitação nova na conexão dentro do período de persistência de sessão, a sessão será automaticamente desconectada.</li><li>Intervalo de valores: 30 a 3.600 segundos.</li></ul> | 30 segundos |

A configuração específica da persistência de sessão é mostrada abaixo:
![](https://main.qcloudimg.com/raw/56f43a42cb15e9909c95122960b0ca75.png)

### Etapa 3. Vincule um servidor de back-end
1. Na página "Listener Management (Gerenciamento de listener)", selecione o servidor criado `HTTPS:443`. Clique em **+** à esquerda para expandir os nomes de domínio e caminhos de URL, selecione o caminho de URL desejado e exiba os servidores de back-end vinculados ao caminho à direita do listener.
![](https://main.qcloudimg.com/raw/1e61d584d4c2ca05ded255a7652e3396.png)
2. Clique em **Bind (Vincular)**, selecione o servidor de back-end em questão, configure a porta e o peso do servidor na janela pop-up.
 ① Adicionar porta: na caixa "Selected (Selecionada)" à direita, clique em **Add Port (Adicionar porta)** para adicionar várias portas à mesma instância do CVM, como as portas 80, 81 e 82.
 ② Porta padrão: insira a **Default Port (Porta padrão)** e, em seguida, selecione a instância do CVM. A porta de cada instância do CVM é a porta padrão.
![](https://main.qcloudimg.com/raw/26021bf7db700056e2cae6a5f3769f4c.png)

Após a conclusão dessas três etapas, a regra do listener HTTPS terá sido configurada conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/56de905b9c6fa1d1323c77de45790322.png)

### Etapa 4. Grupo de segurança (opcional)
É possível configurar um grupo de segurança do CLB para isolar o tráfego da rede pública. Para obter mais informações, consulte [Configuração de grupos de segurança do CLB](https://intl.cloud.tencent.com/document/product/214/14733)

### Etapa 5. Modifique e exclua um listener (opcional)
Caso precise modificar ou excluir um listener criado, clique no listener/nome de domínio/caminho de URL na guia **Listener Management (Gerenciamento de listener)** e selecione **Modify (Modificar)** ou **Delete (Excluir)**.
![](https://main.qcloudimg.com/raw/b1732ce6293a7b3382d6e8c8a9b18342.png)


