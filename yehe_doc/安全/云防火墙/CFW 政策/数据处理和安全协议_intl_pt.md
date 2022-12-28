## 1\. CONSIDERAÇÕES INICIAIS

Este Módulo se aplica se você usar o Cloud Firewall (“**Recurso**”). Esse Módulo está incorporado ao Contrato de Segurança e Processamento de Dados localizado em: (“[DPSA](https://intl.cloud.tencent.com/document/product/301/17347)”). Os termos utilizados, mas não definidos nesse Módulo, devem ter o significado dado a eles no DPSA. No caso de qualquer conflito entre o DPSA e esse Módulo, esse Módulo será aplicado conforme a inconsistência.

## 2\. PROCESSAMENTO

Processaremos os seguintes dados em conexão com o recurso:

| **Informações Pessoais**                                     | **Uso**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Dados do ativo:** informações sobre seus ativos na Tencent Cloud (hosts, endereços IP públicos, serviços web, gateway, VPC, sub-redes e bancos de dados) protegidos por este Recurso: ID/nome da instância do ativo, endereço IP, tipo de ativo, região, rede privada, identificação do recurso, tags do recurso, pico da largura de banda de entrada e saída, tráfego cumulativo de entrada e saída, ataque cibernético, portas expostas, vulnerabilidades expostas e segurança do host | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você.<br/>Observe que esses dados são compartilhados por meio de outros recursos da Tencent Cloud (de acordo com suas configurações e permissões de acesso), armazenados no TencentDB para MySQL ("**MySQL**") e Cloud Data Warehouse ("**Clickhouse**") e copiados com backup no recurso Cloud Object Storage ("**COS**"). |
| **Dados comerciais do CFW:** largura de banda de entrada e saída, taxa de fluxo cumulativa de entrada e saída, nome da abertura, porta exposta, dados de configuração de firewall (regras de controle de acesso, regras de proteção contra intrusão, modelo de proteção contra intrusão, lista de proibição, lista de liberação, lista de isolamento, configuração de investigação do honeypot, configuração de rede do honeypot, modelo de endereço), outros dados de configuração do firewall (dados do firewall ativados e desativados e dados de configuração da instância NATFW) | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você.<br/>Observe que esses dados são armazenados nos recursos MySQL e Clickhouse e é feito um backup no recurso COS. |
| **Dados do invasor:** dados de log de informações do invasor a serem identificados ou interceptados: endereço IP, localização geográfica, pacote do ataque (inclusive payload), tipo de ataque, tipo de evento do ataque, rastreamento do ataque e informações do invasor | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você.<br/>Observe que esses dados são armazenados nos recursos MySQL e Clickhouse e é feito um backup no recurso COS. |
| **Dados de registro:** <br/><li>Registros de controle de acesso \[que contém dados como direcionamento de regras, tempo necessário para acesso, origem do acesso, porta de origem, destino de acesso, porta de destino, contrato (contrato de serviço de comunicação de rede, protocolos TCP, UDP e HTTP) e políticas em vigor\]; <br/><li>Registros de prevenção contra invasão \[que contêm dados como tipo de evento do ataque, nível de risco, fonte de acesso externo, porta de origem, destino do acesso, porta de destino, contrato (contrato de serviço de comunicação de rede, protocolos TCP, UDP e HTTP), horário da ocorrência, políticas e origem da decisão\]; <br/><li>Registro de tráfego \[que contêm dados como direcionamento de tráfego, horário, origem de acesso externo, porta de origem, destino do acesso, porta de destino, contrato (contrato de serviço de comunicação de rede, protocolos TCP, UDP e HTTP), bytes de transmissão, região e operador\] e <br/><li>Registros de operação (que contêm dados como horário, conta da operação, tipo de operação, comportamento da operação, detalhes da operação e nível de risco) | Apenas processamos esses dados para fins de fornecer o Recurso a você, inclusive para permitir que você revise os registros relacionados aos ativos e/ou ataques aos ativos.<br/>Observe que estes dados são armazenados no recurso Elasticsearch Service, e um backup é realizado no recurso COS. |

## 3\. REGIÃO DO SERVIÇO

Conforme especificado no DPSA.

## 4\. SUBPROCESSADORES

Conforme especificado no DPSA.

## 5\. RETENÇÃO DE DADOS

Armazenaremos dados pessoais processados em conexão com o Recurso da seguinte forma (salvo se de outra forma exigido pelas Leis de Proteção de Dados aplicáveis):

| **Informações Pessoais** | **Política de Retenção**                                         |
| ------------------------ | ------------------------------------------------------------ |
| Dados do ativo               | Retemos esses dados até que você encerre sua assinatura do Recurso. Após isso, esses dados serão excluídos dentro de 14 dias. |
| Dados comerciais do CFW        | Por padrão, retemos esses dados por 7 dias (a menos que a capacidade de armazenamento exceda 50 GB. Neste caso, esses dados serão excluídos antecipadamente). Se você adquirir o serviço de análise de registros deste Recurso (que é interdependente do recurso Message Queue CKafka), reteremos esses dados por 6 meses (até o limite de capacidade de armazenamento que você determinou). Se você atingir o limite de capacidade de armazenamento, os dados serão substituídos em sobreposição. |
| Dados do invasor            | Por padrão, retemos esses dados por 7 dias (a menos que a capacidade de armazenamento exceda 50 GB. Neste caso, esses dados serão excluídos antecipadamente). Se você adquirir o serviço de análise de registros deste Recurso (que é interdependente do recurso Message Queue CKafka), reteremos esses dados por 6 meses (até o limite de capacidade de armazenamento que você determinou). Se você atingir o limite de capacidade de armazenamento, os dados serão substituídos em sobreposição. |
| Dados de registro                 | Por padrão, retemos esses dados por 7 dias (a menos que a capacidade de armazenamento exceda 50 GB. Neste caso, esses dados serão excluídos antecipadamente). Se você adquirir o serviço de análise de registros deste Recurso (que é interdependente do recurso Message Queue CKafka), reteremos esses dados por 6 meses (até o limite de capacidade de armazenamento que você determinou). Se você atingir o limite de capacidade de armazenamento, os dados serão substituídos em sobreposição. |

Você pode solicitar a exclusão desses dados pessoais de acordo com o DPSA.