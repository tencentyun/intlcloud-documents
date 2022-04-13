## 1\. INTRODUÇÃO
Este Módulo é aplicável se você usa o TencentCloud EdgeOne (“Recurso”). Este Módulo está incorporado à política de privacidade localizada em [Política de Privacidade](https://intl.cloud.tencent.com/document/product/301/17345). Os termos usados, mas não definidos neste Módulo, devem ter o significado que lhes é atribuído na Política de Privacidade. Em caso de conflito entre a Política de Privacidade e este Módulo, este Módulo se aplicará conforme a inconsistência.
## 2\. CONTROLADORIA
O controlador das informações pessoais descritas neste Módulo é o especificado na Política de Privacidade.
## 3\. DISPONIBILIDADE
Esse recurso está disponível para os usuários em todo o mundo.
## 4\. COMO USAMOS AS INFORMAÇÕES PESSOAIS
Usaremos as informações nos seguintes modos e de acordo com as seguintes bases jurídicas:

| **Informações Pessoais**                                     | **Uso**                                                      | **Base Jurídica**                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Dados de registro de acesso ao nó de borda:** O registro de data e hora de acesso, o endereço IP do cliente, o endereço IP público do servidor de nó, o host, a porta, a URL, os cabeçalhos HTTP acessados (solicitações HTTP do usuário final, como usuário-agente, árbitro, cookie), corpo de dados POST (o primeiro 10 kB), em caso de ataques maliciosos, e regras de segurança ativadas | Usamos essas informações com a finalidade de fornecer o Recurso para você, incluindo:<li>consultas de usuários sobre o tráfego de negócios e o status de acesso superior de diferentes dimensões (como URL, UA);<li>analisar riscos de tráfego e identificar características maliciosas; e<li>solução de problemas.<br/>Observe que esses dados estão integrados ao nosso recurso ClickHouse para fins de armazenamento e pré-agregação, e também são armazenados em nossos recursos Cloud Virtual Machine (CVM), Cloud Object Storage (COS) e ClickHouse. | Processamos essas informações porque são necessárias para a execução de nosso contrato com você para o fornecimento do Recurso. |
| **Dados de tráfego:** Acesse os dados de tráfego de cada host em um único IP de servidor (tráfego de entrada, tráfego de saída, número de solicitações) | Utilizamos essas informações com o objetivo de calcular o número de visitas de usuários, para fins de faturamento. <br/>Observe que esses dados são integrados ao nosso recurso ClickHouse para fins de armazenamento e pré-agregação e também são armazenados e copiados em nosso recurso TencentDB para MySQL. | Processamos essas informações porque são necessárias para a execução de nosso contrato com você para o fornecimento do Recurso. |
| **Dados de configuração do sistema:** Dados de configuração de nó (IP, ISP, endereço), dados de configuração de cluster de servidor, dados de configuração de API, endereços DB e chaves | Usamos essas informações com o propósito de fornecer o Recurso para você, incluindo garantir o bom funcionamento da rede de entrega de conteúdo (CDN). <br/>Note que esses dados estão armazenados com backup em nosso recurso TencentDB for MySQL. | Processamos essas informações porque são necessárias para a execução de nosso contrato com você para o fornecimento do Recurso. |
| **Dados de registro de acesso da API:** O registro de data e hora de acesso, o endereço IP do cliente, o endereço IP intranet do servidor API, a URL, o órgão de solicitação (incluindo os dados de configuração), o corpo de resposta (incluindo os dados de configuração) | Usamos essas informações para fins de solução de problemas. <br/>Observe que esses dados estão integrados ao nosso recurso de auditoria na nuvem para fornecer autenticação e registros de auditoria CAM, e são armazenados em nosso recurso Cloud Log Service. | Processamos essas informações porque são necessárias para a execução de nosso contrato com você para o fornecimento do Recurso. |

## 5\. COMO ARMAZENAMOS E COMPARTILHAMOS INFORMAÇÕES PESSOAIS
Como especificado na Política de Privacidade. 
Além disso, a APPID e UIN são armazenadas em nosso recurso TencentDB para MySQL.
## 6\. RETENÇÃO DE DADOS
Reteremos informações pessoais de acordo com o seguinte:

| **Informações Pessoais**          | **Política de Retenção** |
| -------------------------           | -------------------- |
| Dados de registro de acesso ao nó de borda        | Armazenados por 30 dias.  |
| Dados de tráfego        | Armazenados por 30 dias, após os quais esses dados são anonimizados. |
| Dados de configuração do sistema            | Retemos esses dados enquanto você usar o Recurso. Quando o uso do Recurso for encerrado, excluiremos esses dados após 30 dias. |
| Dados de registro de acesso da API         | Armazenados por 180 dias. |