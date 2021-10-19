## Visão geral da funcionalidade

O Quick UDP Internet Connections (QUIC) é um protocolo de rede comum, que garante a segurança da rede e reduz a latência na transferência e nas conexões, a fim de evitar o congestionamento da rede. É possível ativar o protocolo QUIC para os clientes acessarem os nós do CDN com segurança de transferência de dados aprimorada e eficiência de acesso.

Atualmente, essas versões do QUIC são compatíveis por padrão: draft h3-28, h3-Q050, h3-Q046, h3-Q043, Q046 e Q043.

O QUIC beta do CDN do Tencent Cloud foi lançado. Você pode [enviar uma solicitação](https://intl.cloud.tencent.com/apply/p/g0lwu71z0i7) e nós a analisaremos em 15 dias úteis.



## Guia beta

Se a sua solicitação for aprovada, você pode acessar o console do CDN e ativar o QUIC para seus nomes de domínio novos para teste.
>!
>- Depois que a sua solicitação for aprovada, o QUIC só poderá ser ativado para nomes de domínio novos, mas não para os existentes.
>- Atualmente, o QUIC está em versão beta no console do CDN, portanto, recomendamos ativar o QUIC apenas para seus nomes de domínio de teste, em vez de nomes de domínio empresariais.
>- A troca de tipos de serviço pode afetar o agendamento de recursos entre plataformas. Recomendamos não trocar os tipos de serviço para os nomes de domínio depois de ativar o QUIC.
>- Atualmente, o pull de origem do QUIC não é compatível.


Faça login no [console do CDN](https://console.cloud.tencent.com/cdn) e marque a caixa para ativar o QUIC ao conectar um nome de domínio novo:
![](https://main.qcloudimg.com/raw/2098308cd8a8c1a0321c0164646b7700.png)
**Limitações de configuração:**

- Atualmente, o QUIC não pode ser ativado para nenhum nome de domínio do tipo de serviço de aceleração de streaming de VOD.
- O QUIC não pode ser ativado para nenhum nome de domínio com o IPv6 ativado.


Depois de conectar o nome de domínio, clique em **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, acessar a página de detalhes do nome de domínio e abrir a guia **HTTPS Configuration (Configuração do HTTPS)** para localizar a seção de configuração do QUIC. Ele fica desativado por padrão e você pode ativá-lo diretamente.
**Observação:** primeiro, configure um certificado HTTPS para ativá-lo.
![](https://main.qcloudimg.com/raw/e697e32b39948d56610285c80043f1de.png)



## Faturamento

Atualmente, o QUIC está em versão beta no console do CDN. É um serviço de valor agregado e atualmente é gratuito.

