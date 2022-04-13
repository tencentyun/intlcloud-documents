Anúncio:

O CDN do Tencent Cloud lançará oficialmente o suporte ao QUIC em 5 de janeiro de 2022.
O suporte ao QUIC é cobrado com base no número de solicitações QUIC. Para obter mais informações, consulte a [Visão geral do faturamento](https://intl.cloud.tencent.com/zh/document/product/228/2949).
Iremos notificá-lo com antecedência sobre o faturamento da sua assinatura. Preste atenção em nossos anúncios no console e na documentação.

## Visão geral da funcionalidade

O Quick UDP Internet Connections (QUIC) é um protocolo de rede comum, que garante a segurança da rede e reduz a latência na transferência e nas conexões para evitar o congestionamento da rede. É possível ativar o protocolo QUIC para clientes acessarem os nós CDN com segurança aprimorada em transferência de dados e eficiência de acesso.

Atualmente, as versões QUIC suportadas incluem draft h3-28, h3-Q050, h3-Q046, h3-Q043, Q046 e Q043.

## Instruções

1. Ativar o QUIC:

Depois de adicionar um nome de domínio, clique em **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, na página de detalhes de nome de domínio e selecione a guia **HTTPS Configuration (Configuração do HTTPS)**  -> **QUIC configuration (Configuração do QUIC)**. O QUIC fica desativado por padrão e você pode ativá-lo manualmente.
**Observação:** Um certificado HTTPS é necessário para habilitar o QUIC.
![img](https://tva1.sinaimg.cn/large/008i3skNgy1gy2n1viwjjj30pf034t8t.jpg)

> Observação:
>
>- A troca de tipos de serviço pode afetar o agendamento de recursos entre plataformas. Recomendamos não trocar os tipos de serviço para os nomes de domínio depois de ativar o QUIC.
>- Solicitações QUIC não podem ser encaminhadas para a origem.
> - O QUIC é apenas parcialmente suportado no momento.

**Limites de uso:**

- No momento, o QUIC não está disponível para aceleração de streaming de vídeo sob demanda.
- O QUIC não pode ser ativado para nenhum nome de domínio com o IPv6 ativado.

2. Desativar o QUIC:

Você pode acessar ** Domain Management (Gerenciamento de domínio)** > ** HTTPS Configuration (Configuração HTTPS)** > **QUIC** e desativar o QUIC.

## Faturamento

O suporte QUIC é um serviço de valor agregado, que é cobrado com base no número de solicitações QUIC e permite o pagamento conforme o uso. Para obter mais informações, consulte a [Visão geral do faturamento](https://intl.cloud.tencent.com/zh/document/product/228/2949).
