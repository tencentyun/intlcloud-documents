Este documento descreve como acelerar o acesso a recursos no COS por meio do CDN no console do COS.

## Pré-requisitos
1. Você criou uma conta na Tencent Cloud e verificou sua identidade.
2. Você ativou o serviço do CDN. Para obter mais informações, consulte [Configuração do CDN do zero](https://intl.cloud.tencent.com/document/product/228/32978).

## Instruções
### Criação de um bucket
Para obter mais informações sobre como criar um bucket, consulte [Criação de buckets](https://intl.cloud.tencent.com/document/product/436/13309).

### Configuração da aceleração
1. Depois de criar um bucket, entre diretamente na página de gerenciamento de configuração dele. Você também pode clicar em **Configuration Management (Gerenciamento de configuração)** na coluna "Operation (Operação)" do bucket na lista de buckets, para acessar a página de gerenciamento de configuração. Em seguida, selecione **Domain and Transfer (Domínio e transferência)**.
2. Habilite o **Default CDN Acceleration Domain (Domínio de aceleração CDN padrão)**.
Gerado pelo sistema, o **Default CDN Acceleration Domain (Domínio de aceleração CDN padrão)** é o nome de domínio que passa pelos nós de cache CDN. Você pode optar por ativá-lo ou desativá-lo.
(1) Clique em **Edit (Editar)** para ativar manualmente o **Default CDN Acceleration Domain (Domínio de aceleração CDN padrão)**.
![](https://main.qcloudimg.com/raw/260fde070f4b2f999c0d9d09bec13d55.png)
(2) Configure a aceleração CDN padrão:
![](https://main.qcloudimg.com/raw/2b72c25d2bf11f0c53a2e8286fcecf07.png)
**Origin Server Type (Tipo de servidor de origem)**: é configurado como **default origin server (servidor de origem padrão)**. Se você habilitou o site estático para o bucket do servidor de origem e deseja acelerar a entrega de conteúdo para o site estático, selecione **static website origin server (servidor de origem do site estático)**.
**Autenticação de pull de origem**: Para os buckets de leitura pública, a autenticação de pull de origem não precisa ser habilitada. Para os buckets de leitura privada, a autorização de serviço do CDN deve ser adicionada e a autenticação de pull de origem deve ser habilitada manualmente. Para obter mais informações, consulte [Habilitação de nomes de domínio de aceleração do CDN padrão](https://intl.cloud.tencent.com/document/product/436/31505).
**CDN Authorization (Autorização de CDN)**: clique em **Add CDN Service Authorization (Adicionar autorização de serviço do CDN)** para selecionar e conceder acesso ao CDN para os recursos do bucket.
![](https://main.qcloudimg.com/raw/41e745800445225d042ef82c6febcc19.png)
(3) Depois de concluir a configuração, clique em **Save (Salvar)** para ativar a aceleração do CDN.
![](https://main.qcloudimg.com/raw/5ffc31cb49410b4685316e75860c9385.png)

>!Para buckets de leitura privada, se a autenticação de pull de origem e a autorização de serviço do CDN estiverem habilitadas, a assinatura não será necessária para o acesso ao servidor de origem via CDN e os recursos em cache no CDN serão distribuídos na rede pública, o que afetará a segurança dos dados. Portanto, recomendamos que você habilite a autenticação CDN.
>
3. Habilite o **Custom CDN Acceleration Domain (Domínio de aceleração do CDN personalizado)**.
É possível vincular um nome de domínio personalizado que já possui registro de ICP ao bucket e ativar a aceleração do CDN.
>?Um máximo de 10 nomes de domínio personalizados podem ser adicionados no console do COS.
>
(1) Clique em **Add domain name (Adicionar nome de domínio)** no módulo **Custom CDN Acceleration Domain (Domínio de aceleração do CDN personalizado)**, para adicionar um nome de domínio personalizado registrado.
![](https://main.qcloudimg.com/raw/eda34cc24d82cebf109e3507a2ae142f.png)
(2) Adicionar o nome do domínio:
**Domínio**: insira o nome de domínio personalizado a ser vinculado (por exemplo, `www.example.com`). Certifique-se de que o nome de domínio tenha um registro de ICP e que um CNAME correspondente tenha sido configurado no provedor de serviços DNS. Para obter mais informações, consulte [Configuração CNAME](https://intl.cloud.tencent.com/document/product/228/3121).
**Autenticação de pull de origem**: para buckets de leitura privada, habilite manualmente a autenticação de pull de origem para proteger o servidor de origem.
Quando concluir a configuração, clique em **Save (Salvar)**.
![](https://main.qcloudimg.com/raw/e21189d91929209ded554581d267a505.png)
>!Para buckets de leitura privada, se a autenticação de pull de origem e a autorização de serviço do CDN estiverem habilitadas, a assinatura não será necessária para o acesso ao servidor de origem via CDN e os recursos em cache no CDN serão distribuídos na rede pública, o que afetará a segurança dos dados. Portanto, recomendamos que você habilite a autenticação CDN.
>
(3) Depois que a configuração for salva, o botão de alternância para a autenticação do CDN será exibido na coluna **CDN Authentication (Autenticação do CDN)**. Você pode habilitar manualmente a autenticação CDN para o nome de domínio personalizado.
**Autenticação do CDN:** a autenticação de carimbo de data/hora pode ser configurada para impedir o roubo por usuários mal-intencionados. Você pode habilitar o recurso depois de adicionar o nome de domínio.

Para obter mais informações sobre como configurar a aceleração de CDN no console COS, consulte [Visão geral do gerenciamento do nome de domínio](https://intl.cloud.tencent.com/document/product/436/18424).


## Configuração recomendada
1. Depois de concluir todas as configurações, vá para o [Console CDN](https://console.cloud.tencent.com/cdn) e pré-busque os arquivos de recursos estáticos no COS para os nós CDN com antecedência, o que reduzirá a tensão no servidor de origem e acelerará a resposta e o download. Para obter mais informações, consulte [Pré-busca de cache](https://intl.cloud.tencent.com/document/product/228/39000).
2. Configure cabeçalhos de acesso de origem cruzada. Para obter mais detalhes sobre permissões de recursos de origem cruzada, consulte [Cabeçalho de resposta HTTP](https://intl.cloud.tencent.com/document/product/228/35320).
3. Se o recurso foi modificado em seu servidor de origem, é recomendável limpar o cache antes de efetuar a pré-busca novamente. Para obter mais detalhes, consulte [Limpeza  do cache](https://intl.cloud.tencent.com/document/product/228/6299).
