

CDN e [DNSPod](https://console.dnspod.cn/) do Tencent Cloud. Se um nome de domínio foi hospedado no DNSPod do Tencent Cloud, você pode configurar o CNAME com algumas etapas por meio do [console do CDN](https://console.cloud.tencent.com/cdn/domains). Assim, você pode reduzir etapas, economizar tempo e habilitar o serviço de aceleração do CDN rapidamente.

>! Está disponível apenas no site chinês, mas não no site internacional.

## Informações gerais

Após um nome de domínio ser conectado ao CDN, o sistema atribuirá automaticamente um nome de domínio do CNAME com o sufixo `.cdn.dnsv1.com`, que pode ser visualizado na página [Gerenciamento de domínio](https://console.cloud.tencent.com/cdn/domains) no console do CDN. Não pode ser acessado diretamente. Em vez disso, primeiro você precisa concluir a configuração do CNAME com o provedor de serviços de nome de domínio. Quando o registro CNAME entrar em vigor, você pode ativar o serviço de aceleração do CDN.

## Cenários

Os usuários do DNSPod e CDN do Tencent Cloud podem configurar o registro CNAME para habilitar o serviço de aceleração do CDN.

## Guia de operação

### Hospedando nomes de domínio no DNSPod

Você precisa hospedar a resolução de nome de domínio no DNSPod primeiro. Para obter mais informações, consulte [Resolução de hospedagem de nome de domínio no DNSPod](https://docs.dnspod.cn/dns/60b99ba0e90008112f815bde/).

### Uso do serviço CDN

#### Adição de um nome de domínio

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), clique em **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Create a Distribution (Criar uma distribuição)** para adicionar o nome de domínio que deseja acelerar. Para obter mais informações, consulte [Adicionar nomes de domínio](https://intl.cloud.tencent.com/document/product/228/5734).

#### Configuração do CNAME

Faça login no [console do CDN] e vá para a página [Gerenciamento de domínio](https://console.cloud.tencent.com/cdn/domains). Encontre o nome de domínio que você deseja acelerar e passe o mouse sobre o ícone na frente do CNAME para visualizar a nota. Clique em **Quick Configure (Configuração rápida)** para configurar o CNAME.



Para ativar o serviço de aceleração para o nome de domínio selecionado, tomaremos as seguintes ações para processar o registro de resolução do nome de domínio no DNSPod.

1. Se o nome de domínio não tiver configurado nenhum registro de resolução, adicione um registro CNAME CDN do Tencent Cloud com o tipo de linha padrão. O TTL padrão é 600.
2. Se o nome de domínio tiver configurado um registro de resolução, pause todos os registros de resolução configurados e adicione um registro CNAME CDN do Tencent Cloud com o tipo de linha padrão. O TTL padrão é 600.
**Observação: pausar todos os registros de resolução configurados para um nome de domínio pode afetar o serviço de resolução DNS existente para o nome de domínio.**


1. Em seguida, você pode fazer login no [Console do DNSPod](https://console.dnspod.cn/dns/list) para gerenciar registros de resolução.


>! Certifique-se de que a conta atual tenha permissões de gerenciamento para o nome de domínio correspondente.
> Se for uma subconta ou conta de colaborador, entre em contato com a conta mestra para obter autorização. Por exemplo, você deve obter a permissão de gravação e a permissão QcloudDNSPodFullAccess correspondente ao nome de domínio de aceleração do CDN.

### Concluindo as configurações de CNAME

Após enviar a resolução para configuração rápida, ela levará cerca de 1 minuto para entrar em vigor. Você pode atualizar a página [Gerenciamento de nomes de domínio](https://console.cloud.tencent.com/cdn/domains) no console do CDN. Quando o status do CNAME muda para ativado, você pode passar o mouse sobre o ícone na frente do CNAME para visualizar uma nota, ou seja, o serviço de aceleração está operando normalmente.

>? Se você não quiser usar esse recurso, poderá configurar o CNAME por conta própria. Para obter mais informações, consulte [Configuração do CNAME](https://intl.cloud.tencent.com/document/product/228/3121)

## Outros
Se você excluir o nome de domínio de aceleração correspondente, não operaremos seus registros de resolução no DNSPod. Modifique os registros de resolução conforme necessário.

