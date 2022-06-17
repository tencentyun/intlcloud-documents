## Parâmetros de entrada
| Campo | Descrição | Comentários |
| ------------------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Bcc | Endereço de cópia oculta | Não aceito no momento |
| Cc | Endereço de cópia | Não aceito no momento |
| Content-Transfer-Encoding | Método de codificação de transferência de conteúdo | Não usado no momento. Você pode deixar em branco. O conteúdo, exceto os anexos, não precisa ser criptografado |
| Content-Type | Tipo de conteúdo | Atualmente, você só pode passar `text/plain; charset=UTF-8,text/html; charset=UTF-8 multipart/mixed`, `multipart/related` ou `multipart/alternative`; caso contrário, um erro será relatado |
| Date | Data e hora | Não usado no momento |
| Delivered-To | Endereço do destinatário | Não usado no momento |
| From | Endereço do remetente | Obrigatório |
| Message-ID | ID da mensagem | Não usado no momento |
| MIME-Version | Versão do MIME | Não usado no momento. Deixe vazio ou passe 1.0; caso contrário, um erro será relatado |
| Received | Caminho de transferência | Não usado no momento |
| Reply-To | Endereço de resposta | Não usado no momento |
| Return-Path | Endereço de resposta | Não usado no momento |
| Subject | Assunto | Obrigatório |
| To | Endereço do destinatário | Obrigatório |

### Parâmetros de anexo (quando for enviar anexo)
| Campo | Descrição | Comentários |
| ------------------------- | --------- | ------------------------------ |
| Content-Type | Tipo de conteúdo | Recomendamos que você passe `application/octet-stream` para arquivos |
| Content-Transfer-Encoding | Método de codificação de transferência de conteúdo | Atualmente, apenas Base64 é aceito e um erro será relatado se você passar outros valores |
| Content-Disposition | Método de disposição de conteúdo | Atualmente, você só pode passar `attachment`, além disso, anexos não podem ser enviados se você passar outros valores |
| Content-ID | ID do conteúdo    | Não aceito no momento |
| Content-Location | Local do conteúdo (caminho) | Não aceito no momento |
| Content-Base | Local da base de conteúdo | Não aceito no momento |

>?Normalmente, os requisitos de verificação dos parâmetros de entrada são os mesmos de [SendEmail](https://intl.cloud.tencent.com/document/product/1084/39408), incluindo as restrições sobre a quantidade de destinatários, tamanho do corpo do e-mail, formato do anexo e tamanho do anexo.

## Parâmetros de resposta
A API do SMTP não tem parâmetros de resposta e aceita apenas o retorno das informações `err`. Se `nil` for retornado, isso indica que a chamada da API foi bem-sucedida, mas o envio de e-mail real pode não ter sido necessariamente bem-sucedido. Para obter o status de envio, consulte [GetSendEmailStatus](https://intl.cloud.tencent.com/document/product/1084 /39502).

## Códigos de erro
### Erros do sistema
1. Há 2 mil ou mais caracteres em uma única linha no corpo do email.
`554 5.0.0 Error: transaction failed, blame it on the weather: smtp: too longer line in input stream` ou outros logs que contenham `too longer`.
`write tcp *.*.*.*:60575->*.*.*.*:25: write: broken pipe`

2. O anexo é muito grande.
Se o anexo tiver cerca de 9 MB de tamanho, o EOF será retornado. Recomendamos que você mantenha o tamanho total do anexo menor que 8 MB e o tamanho total da mensagem menor que 10 MB. Caso contrário, o conteúdo será truncado e outros erros de exceção, como falha de decodificação Base64, serão relatados.
				
### Erros de negócios
O formato de um erro de negócios é o seguinte:
`
554 5.0.0 Error: transaction failed, blame it on the weather: ##SES-response-json: {"Response":{"RequestId":"bee4e9fb-8127-48cc-b606-bbb1e801596b","QcloudError":{"Error":{"Code":"FailedOperation.MissingEmailContent. A operação falhou. O conteúdo do e-mail está ausente (`TemplateData` e `Simple` não podem estar ambos vazios).
`
 Após `##SES-response-json:` está a forma `json` da estrutura retornada pela API de envio. Os campos são conforme descrito abaixo:

| Campo | Tipo | Descrição |
| ----------- | ------ | ----- |
| RequestId | string | ID da solicitação | 
| QcloudError | stuct | Estrutura de erro | 

QcloudError:

| Campo | Tipo | Descrição | 
| ----------- | ------ | ----- | 
| Code | string | Código do erro | 
| Message | string | Mensagem de erro | 



Descrição geral de erro de negócios:

| Código do erro | Descrição do erro | Comentários |
| ---------------------------------- | ------------------------------------------------------------------ | ------------------------------------- |
| FailedOperation | msg.From is null | O remetente está vazio |
| FailedOperation | msg.Subject is null | O assunto está vazio |
| FailedOperation | msg.Body is null | O corpo da mensagem está vazio |
| FailedOperation | Content-Transfer-Encoding must in... | Verifique o parâmetro `Content-Transfer-Encoding` em relação à descrição do parâmetro de entrada |
| FailedOperation | Content-Type must in... | Verifique o parâmetro `Content-Type` no cabeçalho em relação à descrição do parâmetro de entrada |
| FailedOperation | Mime-Version must in... | Verifique o parâmetro `Mime-Version` no cabeçalho em relação à descrição do parâmetro de entrada |
| FailedOperation | The email is too large. Remove some content... | O corpo do e-mail, exceto os anexos, não pode exceder 1 MB de tamanho |
| FailedOperation | Incorrect attachment content. Make sure the base64 content is... | O conteúdo do anexo deve ser codificado em Base64 |
| FailedOperation | The attachments are too large. Make sure they do not exceed the... | O tamanho de um único anexo excede 5 MB ou o tamanho total de todos os anexos excede 10 MB (o que pode ser ajustado) |
| RequestLimitExceeded.SmtpRateLimit | smtp sending frequency limit... | O limite de taxa de chamadas do SMTP foi atingido |

### Outros erros de negócios
Você pode consultar as descrições dos códigos de erro em [SendEmail](https://intl.cloud.tencent.com/document/product/1084/39408).
