<style> 
table th:nth-of-type(1) { width:18%; } 
table th:nth-of-type(2){ width:82%; } 
</style>

Este documento descreve como acelerar o acesso a recursos no COS por meio do CDN.

## Pré-requisitos

1. Você criou uma conta na Tencent Cloud e verificou sua identidade.
2. Um bucket do COS foi criado. Para obter mais informações, consulte [Criação de buckets](https://intl.cloud.tencent.com/document/product/436/13309).

## Instruções

### Criação de uma distribuição

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), clique em **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, para acessar a página de gerenciamento do nome de domínio, e clique em **Create Distribution (Criar distribuição)**.
### Seleção do COS como servidor de origem

#### Parte 1: Configuração de nome de domínio

Insira o nome de domínio da sua empresa no campo de domínio, selecione um projeto e tipo de aceleração, escolha se deseja habilitar o acesso IPv6 e defina uma tag:


**Descrição da configuração:**

| Configuração | Descrição                                                     |
| :------- | :----------------------------------------------------------- |
| Região | **China continental**: todas as solicitações são programadas para armazenar nós em cache na China continental. <br/>** Fora da China continental**: todas as solicitações são programadas para os nós de cache fora da China continental. <br/>**Global**: as solicitações são agendadas para o nó ideal mais próximo. <br/><br/>**Observações:** Os serviços de aceleração dentro e fora da China continental são faturados separadamente. Para obter mais informações, consulte a [Visão geral do faturamento](https://intl.cloud.tencent.com/document/product/228/2949). |
| Nome de domínio de aceleração          | 1. O nome de domínio pode conter até 81 caracteres.<br/>2. O registro de ICP é necessário para nomes de domínio em execução na China continental.<br/>3. Subdomínios (`a.test.com` ou `a.b.test.com`) e nomes de domínio curinga (`*.test.com` ou `*.a.test.com`) são compatíveis.<br/>4. É preciso [verificar a propriedade do nome de domínio](https://intl.cloud.tencent.com/document/product/228/5734) ao conectar um nome de domínio curinga ou um nome de domínio conectado.<br/><br/> **Observações:<br/>** 1. Se um nome de domínio curinga for conectado, os respectivos nomes de subdomínio e nomes de domínio curinga de segundo nível não podem ser conectados por outras contas.<br/> 2. Nomes de domínio nos formatos `*.test.com` e `*.a.test.com` não podem ser configurados ao mesmo tempo.<br/>3. Os nomes de domínio contendo sublinhados e caracteres chineses convertidos em punycode estão agora disponíveis.<br/>　4. Nomes de domínio maliciosos ou de alto risco não podem ser conectados. Para obter mais informações, consulte os [Limites de uso](https://intl.cloud.tencent.com/document/product/228/32981). |
| Projeto | (Opcional) Projeto é um conjunto de recursos compartilhados por todos os produtos da Tencent Cloud. É possível gerenciá-lo na página [Gerenciamento de projetos](https://console.cloud.tencent.com/project). |
| Tipo de aceleração | O CDN otimiza o desempenho de aceleração com base no tipo de serviço. Para um melhor efeito de aceleração, recomendamos selecionar o tipo de aceleração semelhante ao do seu negócio real.  <br/>Aceleração estática: aplicável a cenários de aceleração de recursos em pequena escala, como e-commerce, site e fotos de jogos. <br/>Aceleração de download: aplicável a cenários de download, como pacotes de instalação de jogos, downloads de arquivos de origem de áudio e vídeo e distribuição de firmware de celular. <br/>Aceleração de streaming de vídeo sob demanda: aplicável à educação online e streaming de vídeo sob demanda. |
| Acesso IPv6 | (Opcional) Os nós do CDN são compatíveis com o acesso IPv4 por padrão. O acesso IPv6 será compatível após a ativação.<br /><br/>**Observação:** O acesso IPv6 está disponível apenas na China continental. |
| Tag     | (Opcional) Uma tag é usada para gerenciar recursos por categoria de diferentes dimensões. Se as tags existentes não atenderem aos seus requisitos, vá para [Tag](https://console.cloud.tencent.com/tag/taglist). |

#### Parte 2: Configuração de origem

Configure a origem. Quando o recurso solicitado não estiver armazenado em cache nos nós CDN, o CDN encaminhará a solicitação para a origem, extrairá o recurso solicitado e o armazenará em cache nos nós CDN.


1. Selecione **COS** na lista suspensa **Origin Type (Tipo de origem)** em **Domain Configuration (Configuração de domínio)**.
2. Selecione um protocolo de pull de origem com base na compatibilidade do servidor de origem.
3. Selecione um **bucket** para o endereço de origem.
4. Habilite o **Private Bucket Access (Acesso ao bucket privado)**. Você deve acessar o **COS-bucket permission management (gerenciamento de permissão de bucket do COS)** para autorizar o serviço CDN primeiro. Depois que a autorização do serviço for confirmada, será possível habilitar manualmente essa funcionalidade.
5. A configuração padrão é usada para **Domínio de origem**. Nenhuma modificação é necessária.

#### Parte 3: Configuração de serviço

Configure o serviço de aceleração de nó:


**Descrição da configuração:**

| Configuração | Descrição                                                     |
| :------- | :----------------------------------------------------------- |
| Ignorar parâmetro | Um nó armazena recursos em cache seguindo o mapeamento `Key-Value`, em que ` Key` é o URL do recurso.<br/> Se "Ignore Query String (Ignorar string de consulta)” estiver habilitado, os parâmetros após "?" no URL serão ignorados antes do mapeamento. <br/>Caso contrário, `Key` será um URL de recurso completo. <br/>Por padrão, essa funcionalidade fica habilitada para a aceleração de download e de streaming de vídeo sob demanda, mas não para a aceleração estática. |
| Range GETs | Isso especifica se as solicitações parciais devem ser processadas durante o pull de origem. Ela pode ser habilitada apenas se o servidor de origem for compatível com Range GETs. Esse recurso é habilitado para o servidor de origem do COS por padrão. |
| Configuração de cache | Isso especifica o período de expiração do cache do nó, que é de 30 dias para todos os arquivos por padrão. O período de validade do cache é a validade mais longa possível. A validade real pode ser menor devido à capacidade de armazenamento disponível do nó.<br />Você pode definir a configuração do cache com base no tipo de origem. |

Depois de inserir todos os itens de configuração na página **Create Distribution (Criar distribuição)**, clique em **Submit (Enviar)** para adicionar o nome de domínio e aguarde até que a configuração do nome de domínio seja entregue em toda a rede, o que costuma levar de 5 a 10 minutos.

### Configuração do CNAME

Depois de adicionar um nome de domínio, é possível visualizar o CNAME de aceleração atribuído pelo CDN na página **Domain Management (Gerenciamento de domínio)**.


É necessário adicionar o registro CNAME para o nome de domínio em seu provedor de serviço de DNS (como DNSPod). Os serviços de aceleração ficarão disponíveis depois que **a configuração do DNS entrar em vigor**. Para obter mais detalhes, consulte [Configuração CNAME](https://intl.cloud.tencent.com/document/product/228/3121).

## Configuração recomendada

1. Depois de concluir todas as configurações, pré-busque os arquivos de recursos estáticos no COS para os nós CDN com antecedência, o que reduzirá a tensão no servidor de origem e acelerará a resposta e o download. Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/228/39000"> Pré-busca de cache</a>.
2. Configurar cabeçalhos de acesso de origem cruzada. Para obter mais detalhes sobre permissões de recursos de origem cruzada, consulte <a href="https://intl.cloud.tencent.com/document/product/228/35320">Cabeçalho de resposta de HTTP</a>.
3. Se o recurso foi modificado em seu servidor de origem, é recomendável limpar o cache antes de efetuar a pré-busca novamente. Para obter mais detalhes, consulte <a href="https://intl.cloud.tencent.com/document/product/228/6299">Limpeza  do cache</a>.
