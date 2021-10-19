Este documento descreve como acelerar o acesso a recursos no COS por meio do CDN.

## Pré-requisitos
1. Você criou uma conta no Tencent Cloud e verificou sua identidade.
2. Um bucket do COS foi criado. Para obter mais informações, consulte a [Criação de buckets](https://intl.cloud.tencent.com/document/product/436/13309).

## Guia de operação
### Adição de um nome de domínio
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), clique em **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, para acessar a página de gerenciamento do nome de domínio, e clique em **Create Distribution (Criar distribuição)**.<!
![](https://main.qcloudimg.com/raw/557bb679be9e43f75f3a9c399a11abde.png)

### Seleção do COS como servidor de origem
![](https://main.qcloudimg.com/raw/ec7ea324171295b8fd0321e226d0e0a3.png)
1. Insira o **domain name (nome de domínio)** a ser acelerado.
Nomes de domínio curinga são aceitos, como `*.test.com`. Até 10 nomes de domínio podem ser conectados em lotes em uma única operação.
O nome de domínio deve atender às seguintes condições:
 - A declaração ICP para serviços na China Continental foi obtida junto ao MIIT para o nome de domínio
 - O nome de domínio nunca foi conectado ao CDN do Tencent Cloud
2. Selecione o **project (projeto)** do nome de domínio.
O projeto é compartilhado por todos os produtos do Tencent Cloud. Você pode adicionar um projeto em [Gerenciamento de projetos](https://console.cloud.tencent.com/project).
3. Selecione **COS** na lista suspensa **Origin Type (Tipo de origem)** em **Domain Configuration (Configuração de domínio)**.
4. Selecione o nome de domínio do **bucket** correspondente.
5. Habilite o **Private Bucket Access (Acesso ao bucket privado)**. Você deve autorizar o serviço do CDN primeiro. Depois que a autorização do serviço for confirmada, será possível habilitar manualmente essa funcionalidade.

>
>- O COS V5 é totalmente implementado para conectar um nome de domínio com o COS como servidor de origem ao CDN. Se você deseja usar um bucket do COS V4 como um servidor de origem, é necessário acessar o console do COS V4 e habilitar o serviço de aceleração para o bucket correspondente.
>- Se o seu bucket do COS V5 for privado, é necessário primeiro permitir que o serviço do CDN acesse o bucket do COS correspondente e, em seguida, habilitar o acesso de pull de origem. Os recursos em todos os buckets privados serão então entregues pela rede pública do CDN, o que envolve riscos de segurança relativamente altos.

### Configuração do serviço de aceleração
Com base nas suas necessidades empresariais, selecione **Business Type (Tipo de negócio)** e defina **Basic Configuration (Configuração básica)** e **Cache Expiration Configuration (Configuração de expiração do cache)**.
![](https://main.qcloudimg.com/raw/6264633c18801547e4aece61a94009cb.png)
1. **Business Type (Tipo de negócio)**
   O tipo de negócio determina a plataforma de recursos a ser programada pelo nome de domínio. A configuração de aceleração varia de acordo com a plataforma de recursos. Selecione um tipo de negócio com base nas condições da sua empresa:
   - Aceleração estática: adequada para cenários de aceleração de recursos estáticos, como comércio eletrônico, sites e imagens de jogos.
   - Aceleração de download: adequada para cenários como instalações de jogos, downloads de áudio/vídeo e distribuição de pacote de firmware de celular.
   - Aceleração de streaming de VOD: adequada para cenários de aceleração de VOD.

2. **Basic Configuration (Configuração básica)**
O CDN fornece a opção Ignore Query String (Ignorar string de consulta), que permite controlar a filtragem de parâmetros após **"?"** em URLs de solicitação de usuários finais. É possível usar essa funcionalidade para controle de versão flexível ou autenticação baseada em token. Para obter mais informações, consulte [Configuração de Ignorar string de consulta](https://intl.cloud.tencent.com/doc/product/228/6291).

3. **Cache Expiration Configuration (Configuração de expiração do cache)**
A configuração de expiração do cache refere-se ao conjunto de regras de expiração que os nós de cache do CDN devem cumprir ao armazenar em cache seu conteúdo empresarial. Para obter mais informações, consulte [Configuração de expiração do cache](https://intl.cloud.tencent.com/doc/product/228/6290).


### Conclusão da conexão
Depois de inserir todos os itens de configuração na página **Create Distribution (Criar distribuição)**, clique em **Submit (Enviar)** para adicionar o nome de domínio e aguarde até que a configuração do nome de domínio seja entregue em toda a rede, o que costuma levar de 5 a 10 minutos.

### Configuração do CNAME
Depois de adicionar um nome de domínio, é possível exibir o CNAME de aceleração atribuído pelo CDN na página **Domain Management (Gerenciamento de domínio)**. É necessário adicionar um registro CNAME para o nome de domínio por meio de seu provedor de serviços de DNS (como DNSPod). Os serviços de aceleração estarão disponíveis depois que **a configuração do DNS entrar em vigor**. Para obter mais informações, consulte [Configuração do CNAME](https://intl.cloud.tencent.com/doc/product/228/3121).
