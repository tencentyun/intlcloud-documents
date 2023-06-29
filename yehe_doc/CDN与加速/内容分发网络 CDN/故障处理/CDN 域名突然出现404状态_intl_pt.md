## Descrição do erro

 O que devo fazer se um código de status 404 for retornado por um nome de domínio do CDN?



## Causa

1. O servidor de origem é excepcional.
2. A configuração das informações do servidor de origem e do cabeçalho do host no console estão alteradas.



## Solução

1. Verifique se o seu servidor de origem funciona corretamente.
2. Verifique se a configuração das informações do servidor de origem e do cabeçalho do host no console estão corretas.



## Procedimento de solução de problemas

[](id:step1)

1. Verifique se o seu servidor de origem é excepcional.

   - Se for o caso, corrija o servidor de origem.
   - Se não for o caso, vá para a [Etapa 2](# step2).
     [](id:step2)

2. Verifique a configuração das informações do servidor de origem e o cabeçalho do host no console.
   Faça login no [console CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)**, encontre o nome de domínio correspondente, selecione **Basic Configuration (Configuração básica)** > **Origin Server Information (Informações do servidor de origem)** e verifique se as configurações de **Origin address (Endereço de origem)** e **Host header (Cabeçalho do host)** estão corretas.

   - Tipo de origem:

   <table>
   <thead>
   <tr>
   <td><strong>Servidor de origem do cliente</strong></td>
   <td>Se você selecionar o servidor de origem do cliente, deverá fornecer um endereço IP ou nome de domínio do servidor de negócios que pode ser acessado normalmente.</td>
   </tr>
   </thead>
   <tbody><tr>
   <td><strong>Servidor de origem do COS</strong></td>
   <td>Se você selecionar um bucket no COS como o servidor de origem, selecione **Default Domain (Domínio padrão)** ou **Static Website (Site estático)** com base na configuração do bucket. Se seu bucket for privado, autorize o CDN e ative a autenticação do pull de origem para ativar o acesso privado ao bucket.</td>
   </tr>
   <tr>
   <td><strong>Armazenamento de objetos de terceiros</strong></td>
   <td>Se você selecionar um serviço de armazenamento de objetos de terceiros, insira o endereço válido de acesso ao bucket como o servidor de origem. Atualmente, o AWS S3 e o Alibaba Cloud OSS são compatíveis. Se o bucket for privado, insira uma chave válida e ative a autenticação de pull de origem para ativar o acesso privado ao bucket.</td>
   </tr>
   </tbody></table>

   - Cabeçalho de host:
     Refere-se ao nome de domínio acessado no servidor de origem por um nó do CDN durante o pull de origem. O padrão é o nome de domínio de aceleração. Se um nome de domínio curinga for conectado, será o nome do subdomínio de acesso real por padrão e poderá ser personalizado. (**Observação:** não pode ser modificado se o tipo de servidor de origem for COS ou um serviço de armazenamento de objetos de terceiros).

Para obter mais informações sobre configuração de servidor de origem, consulte [Configuração do servidor de origem](https://intl.cloud.tencent.com/document/product/228/6289).
