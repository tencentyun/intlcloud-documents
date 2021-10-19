

## Visão geral das configurações
Com a funcionalidade Duplicar configuração, é possível duplicar as configurações de um nome de domínio de encaminhamento existente para um ou vários nomes novos de domínio de encaminhamento. 

>!
>- Essa funcionalidade não está disponível para os nomes de domínio desativados ou bloqueados, com declaração ICP expirada (apenas para os nomes de domínio chineses), usando certificados externos ou com configurações não aceitas variando entre regiões.
>- As configurações de back-end (por exemplo, configurações não definidas no console) não podem ser duplicadas.


## Guia de configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Duplicate Configuration (Duplicar configuração)** à direita de um nome de domínio para acessar sua página de configuração.
![](https://main.qcloudimg.com/raw/c9acd7ed82a3c675ec4369e294b2f94b.png)
Adicione um novo nome de domínio de encaminhamento e envie-o. As configurações do nome de domínio atual serão duplicadas para o novo.
![](https://main.qcloudimg.com/raw/4e8c4c4cf589118a97bd71c01f798890.png)

>?
>- O processo de envio não pode ser interrompido. Será possível gerenciar a configuração depois que o novo nome de domínio for adicionado.
>- As configurações de um novo nome de domínio serão implantadas nos nós do CDN em toda a rede, sem afetar seus negócios em execução. Se você desejar ativar o serviço de aceleração, será necessário configurar o CNAME. Para obter instruções sobre a configuração, consulte [Configuração do CNAME](https://intl.cloud.tencent.com/document/product/228/3121).
