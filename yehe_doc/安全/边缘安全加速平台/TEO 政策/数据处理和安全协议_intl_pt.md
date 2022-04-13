## 1\. CONSIDERAÇÕES INICIAIS

Este Módulo é aplicável se você usa o TencentCloud EdgeOne (“**Recurso**”). Este módulo está incorporado ao contrato de segurança e privacidade de dados localizado no [DPSA](https://intl.cloud.tencent.com/document/product/301/17347). Os termos utilizados, mas não definidos neste Módulo, devem ter o significado dado a eles no DPSA. No caso de qualquer conflito entre o DPSA e este Módulo, este Módulo se aplicará conforme a inconsistência.

## 2\. PROCESSAMENTO

Processaremos os seguintes dados em conexão com o Recurso:

| **Informações Pessoais**                                     | **Uso**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Dados de configuração do sistema:** nome de domínio, registros de configuração DNS (registro de host, tipo de registro, valor de registro, tipo de aceleração, TTL), configuração do local de origem (endereço do local de origem, porta), registro de configuração do CDN (como regra de acesso, regra de cache, senha de autenticação MD5, chave, configuração CDN de pequenos recursos), certificado e chave SSL, configuração de segurança (ID da política de proteção, regras de proteção personalizadas, como regras de pacote TCP e regras de pacote HTTP) | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você conforme sua configuração específica. Observe que o certificado e a chave SSL estão integrados ao nosso recurso SSL Certificate Service para fornecer serviços de segurança como parte do Recurso, e os registros de nome de domínio e configuração de DNS estão integrados ao nosso recurso DNSPod para fornecer serviços DNS como parte do Recurso. Observe que esses dados também são armazenados em nosso recurso Cloud Object Storage (COS) e armazenados com backup em nosso recurso TencentDB para MySQL. |
| **Dados de cache do CDN:** resposta HTTP do servidor de origem do usuário final (cópia em cache) | Apenas processamos esses dados com a finalidade de fornecer o Recurso para você. Observe que esses dados são armazenados em nosso recurso de rede de entrega de conteúdo (Content Delivery Network, CDN). |

## 3\. REGIÃO DO SERVIÇO

Conforme especificado no DPSA.

## 4\. SUBPROCESSADORES

Conforme especificado no DPSA.

## 5\. RETENÇÃO DE DADOS

Armazenaremos dados pessoais processados em conexão com o Recurso da seguinte forma:

| **Informações Pessoais**  | **Política de Retenção**                                         |
| ------------------------- | ------------------------------------------------------------ |
| Dados de configuração do sistema | Retemos esses dados enquanto você usar o Recurso. Quando o uso do Recurso for encerrado, excluiremos esses dados após 30 dias. |
| Dados de cache CDN            | Retemos esses dados enquanto você usar o Recurso. Quando o uso do Recurso for encerrado, excluiremos esses dados após 30 dias. |

Você pode solicitar a exclusão desses dados pessoais de acordo com o DPSA.

## 6\. CONDIÇÕES ESPECIAIS

Você deve garantir que este Recurso seja usado somente por usuários finais com a idade mínima exigida para que possam consentir com o processamento de seus dados pessoais. Pode haver diferenças dependendo da jurisdição em que o usuário final está localizado.