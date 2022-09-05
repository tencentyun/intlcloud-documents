## 1\. **CONSIDERAÇÕES INICIAIS**

Este módulo se aplica se você usar o Customer Identity and Access Management (Gerenciamento de Identidade e Acesso do Usuário, CIAM) (“**Recurso**”). Este Módulo está incorporado ao Contrato de Segurança e Processamento de Dados localizado em (“[DPSA](https://intl.cloud.tencent.com/document/product/301/17347 )”). Os termos utilizados, mas não definidos nesse Módulo, devem ter o significado dado a eles no DPSA. No caso de qualquer conflito entre o DPSA e esse Módulo, esse Módulo será aplicado conforme a inconsistência.


## 2\. **PROCESSAMENTO**

Processaremos os seguintes dados em conexão com o Recurso:

| **Informações Pessoais**                                     | **Uso**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Dados de configuração de gerenciamento do usuário:** Atributos predefinidos do usuário determinados por você (descrição, nacionalidade, posição do usuário, data de aniversário, sexo e endereço); grupo de usuários (lista de grupos de usuários, nome, observações, tempo de criação e lista de usuários incluída). | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você.<br/> Observe que esses dados são integrados, armazenados e têm uma cópia de segurança em nosso recurso TencentDB for MongoDB (MongoDB), e também estão integrados ao nosso recurso TencentDB for Redis (Redis). |
| **Dados de gerenciamento de aplicações:** <br><li>Aplicação M2M: ícone, nome da aplicação, tipo de aplicação, setor, ID do cliente, senha, descrição da aplicação, validade do token de acesso, domínio de segurança e URI configurado específico do CORS;<br><li>Aplicação de miniprograma: download de aplicação de estilo, guia de configuração, ícone, nome da aplicação, tipo de aplicação, setor, ID do cliente, senha, descrição da aplicação, redirecionamento de URI, redirecionamento de logout de URI, validade do token de acesso, token de atualização, requisições, configuração do processo de registro e login, URI do domínio de segurança da configuração específica do CORS;<br><li>Aplicativo de celular: ícone, nome do aplicativo, tipo de aplicativo, setor, ID do cliente, senha, descrição do aplicativo, redirecionamento de URI, redirecionamento de logout de URI, validade do token de acesso, token de atualização, requisições, processo de registro, processo de login, processo de autenticação multifator (Multi Factor Authentication, MFA), processo de recuperação de senha, processo de recuperação de nome de usuário, gerenciamento de protocolo, URI do domínio de segurança da configuração específica do CORS;<br><li>Aplicação web: ícone, nome do aplicativo, tipo de aplicativo, setor, ID do cliente, senha, descrição da aplicação, redirecionamento de URI, redirecionamento de logout de URI, validade do token de acesso, token de atualização, requisições, processo de registro, processo de login, processo de autenticação multifator (MFA), processo de recuperação de senha, processo de recuperação de nome de usuário, gerenciamento de protocolo, URI do domínio de segurança da configuração específica do CORS. | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você.  <br/>Observe que esses dados estão integrados, armazenados e têm uma cópia de segurança em nossos recursos Cloud Object Storage (COS) e MongoDB. |
| **Dados de configurações de sincronização de dados:** Nome da origem dos dados, ID de origem dos dados, descrição, guia de configuração, ID do cliente, senha do cliente, token, URL do usuário, URL do grupo. | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você.<br/>Observe que esses dados estão integrados, armazenados e têm uma cópia de segurança em nosso recurso MongoDB. |
| **Dados de gerenciamento de certificados** <br><li>Fonte de autenticação geral: ícone de fonte de autenticação, nome da fonte de autenticação, atributo da fonte de autenticação, descrição da fonte de autenticação, política de senha, comprimento do código de verificação por SMS, período de validade do código de verificação por SMS, comprimento do código de verificação por e-mail, período de validade do código de verificação por e-mail; <br><li>Fonte de autenticação social: ícone da fonte de autenticação, nome da fonte de autenticação, descrição da fonte de autenticação, ID do aplicativo, chave de senha do aplicativo, mapeamento de atributos. | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você.<br/>Observe que esses dados estão integrados, armazenados e têm uma cópia de segurança em nossos recursos COS e MongoDB. Se você adquiriu nossos serviços de mensagem de texto (SMS) e Serviço de E-mail Simples (Simple Email Service, SES), os dados gerais da fonte de autenticação também estão integrados aos nossos recursos de SMS e SES. |
| **Dados de personalização:** <br><li>Configuração do nome de domínio : conjunto de nomes de domínio e nome fornecido por você (ou, se necessário, nome de domínio padrão fornecido por nós); <br><li>Configuração do modelo (configurações relativas à opção do uso de recursos de SMS e/ou SES): modelo de SMS (servidor SMS, assinatura de login por SMS, ID de modelo de SMS); modelo de caixa de correio eletrônico (servidor de e-mail, ID do modelo de código de verificação, recuperação de ID do modelo de senha, recuperação de ID do modelo de nome de usuário); <br><li>Modelo de autenticação de nome real \[provedor de serviço de autenticação de nome real, credenciais de segurança do requisitor de API (ID secreto, chave secreta)\]. | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você.<br/>Observe que esses dados estão integrados, armazenados e têm uma cópia de segurança em nosso recurso MongoDB. Se você adquiriu nossos serviços de SMS e SES, os dados de configuração de modelos também estão integrados aos nossos recursos de SMS e SES. |
| **Dados de atributos de usuário incorporados:** horário de login incorreto, horário de bloqueio, ID do usuário Alipay, endereço de e-mail, horário de atualização, fuso horário do usuário, localização geográfica, último horário de login, número de telefone, horário de criação, grupo do usuário, agrupamento de usuários, apelido do usuário, ID do usuário, nome do usuário, ID aberto do WeChat, se o usuário fez login pela primeira vez, fonte do usuário, ID do Wechatunion, status do usuário, ID aberto QQ, ID do QQunion, se o usuário tem autenticação do nome real, nome do método de autenticação do nome real, número de identificação, se a conta é principal ou não. | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você.<br/>Observe que esses dados são integrados, armazenados e copiados para segurança em nosso recurso MongoDB e também estão integrados em nosso recurso Redis. Se você adquiriu nossos serviços de SMS e SES, o número de telefone também está integrado ao nosso recurso de SMS, e o endereço de e-mail é integrado ao nosso recurso de SES. |


## 3\. **REGIÃO DO SERVIÇO**

Conforme especificado no DPSA.


## 4\. **SUBPROCESSADORES**

Conforme especificado no DPSA.


## 5\. **RETENÇÃO DE DADOS**

Armazenaremos dados pessoais processados em conexão com o Recurso da seguinte forma:

| **Informações Pessoais**                                     | **Política de Retenção**                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Dados de configuração de gerenciamento de usuário Dados de gerenciamento de aplicações Dados de configurações de sincronização de dados Dados de gerenciamento de certificados Dados de personalização  Dados de atributos de usuário incorporados | Retemos esses dados até que você os exclua manualmente. Caso contrário, quando você excluir sua conta ou encerrar o uso do recurso, excluiremos esses dados. |

Você pode solicitar a exclusão desses dados pessoais de acordo com o DPSA.


## 6\. **CONDIÇÕES ESPECIAIS**

Você deve garantir que esse Recurso seja usado somente por usuários finais com a idade mínima exigida para que possam consentir com o processamento de seus dados pessoais. Pode haver diferenças dependendo da jurisdição em que o usuário final está localizado.