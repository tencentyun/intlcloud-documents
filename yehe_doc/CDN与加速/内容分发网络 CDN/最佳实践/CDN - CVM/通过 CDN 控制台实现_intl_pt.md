
<style> 
table th:nth-of-type(1) { width:16%; } 
table th:nth-of-type(2){ width:84%; } 
</style>

Este documento descreve como acelerar o acesso a instâncias do CVM por meio do console do CDN.

## Pré-requisitos

1. Você criou uma conta na Tencent Cloud e verificou sua identidade.
2. Você ativou o serviço do CVM. Para obter mais informações, consulte [Introdução ao CVM](https://intl.cloud.tencent.com/document/product/213/10517).

## Instruções

### Criação de uma distribuição

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), clique em **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, para acessar a página de gerenciamento do nome de domínio, e clique em **Create Distribution (Criar distribuição)**.

### Parte 1: Configurações de nomes de domínio

Insira o nome de domínio do serviço no campo de domínio e selecione o projeto, a região e o tipo de serviço:


**Descrição da configuração:**

| Configuração | Descrição                                                     |
| -------- | ------------------------------------------------------------ |
| Nome de domínio          | 1. O nome de domínio pode conter até 81 caracteres.<br/>2. O registro de ICP é necessário para nomes de domínio em execução na China continental.<br/>3. Subdomínios (a.test.com ou a.b.test.com) e nomes de domínio curinga (\*.test.com ou \*.a.test.com) são compatíveis.<br/>4. É preciso [verificar a propriedade do nome de domínio](https://intl.cloud.tencent.com/document/product/228/5734) ao conectar um nome de domínio curinga ou um nome de domínio conectado.<br/><br/><strong>Observações:</strong><br/>1. Se um nome de domínio curinga for conectado aqui, seus nomes de subdomínio e nomes de domínio curinga de segundo nível não podem ser conectados por outras contas.<br/>2. Nomes de domínio nos formatos `*.test.com` e `*.a.test.com` não podem ser configurados ao mesmo tempo.<br/>3. Os nomes de domínio contendo sublinhados e caracteres chineses convertidos em punycode estão agora disponíveis.<br/>　4. Nomes de domínio maliciosos ou de alto risco não podem ser conectados. Para obter mais informações, consulte os [Limites de uso](https://intl.cloud.tencent.com/document/product/228/32981). |
| Projeto | Projeto é um conjunto de recursos compartilhados por todos os produtos da Tencent Cloud. É possível gerenciá-lo na página [Gerenciamento de projetos](https://console.cloud.tencent.com/project). |
| Região | **China continental**: as solicitações de acesso de usuários globais serão programadas para os nós de cache na China continental. <br/>** Fora da China continental**: as solicitações de acesso de usuários globais serão programadas para os nós de cache fora da China continental. <br/>**Global**: as solicitações de acesso serão programadas para o nó ideal mais próximo, independentemente de estar dentro ou fora da China continental. <br/><br/><strong>**Observações:** </strong><br/>Os serviços de aceleração dentro e fora da China continental são faturados separadamente. Para obter mais informações sobre as políticas de faturamento, consulte [Visão geral do faturamento](https://intl.cloud.tencent.com/document/product/228/2949). |
| Tipo de serviço | O CDN otimiza o desempenho de aceleração com base no tipo de serviço. <br/>Para obter o melhor resultado de aceleração, recomendamos escolher o tipo de serviço semelhante ao da sua empresa real. <br/><br/>Aceleração estática: adequada para cenários de aceleração de recursos em pequena escala, como comércio eletrônico, sites e imagens de jogos.<br/>Aceleração de download: adequada para cenários de download, como instalação de jogos, download de arquivos de origem de áudio/vídeo e distribuição de firmware para celulares. <br/>Aceleração de streaming de VOD: adequada para cenários como educação online e VOD. |
| Protocolo de Internet | IPv4: os nós só podem ser acessados ​​por meio de endereços IPv4. <br/>IPv4+IPv6: os nós podem ser acessados ​​por meio de endereços IPv4 e IPv6. Somente quando esta opção é selecionada pode ser configurado um servidor de origem IPv6. <br/><br/><strong>Observação: </strong><br/>O Ipv6 é suportado apenas na China continental. |

### Parte 2: Configurações de servidor de origem

Configure a origem. Quando o recurso solicitado não estiver armazenado em cache nos nós CDN, o CDN encaminhará a solicitação para a origem, extrairá o recurso solicitado e o armazenará em cache nos nós CDN.


**Descrição da configuração:**

| Configuração | Descrição                                                     |
| -------- | ------------------------------------------------------------ |
| Tipo de servidor origem | Origem do cliente: selecione essa opção se você já tiver seu próprio servidor corporativo (ou seja, servidor de origem). <br/><a href = "https://intl.cloud.tencent.com/product/cos">COS da Tencent Cloud</a>: se os recursos forem armazenados no COS, o bucket pode ser selecionado diretamente como o servidor de origem. |
| Endereço do servidor de origem | Origem do cliente: <br/>1 Vários IPs podem ser configurados como o servidor de origem, que será sondado durante o pull de origem. <br/>2 Se vários IPs forem usados, você pode configurar o pull de origem ponderado no formato de `IP:port:weight(1 - 100)`. A porta pode ser omitida e o formato torna-se `IP::weight`. <br/>3 É possível configurar um nome de domínio como o servidor de origem, que deve ser diferente do nome de domínio de aceleração corporativo. <br/><br/>COS da Tencent Cloud: <br/>1 Selecione na lista suspensa o bucket a ser configurado como servidor de origem. <br/>2 Se o bucket for de leitura/gravação privada, primeiro conceda acesso CDN ao bucket. Caso contrário, o pull de origem falhará. |
| Protocolo de pull de origem | Essa opção pode ser selecionada com base nos protocolos compatíveis com servidor de origem: <br/>HTTP: as solicitações de acesso HTTP/HTTPS usam pull de origem HTTP. <br/>HTTPS: as solicitações de acesso HTTP/HTTPS usam pull de origem HTTPS (o servidor de origem deve ser compatível com o acesso HTTPS). <br/>Seguir o protocolo: as solicitações de acesso HTTP usam pull de origem HTTP, já as solicitações de acesso HTTPS usam pull de origem HTTPS (o servidor de origem deve ser compatível com o acesso HTTPS). |
| Domínio de origem | Refere-se ao nome de domínio acessado no servidor de origem por um nó do CDN durante o pull de origem. <br/>Se um nome de subdomínio for conectado, será igual ao nome de domínio de aceleração por padrão e poderá ser personalizado. <br/>Se um nome de domínio curinga for conectado, será o nome do subdomínio de acesso real por padrão e poderá ser personalizado. |

### Parte 3: Configuração de serviço

Configure o serviço de aceleração de nó:


**Descrição da configuração:**

| Configuração | Descrição                                                     |
| -------- | ------------------------------------------------------------ |
| Ignorar parâmetro | Um nó armazena recursos em cache seguindo o mapeamento `Key-Value`, em que ` Key` é o URL do recurso.<br/> Se "Ignore Query String (Ignorar string de consulta)" estiver habilitado, os parâmetros após "?" no URL serão ignorados.<br/> Caso contrário, `Key` será um URL de recurso completo.<br/>Esse recurso fica desabilitado para aceleração estática e habilitado para aceleração de VOD de mídia de download e streaming por padrão. Para obter mais informações, consulte [Configuração de regra de chave de cache](https://intl.cloud.tencent.com/document/product/228/35316). |
| Range GETs | Especifica se as solicitações parciais devem ser processadas durante o pull de origem. Pode ser habilitado apenas se o servidor de origem for compatível com Range GETs. Para obter mais informações, consulte [Configuração de Range GETs](https://intl.cloud.tencent.com/document/product/228/7184).<br/>Esse recurso é habilitado para origem de COS por padrão |
| Configuração de cache | Especifica a configuração de validade do cache do nó. O tempo de expiração do cache para todos os arquivos é de 30 dias por padrão.<br/>A validade configurada do cache é o tempo mais longo possível, a validade real do cache está relacionada aos recursos nos nós. Para obter mais informações, consulte [Configuração de validade de cache do nó (Herdada)](https://intl.cloud.tencent.com/document/product/228/35317) |

### Conclusão da configuração

Depois de inserir todos os itens de configuração na página **Create Distribution (Criar distribuição)**, clique em **Submit (Enviar)** para adicionar o nome de domínio e aguarde até que a configuração do nome de domínio seja entregue em toda a rede, o que costuma levar de 5 a 10 minutos.

### Configuração do CNAME

Depois de adicionar um nome de domínio, é possível visualizar o CNAME de aceleração atribuído pelo CDN na página **Domain Management (Gerenciamento de domínio)**. É necessário adicionar um registro CNAME para o nome de domínio por meio de seu provedor de serviços de DNS (como DNSPod). Os serviços de aceleração estarão disponíveis depois que **a configuração do DNS entrar em vigor**. Para obter mais informações, consulte [Configuração CNAME](https://intl.cloud.tencent.com/document/product/228/3121).

> ! De acordo com os regulamentos, se o servidor de origem estiver em um nome de domínio acelerado do CVM da Tencent Cloud, o nome de domínio configurado para o cabeçalho do host deve obter um registro de ICP por meio da Tencent Cloud. Para obter mais informações, consulte [Configuração de cabeçalho de host](https://intl.cloud.tencent.com/document/product/228/6289).
