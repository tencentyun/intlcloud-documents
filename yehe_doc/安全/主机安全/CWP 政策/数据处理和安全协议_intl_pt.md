## 1\. CONSIDERAÇÕES

Este Módulo se aplica se você usa Cloud Workload Protection Platform (CWPP) (“**Recurso**”). Este Módulo está incorporado ao Contrato de Processamento de Dados e Segurança localizado no (“[DPSA](https://intl.cloud.tencent.com/document/product/301/17347)”). Os termos utilizados, mas não definidos nesse Módulo, devem ter o significado dado a eles no DPSA. No caso de qualquer conflito entre o DPSA e esse Módulo, esse Módulo será aplicado conforme a inconsistência.

## 2\. PROCESSAMENTO

Processaremos os seguintes dados em conexão com o Recurso:

| **Informações pessoais**                                     | **Uso**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Informação de recurso protegido pelo cliente: <br><li>**Para proteção dos servidores Tencent Cloud**: ID da aplicação, número de identificação único, suas informações dos servidores (nome, endereço IP, tipo, sistema operacional, versão do agente, instalação do agente data, hora do último login, status online, componentes instalados e nível de segurança) <br><li>**Para proteção dos servidores que não são da Tencent Cloud**: monitoramento de recurso, conta, porta, aplicativo de software, processo, banco de dados, aplicação Web, serviço Web, framework para Web, site, pacote jar, serviço de inicialização, tarefa agendada, variáveis de ambiente, módulo kernel | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você. <br/> Observe que, a menos que autorizado por você, não temos acesso aos dados pessoais armazenados no banco de dados, caso existam, nem controle sobre os dados.<br/> Observe que esses dados estão armazenados e têm uma cópia de segurança no nosso recurso TencentDB for MySQL (MySQL). |
| Informação de incidente de segurança: **para a assinatura gratuita do Recurso:** <br><li>Informação de detecção de intrusão: eventos como login anormal do servidor cliente, quebra de senha, informações sobre eventos relevantes (servidor UUID, detalhes de eventos, nível de ameaça e status de processamento). **Para a assinatura paga do Recurso, os seguintes itens são processados adicionalmente:** <br><li> Informações de detecção sobre falhas de segurança dos servidores: UUID dos servidores afetados, nome e descrições das falhas de segurança detectadas, estado atual, data e hora da detecção mais recente; <br><li>Linha de base de segurança informação: UUID dos servidores, nome da linha de base de segurança, tipo de detecção, níveis de ameaça à segurança, status atual, data e hora da última detecção; <br><li>Relatório de segurança dos servidores: número total de login anormal do cliente registrado, resultados da varredura de vulnerabilidade, quebra de senha e varredura de arquivos maliciosos; números e tipos de assinaturas compradas do Recurso por você. | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você. Também podemos anonimizar e desidentificar determinadas informações de incidentes de segurança para melhorar o Recurso. <br/>Observe que esses dados são armazenados e têm uma cópia de segurança em nosso recurso MySQL. |
| Dados de configuração do cliente: <br><li>Configuração de detecção de vulnerabilidades/linhas de base/arquivos: configurações regulares de detecção, vulnerabilidades/linhas de base ignoradas, arquivos confiáveis, arquivos em quarentena; <br><li>Configuração de listas de permissões de funções de prevenção de intrusão: condições da lista de permissões, servidores contemplados; <br><li>Outras configurações: configurações de atualização de proteção automática, configurações de renovação automática e configurações de alarme. | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você conforme sua configuração específica. <br/>Observe que esses dados são armazenados e têm uma cópia de segurança em nosso recurso MySQL. |

## 3\. REGIÃO DE SERVIÇO

Conforme especificado no DPSA.

## 4\. SUBPROCESSADORES

Conforme especificado no DPSA.

## 5\. RETENÇÃO DE DADOS

Armazenaremos dados pessoais processados em conexão com o Recurso da seguinte forma:

| **Informações pessoais**                                     | **Política de retenção**                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Recurso protegido pelo cliente Informação  Incidente de segurança Informação Dados de configuração do cliente | Retemos esses dados até que você os exclua manualmente. Caso contrário, quando você excluir sua assinatura de uso do Recurso ou excluir sua conta, excluiremos esses dados em até 7 dias. |

Você pode solicitar a exclusão desses dados pessoais de acordo com o DPSA.

## 6\. CONDIÇÕES ESPECIAIS

Você deve garantir que esse Recurso seja usado somente por usuários finais com a idade mínima exigida para que possam consentir com o processamento de seus dados pessoais. Pode haver diferenças dependendo da jurisdição em que o usuário final está localizado.