[](id:que1) 
### Posso enviar e-mails de qualquer endereço de e-mail?
**Não**, você pode usar o SES para enviar e-mails apenas de endereços ou domínios de sua propriedade.

Primeiro, o domínio deve ser verificado para provar que você é o proprietário. Cada conta da Tencent Cloud pode ter até 10 domínios. Para obter mais informações sobre a verificação de endereços de e-mail e domínios, consulte a **Etapa 4. Configurar um domínio de remetente** em [Introdução](https://intl.cloud.tencent.com/document/product/1084/39332).

[](id:que2) 
### Existe um limite no tamanho de um e-mail enviado pelo SES?
Sim, um e-mail (incluindo imagens e anexos) não pode exceder 4 MB.

[](id:que3) 
### Existem limites na quantidade de e-mails que posso enviar?
Cada conta do SES tem um conjunto de limites de envio, incluindo:

- Quantidade máxima de envios diários: a quantidade máxima de e-mails que você pode enviar em 24 horas. Por padrão, esse limite é de 300 mil e-mails diários para cada conta. No entanto, você pode aumentar esse limite.
- Taxa máxima de envio: a quantidade máxima de e-mails que você pode enviar por segundo. Por padrão, esse limite é de 20 e-mails por segundo para cada conta.
- Quantidade máxima de envios para o mesmo endereço de e-mail por hora: 10 (padrão). Se esse limite for excedido, os demais e-mails para este endereço serão bloqueados. Você pode reenviá-lo após 1 hora. Esse mecanismo serve para evitar exceções de negócios e de push.

>! 
>- Todos os três limites acima podem ser ajustados. Entre em contato com o suporte técnico da Tencent Cloud e informe o cenário de envio e o motivo, se precisar solicitar o ajuste.
>- Se encontrarmos um problema com a qualidade do seu e-mail, como uma alta taxa de reclamação ou de devolução, temos o direito de impedir você de enviar e-mails pelo SES.

[](id:que4) 
### Há alguma restrição no formato do assunto do e-mail?
O assunto do e-mail deve estar no formato UTF-8 e conter no máximo 998 caracteres. Caso contrário, o e-mail não será enviado. A Tencent Cloud recomenda que você mantenha o assunto em 78 caracteres.

[](id:que5) 
### Existem restrições nos endereços de e-mail dos destinatários ao enviar e-mails por meio de chamadas de API?
Não. No entanto, os endereços de e-mail dos destinatários devem ser válidos (não obtidos por rastreamento ou comprados de terceiros) e são necessários gatilhos ativos ou assinaturas dos destinatários.

[](id:que6) 
### O que devo fazer para poder enviar conteúdo personalizado?
Você só pode enviar e-mails usando um modelo.
