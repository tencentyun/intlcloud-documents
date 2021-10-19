Este documento descreve como acelerar o acesso a recursos no COS por meio do CDN no console do COS.

## Pré-requisitos
1. Você criou uma conta no Tencent Cloud e verificou sua identidade.
2. Você ativou o serviço do CDN. Para obter mais informações, consulte [Introdução](https://intl.cloud.tencent.com/document/product/228/32978).

## Guia de operação

### Criação de um bucket
Para obter mais informações sobre como criar um bucket, consulte [Criação de buckets](https://intl.cloud.tencent.com/document/product/436/13309).

### Configuração da aceleração
1. Depois de criar um bucket, acesse sua página de gerenciamento de configuração diretamente. Você também pode clicar em **Configuration Management (Gerenciamento de configuração)** na coluna "Operation (Operação)" do bucket na lista de buckets, para acessar a página de gerenciamento de configuração.
2. Habilite o **default acceleration domain name (nome de domínio de aceleração padrão)**.
Gerado pelo sistema, ele é o nome de domínio que passa pelos nós de cache do CDN. Você pode optar por habilitá-lo ou desabilitá-lo.
(1) Clique em **Edit (Editar)** próximo ao **default acceleration domain name (nome de domínio de aceleração padrão)**, para habilitá-lo ou desabilitá-lo manualmente na página de configuração de aceleração padrão.
![](https://main.qcloudimg.com/raw/260fde070f4b2f999c0d9d09bec13d55.png)
(2) Configure a aceleração padrão:
![](https://main.qcloudimg.com/raw/2b72c25d2bf11f0c53a2e8286fcecf07.png)
**Tipo do servidor de origem**: o tipo padrão é **default origin server (servidor de origem padrão)**, mas se você habilitou o site estático para o bucket do servidor de origem e deseja acelerar a entrega de conteúdo para o site estático, selecione **static website origin server (servidor de origem do site estático)**.
**Autenticação de pull de origem**: para os buckets de leitura pública, a autenticação de pull de origem não precisa ser habilitada. Para os buckets de leitura privada, a autorização de serviço do CDN deve ser adicionada e a autenticação de pull de origem deve ser habilitada manualmente. Para obter mais informações, consulte [Ativação da autenticação de pull de origem](https://intl.cloud.tencent.com/document/product/436/31505).
**Autorização de serviço do CDN**: clique em **Add CDN service authorization (Adicionar autorização de serviço do CDN)** para selecionar e conceder acesso ao CDN para os recursos do bucket.
![](https://main.qcloudimg.com/raw/41e745800445225d042ef82c6febcc19.png)
(3) Depois de concluir a configuração, clique em **Save (Salvar)** para ativar a aceleração do CDN.
![](https://main.qcloudimg.com/raw/5ffc31cb49410b4685316e75860c9385.png)

> Para buckets de leitura privada, se a autenticação de pull de origem e a autorização de serviço do CDN estiverem habilitadas, a assinatura não será necessária para o acesso ao servidor de origem via CDN e os recursos em cache no CDN serão distribuídos na rede pública, o que afetará a segurança dos dados. Portanto, recomendamos que você habilite a autenticação do CDN.
>
3. Habilite o **custom acceleration domain name (nome de domínio de aceleração personalizado)**.
É possível vincular um nome de domínio personalizado arquivado ao bucket e ativar a aceleração do CDN.
> Um máximo de 10 nomes de domínio personalizados podem ser adicionados no console do COS
>
(1) Clique em **Add domain name (Adicionar nome de domínio)** no módulo **custom acceleration domain name (nome de domínio de aceleração personalizado)**, para adicionar um nome de domínio personalizado arquivado.
![](https://main.qcloudimg.com/raw/eda34cc24d82cebf109e3507a2ae142f.png)
(2) Configuração para adicionar nomes de domínio:
**Nome de domínio**: insira o nome de domínio personalizado a ser vinculado (como `www.example.com`). Certifique-se de que a declaração ICP para serviços na China Continental foi obtida do MIIT para o nome de domínio e um CNAME correspondente foi configurado para o nome de domínio com o provedor de serviços de DNS. Para obter mais informações, consulte [Configuração do CNAME](https://intl.cloud.tencent.com/document/product/228/3121).
**Autenticação de pull de origem**: para buckets de leitura privada, habilite manualmente a **autenticação de pull de origem** para proteger o servidor de origem.
Quando concluir a configuração, clique em **Save (Salvar)**.
![](https://main.qcloudimg.com/raw/e21189d91929209ded554581d267a505.png)
> Para buckets de leitura privada, se a autenticação de pull de origem e a autorização de serviço do CDN estiverem habilitadas, a assinatura não será necessária para o acesso ao servidor de origem via CDN e os recursos em cache no CDN serão distribuídos na rede pública, o que afetará a segurança dos dados. Portanto, recomendamos que você habilite a autenticação do CDN.
>
(3) Depois que a configuração for salva, o botão de alternância para a autenticação do CDN será exibido na coluna **CDN Authentication (Autenticação do CDN)**. É possível habilitar manualmente a autenticação do CDN para o nome de domínio personalizado.
**Autenticação do CDN:** a autenticação de carimbo de data/hora pode ser configurada para impedir o roubo por usuários mal-intencionados. É possível habilitar a funcionalidade depois de adicionar o nome de domínio.

Para obter mais informações sobre como configurar a aceleração do CDN no console do COS, consulte [Visão geral](https://intl.cloud.tencent.com/document/product/436/18424).
