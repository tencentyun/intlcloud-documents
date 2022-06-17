## Observações
- Você deve ter permissões de administrador no domínio do remetente.
- Se o seu domínio estiver hospedado na Tencent Cloud, faça login no [console do DNSPod](https://console.cloud.tencent.com/cns) para configurar o domínio. Se o seu domínio estiver hospedado em outro provedor de serviços de domínio, configure-o de acordo com a lista de verificação.
- Após a configuração do domínio, a sincronização pode levar de cinco minutos a duas horas. Aguarde a conclusão da verificação.
- Após a conclusão da verificação do domínio, não exclua ou modifique os registros SPF e MX configurados, caso contrário, poderão ocorrer erros ao enviar e-mails.
- Não use um domínio de e-mail corporativo para evitar conflitos entre registros SPF e MX. Você pode criar e usar um domínio de segundo nível em seu domínio de e-mail corporativo atual.
- Cada conta da Tencent Cloud pode ser configurada com até dez domínios.

<span id ="Step1"></span>
## Etapa 1. Fazer login no console
Faça login no [Console do SES](https://console.cloud.tencent.com/ses). Se você ainda não tem uma conta da Tencent Cloud, consulte [Criação de conta da Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985) para criar uma.

<span id ="Step2"></span>
## Etapa 2. Realizar a verificação da organização
Se você não concluiu a verificação de identidade da sua conta, acesse o [Centro de contas](https://console.cloud.tencent.com/developer) para verificar sua identidade. Para obter mais informações, consulte o [Guia de verificação de identidade](https://intl.cloud.tencent.com/document/product/378/3629).

<span id ="Step3"></span>
## Etapa 3. Ativar o SES
Se você já concluiu a verificação de identidade da sua conta, clique em **Activate (Ativar)** para ativar o SES. Após a ativação, você receberá uma camada gratuita de mil e-mails.
Após o uso da camada gratuita, seus planos passarão a ser utilizados automaticamente. Se não houver planos disponíveis, você será cobrado via pagamento conforme o uso.

<span id ="Step4"></span>
## Etapa 4. Configurar um domínio de remetente
>!Se um domínio foi registrado para o Tencent Exmail, ele não pode ser usado como o domínio de remetente.
1. Faça login no [console do SES](https://console.cloud.tencent.com/ses) e clique em **Sender Domain (Domínio de remetente)**.
2. Na página **Sender Domain (Domínio de remetente)**, clique em **Create (Criar)**.
3. Insira um domínio de remetente no campo **Domain (Domínio)**, por exemplo, `mail.qcloud.com` e clique em **Submit (Enviar)**.
    
>!Um domínio de remetente é a base de um endereço de e-mail e representa a identidade corporativa do remetente. Para verificar um domínio de remetente, é necessário configurar as informações de DNS dele. Portanto, você deve ter permissões de administrador no domínio.
   
4. Após a conclusão da configuração do DNS, clique em **Verify (Verificar)**.
5. Na caixa de diálogo **Sender Domain Configuration (Configuração do domínio de remetente)**, clique em **Submit (Enviar)** para verificar o domínio de remetente.

<span id ="Step5"></span>
## Etapa 5. Configurar um endereço de remetente

1. Retorne à página **Overview (Visão geral)** e clique em **Sender Address (Endereço de remetente)**.
2. Na página **Sender Address (Endereço de remetente)**, clique em **Create (Criar)**.
3. Defina os seguintes parâmetros:
	- Domínio de remetente: selecione um domínio de remetente **verificado** criado na [etapa 4](#Step4).
	- Prefixo de e-mail: por exemplo, `test`.
	- Nome do remetente: por exemplo, `Lil C`.
>!Seu endereço de remetente deve ser um endereço de e-mail completo com o sufixo de um domínio de remetente **verificado**.
>Por exemplo, <code>test@example.qcloudmail.com</code>.

4. Clique em **Submit (Enviar)** para concluir a configuração do endereço de remetente.

<span id ="Step6"></span>
## Etapa 6. Configurar um modelo
1. Retorne à página **Overview (Visão geral)** e clique em **Email Template (Modelo de e-mail)**.
2. Na página **Email Template (Modelo de e-mail)**, clique em **Create (Criar)**.
3. Defina os seguintes parâmetros:
	- Nome do modelo: por exemplo, `test`.
	- Tipo de modelo: selecione **HTML rich text**.
	- Resumo do e-mail: por exemplo, `notification email template`.
	- Corpo do e-mail: clique em **Choose a file (Escolher um arquivo)** e selecione um arquivo HTML como corpo do e-mail.
>?O conteúdo do e-mail pode estar em formato de texto simples ou rich text. O formato rich text requer código HTML preparado com antecedência. Após o envio do modelo, ele entrará na fase de revisão e poderá ser usado mediante aprovação. A revisão será concluída em um dia útil.

4. Clique em **Preview (Visualizar)** para exibir o modelo de e-mail.

5. Clique em **Submit (Enviar)** para concluir a configuração do modelo.

<span id ="Step7"></span>
## Etapa 7. Enviar e-mails
Após a conclusão do registro do domínio e a aprovação do modelo, você poderá enviar e-mails por meio do console do SES ou de chamadas de API.
1. Clique em **Email Sending (Envio de e-mail)** para acessar a página de envio de e-mail.
>?Esta página é apenas para testar o envio de e-mail. São permitidos até 20 endereços de destinatários para um único teste. Você pode enviar e-mails para mais destinatários por vez por meio de chamadas de API. Para obter mais informações, consulte [aqui](https://intl.cloud.tencent.com/document/product/1084/39408).
2. Defina os seguintes parâmetros:
 - Modelo: selecione um modelo **aprovado** criado na [etapa 6](#Step6).
 - Assunto: insira o assunto do e-mail correspondente.
 - De: selecione um endereço de remetente configurado na [etapa 5](#Step5).
 - Para: insira os endereços de e-mail para os quais você deseja enviar o e-mail.
 - Variáveis: insira as variáveis correspondentes.
3. Após o envio do e-mail, clique em [Statistics (Estatísticas)](https://console.cloud.tencent.com/ses/stats) para exibir as estatísticas.

