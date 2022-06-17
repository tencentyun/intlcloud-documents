### O que significa o parâmetro `ReplyToAddresses`?
Ele indica o endereço de e-mail para o qual a mensagem de resposta será enviada. Por exemplo, quando alguém recebe seu e-mail e clica em “responder”, o e-mail de resposta será enviado para o endereço especificado por você em `ReplyToAddresses`.

### Ao tentar enviar e-mails, recebi o erro “FailedOperation.ExceedSendLimit”, indicando que o limite diário de envio de e-mails foi atingido. Qual é o limite? Posso aumentar o limite?
Por padrão, cada conta pode enviar no máximo 300 mil e-mails por dia. Para aumentar o limite, entre em contato com o [Suporte técnico da Tencent Cloud](https://console.cloud.tencent.com/workorder/category).

### Como devo inserir o `Template.TemplateData` na API `SendEmail`?
`{}` significa que nenhuma variável é passada. Para obter detalhes, consulte o campo [TemplateData](https://intl.cloud.tencent.com/document/product/1084/39418#Template) na documentação da API.
