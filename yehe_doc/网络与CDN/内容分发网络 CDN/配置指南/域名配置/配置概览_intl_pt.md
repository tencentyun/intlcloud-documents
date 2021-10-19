## Visão geral das configurações

O CDN aceita várias configurações personalizadas e você pode ajustá-las com base nas necessidades da sua empresa.

### Configurações básicas

As configurações básicas são os conteúdos necessários para a aceleração do CDN, incluindo as configurações do servidor de origem e as informações básicas do serviço de aceleração, como região de aceleração e tipo de serviço, etc.

| Configuração                                                     | Descrição                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Informações básicas](https://intl.cloud.tencent.com/document/product/228/7864) | Modifica informações básicas, como projeto, região de aceleração, tipo de serviço, etc.         |
| [Configuração do servidor de origem](https://intl.cloud.tencent.com/document/product/228/6289) | Configura pull de origem de round robin de vários IPs, pull de origem baseado em nomes de domínio, pull de origem ponderado de round robin, domínios de origem e protocolos de pull de origem.<br/>Aceita a configuração de servidores de origem de backup dinâmico.<br/>**Para nomes de domínio de aceleração global, a aceleração dentro e fora da China Continental pode ser configurada separadamente.** |

### Controle de acesso

É possível configurar várias regras com base nas solicitações do usuário para permitir ou bloquear solicitações de acesso.

| Configuração                                                     | Descrição                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Proteção de hotlink](https://intl.cloud.tencent.com/document/product/228/6292) | Aceita a configuração de listas de permissões/bloqueio de referenciais, para determinar se deve permitir ou negar solicitações de acesso HTTP com base nos cabeçalhos de referencial de solicitação.<br/>**Para nomes de domínio de aceleração global, a aceleração dentro e fora da China Continental pode ser configurada separadamente.** |
| [Lista de bloqueio/permissões de IP](https://intl.cloud.tencent.com/document/product/228/6298) | Aceita a configuração de listas de permissões/bloqueio de IPs, para determinar se deve permitir ou negar solicitações de acesso HTTP com base nos IPs de solicitação de cliente.<br/>**Para nomes de domínio de aceleração global, a aceleração dentro e fora da China Continental pode ser configurada separadamente.** |
| [Limite de acesso de IP](https://intl.cloud.tencent.com/document/product/228/6420) | Limita a frequência com que um IP pode acessar um único nó, para negar as solicitações de acesso de IPs do cliente que excederem o limite.  |
| [Autenticação](https://intl.cloud.tencent.com/document/product/228/35237) | Aceita vários algoritmos de assinatura de carimbo de data/hora e regras para configuração anti-hotlinking.<br/>**Para nomes de domínio de aceleração global, a aceleração dentro e fora da China Continental pode ser configurada separadamente.** |
| [Arraste de vídeo](https://intl.cloud.tencent.com/document/product/228/8111) | Ela foi projetada para a aceleração de streaming de VOD.<br/>Com a funcionalidade de arrasto de vídeo habilitada, é possível especificar o ponto inicial de um vídeo por meio do parâmetro `start`.|
| [Lista de bloqueio/permissões de agente do usuário (UA)](https://intl.cloud.tencent.com/document/product/228/37256)  | Determina se nega ou permite solicitações de acordo com o cabeçalho de solicitação HTTP `User-Agent`.  |
| [Limite de velocidade downstream](https://intl.cloud.tencent.com/document/product/228/37257) | Controla a largura de banda de acesso ao CDN definindo o limite de velocidade downstream em um URL.   |

### Configuração de cache

A configuração do cache controla o cache em nós do CDN.

| Configuração                                                     | Descrição                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Ignorar string de consulta](https://intl.cloud.tencent.com/document/product/228/35316) | Para o cache de recursos, ele aceita a configuração de ignorar parâmetros após "?" em um URL de acesso.<br/>**Recomendamos desativar essa funcionalidade se os parâmetros após "?" indicarem conteúdos diferentes da sua empresa.** |
| [Validade do cache de nó](https://intl.cloud.tencent.com/document/product/228/35317) | Aceita a configuração da validade do cache de arquivos em nós com base no caminho e tipo de arquivo.    |
| [Cache do código de status](https://intl.cloud.tencent.com/document/product/228/35318) | Aceita a configuração da validade do cache do código de status para nós do CDN, para responder aos códigos de status 2XX diretamente, reduzindo assim a pressão no servidor de origem. |
| [Cache do cabeçalho HTTP](https://intl.cloud.tencent.com/document/product/228/35319) | Ela pode ser desabilitada conforme necessário. Os nós do CDN armazenam em cache todos os cabeçalhos de resposta do servidor de origem por padrão.        |
| [Não diferenciar maiúsculas de minúsculas no URL de cache](https://intl.cloud.tencent.com/document/product/228/35316) | O cache do nó do CDN não ignora a diferenciação de maiúsculas de minúsculas por padrão. A diferenciação de maiúsculas de minúsculas pode ser ignorada conforme necessário. |
| [Regravação de URL de acesso](https://intl.cloud.tencent.com/document/product/228/38074)| Aceita a personalização da configuração de regravação de URL para redirecionar solicitações de URLs com código de status 302 para URLs de destino.|


### Configuração de pull de origem

A configuração de pull de origem controla o processo de encaminhamento de solicitações dos nós do CDN para os servidores de origem.

| Configuração                                                     | Descrição                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [GETs de alcance](https://intl.cloud.tencent.com/document/product/228/7184) | Os GETs de alcance são usados para pull de origem por padrão. Se não forem compatíveis com seu servidor de origem, você pode desabilitá-los. |
| [Cabeçalho de solicitação](https://intl.cloud.tencent.com/document/product/228/37037) | Adiciona cabeçalhos especificados durante o pull de origem, como o IP real do cliente.      |
| [Acompanhamento 301/302](https://intl.cloud.tencent.com/document/product/228/7183) | Ele pode ser habilitado para pull de origem conforme necessário.                                  |
| [Tempo limite de pull de origem](https://intl.cloud.tencent.com/document/product/228/35227) | Configura o período limite da conexão TCP (que é padronizado em 5 segundos) e o período de carregamento (que é padronizado em 10 segundos) de pull de origem. |

### Configuração de aceleração HTTPS

A aceleração HTTPS aceita várias configurações relacionadas a HTTPS.

| Configuração                                                     | Descrição                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Configuração do HTTPS](https://intl.cloud.tencent.com/document/product/228/35213) | Aceita o upload de um certificado próprio ou de um certificado hospedado para habilitar a aceleração HTTPS.  |
| [Configuração do HTTP2.0](https://intl.cloud.tencent.com/document/product/228/35215) | Com ela habilitada, os servidores de borda do CDN podem aceitar o HTTP2.0.<br/>**Primeiro configure um certificado para habilitar o HTTP2.0.** |
| [Configuração de redirecionamento forçado](https://intl.cloud.tencent.com/document/product/228/35214) | O redirecionamento forçado de HTTPS para acesso HTTP pode ser obtido com ou sem um certificado.<br/>O redirecionamento forçado de HTTP para acesso HTTPS requer um certificado. |
| [Grampeamento OCSP](https://intl.cloud.tencent.com/document/product/228/35216) | Com a configuração habilitada, o grampeamento OCSP é compatível.<br/>**Primeiro configure um certificado para habilitar o grampeamento OCSP.** |
| [Configuração do HSTS](https://intl.cloud.tencent.com/document/product/228/37036) | Se estiver habilitada, o cabeçalho `strict-transport-security` será adicionado.<br/>**Primeiro configure um certificado para habilitar a configuração do HSTS.** |

### Configuração avançada

| Configuração                                                     | Descrição                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Configuração do limite de largura de banda](https://intl.cloud.tencent.com/document/product/228/7541) | Aceita a configuração de limite de largura de banda para a aceleração dentro e fora da China Continental. O serviço de aceleração pode ser interrompido conforme necessário se o limite for excedido. <br/>**Para nomes de domínio de aceleração global, a aceleração dentro e fora da China Continental pode ser configurada separadamente.** |
| [Configuração do SEO](https://intl.cloud.tencent.com/document/product/228/35219) | Aceita o reconhecimento automático de se um IP de acesso pertence a um mecanismo de pesquisa.<br/>Em caso afirmativo, as solicitações do IP serão encaminhadas ao servidor de origem para garantir a estabilidade do peso do mecanismo. |
| [Configuração do cabeçalho de resposta](https://intl.cloud.tencent.com/document/product/228/35320) | Define cabeçalhos de resposta HTTP conforme necessário e os adiciona às solicitações de resposta aos clientes.  |
| [Configuração de compressão inteligente](https://intl.cloud.tencent.com/document/product/228/35220) | Realiza a compactação Gzip ou Brotli em arquivos especificados com base no tipo e intervalo de arquivo.                           |


