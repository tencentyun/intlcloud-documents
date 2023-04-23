## 1\. CONSIDERAÇÕES INICIAIS

Este Módulo se aplica se houver uso do Tencent Container Security Service (“**Recurso**”). Este Módulo está incorporado ao Contrato de Segurança e Processamento de Dados localizado em (“[DPSA](https://intl.cloud.tencent.com/document/product/301/17347)”). Os termos utilizados, mas não definidos nesse Módulo, devem ter o significado dado a eles no DPSA. No caso de qualquer conflito entre o DPSA e esse Módulo, esse Módulo será aplicado conforme a inconsistência.

## 2\. PROCESSAMENTO

Processaremos os seguintes dados em conexão com o Recurso:

| **Informações pessoais**                                     | **Uso**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Dados básicos do ativo:** informações básicas sobre servidores, contêineres, imagens e clusters {informações de impressão digital de ativos (monitoramento de recursos, contas, portas, aplicações de software, processos, bancos de dados, aplicativos da Web, serviços da Web, estruturas da Web, sites, serviços de inicialização de pacotes Jar, tarefas agendadas, variáveis de ambiente, módulos do kernel), informações básicas do repositório de imagens \[endereço do repositório de imagens, tipo de repositório, nome da imagem, ID da imagem, versão da imagem, tamanho da imagem, riscos de segurança (incluindo vulnerabilidades de segurança, cavalos de Troia, informações confidenciais), histórico de composição\]} | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você.<br/>Observe que esses dados são armazenados e têm uma cópia de segurança em nossos recursos TencentDB para MongoDB (MongoDB) e TencentDB para MySQL (MySQL), temporariamente armazenados com backup no recurso Cloud Object Storage (COS)  e integrados com o Serviço de Hospedagem (conforme definido no módulo de Política de Privacidade para este Recurso) correspondente à sua assinatura. Se você adquiriu nosso cluster Tencent Kubernetes Engine (TKE), as informações básicas do repositório de imagens também serão compartilhadas conosco mediante sua autorização, com a finalidade de fornecer o Recurso a você (inclusive para realizar verificações de segurança). |
| **Dados para configuração do console:**<br/><li>Configuração de imagem, cluster, vulnerabilidade, baseline, arquivo,  detecção de log: detecção regular, rejeição de vulnerabilidade/baseline, confirmação de confiança ou isolamento de um arquivo, interceptação de processos, interceptação de imagens, interceptação de acesso à rede de contêineres)<li>Configuração da whitelist para escape de contêiner, shell reverso, verificação de arquivos, processos incomuns, adulteração de arquivos, execuções de queda do sistema com classificação de alto risco e outros recursos de prevenção de intrusão: condições da whitelist, intervalo de espelhamento efetivo. Outras informações de configuração: configurações de proteção relacionadas à atualização automática do servidor, configurações de renovação automática e configurações de alarme | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você conforme sua configuração específica.<br/>Observe que esses dados são armazenados e têm uma cópia de segurança em nossos recursos TencentDB para MongoDB (MongoDB) e TencentDB para MySQL (MySQL) e integrados com o Serviço de Hospedagem (conforme definido no módulo de Política de Privacidade para este Recurso) correspondente à sua assinatura. |

## 3\. REGIÃO DO SERVIÇO

Conforme especificado no DPSA.

## 4\. SUBPROCESSADORES

Conforme especificado no DPSA.

## 5\. RETENÇÃO DE DADOS

Armazenaremos dados pessoais processados em conexão com o Recurso da seguinte forma:

| **Informações pessoais**   | **Política de retenção**                                         |
| -------------------------- | ------------------------------------------------------------ |
| Dados básicos do ativo           | Retemos esses dados por, no mínimo, 180 dias. Os dados são retidos até o encerramento do uso do(s) Serviço(s) de Hospedagem correspondente(s). Neste caso, faremos a retenção temporariamente no recurso COS e os excluiremos (i) 30 dias depois ou (ii) após transcorrido o número mínimo de dias necessários para atingir o limite mínimo de retenção de dados de 180 dias (conforme aplicável). |
| Dados de configuração | Armazenados até a solicitação de exclusão, mediante a qual esses dados serão excluídos dentro de 30 dias úteis. Quando você não solicitar a exclusão, esses dados serão excluídos após 1 mês após o término do seu uso deste Recurso, a menos que exigido de outra forma pelas leis de proteção de dados aplicáveis. |

Você pode solicitar a exclusão desses dados pessoais de acordo com o DPSA.

## 6\. CONDIÇÕES ESPECIAIS

Você deve garantir que esse Recurso seja usado somente por usuários finais com a idade mínima exigida para que possam consentir com o processamento de seus dados pessoais. Pode haver diferenças dependendo da jurisdição em que o usuário final está localizado.

Este Recurso não se destina ao processamento de dados confidenciais. Você deve garantir que este Recurso não seja usado para transferir ou processar de outra forma quaisquer dados confidenciais por você ou seus usuários finais.