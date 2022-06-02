[](id:que1) 
### Como o SES garante uma transmissão de e-mail confiável?
Depois de criar um modelo de e-mail, analisaremos o conteúdo do modelo para garantir que ele atenda aos requisitos do ISP. Para melhorar ainda mais sua taxa de entrega de e-mails, o SES fornece um mecanismo de feedback que inclui devoluções de e-mail, reclamações e notificações de entrega.

[](id:que2) 
### O SES pode garantir a entrega bem-sucedida dos meus e-mails?
Tanto no SES como no caso de qualquer outro serviço de e-mail, não é possível garantir 100% de entrega bem-sucedida de todos os e-mails, o que é afetado por muitos fatores, como conteúdo do e-mail, reputação do nome de domínio, taxa de abertura e reclamações dos usuários. Para obter mais informações, consulte [Como impedir que meus e-mails sejam marcados como spam?](https://intl.cloud.tencent.com/document/product/1084/42369).


[](id:que3) 
### Quanto tempo leva para um e-mail enviado pelo SES chegar à caixa de entrada do destinatário?
Normalmente, o tempo para que um e-mail seja entregue na caixa de entrada do destinatário fica entre 3 segundos e 5 minutos, com um prazo máximo 72 horas. Alguns e-mails podem sofrer atrasos devido a fatores como o conteúdo do e-mail e a política do provedor de serviços de e-mail. Portanto, é normal entregar um e-mail em mais de 5 minutos.

[](id:que4) 
### As devoluções de e-mail ou reclamações causadas por outros usuários do SES afetarão minha taxa de entrega de e-mail?
Normalmente, se você estiver usando um IP compartilhado, as devoluções de e-mail ou reclamações causadas por outros usuários do SES podem afetar um pouco a sua taxa de entrega de e-mail. Se você estiver usando um IP dedicado, não haverá impacto.

[](id:que5) 
### O que devo fazer se a imagem no e-mail não for exibida?
Você pode solucionar o problema das seguintes formas:

1. Verifique se o URL da imagem está correto.
2. Verifique se o seu cliente de e-mail proíbe o carregamento de imagens. Se proibir, clique no botão **Show Image (Mostrar imagem)**.
3. Verifique se a imagem foi bloqueada pelo destinatário.

[](id:que6) 
### O que devo fazer se meu e-mail enviado pelo SES for bloqueado pelo serviço de e-mail corporativo?
Normalmente, os serviços de e-mail corporativo bloqueiam e-mails de publicidade, portanto, não inclua conteúdo de publicidade no assunto e no conteúdo do seu e-mail, a menos que seja necessário.

[](id:que7) 
### Por que meu e-mail não foi enviado?
Primeiro, verifique o documento de códigos de erros para determinar o tipo de erro.

Em seguida, solucione o problema na seguinte ordem:
1. Verifique se a conta tem a permissão `QcloudFullAccess` e se `SecretId` e `SecretKey` estão corretos.
2. Confirme se o domínio do remetente foi verificado. (Não modifique o DNS configurado depois de ser aprovado na verificação.)
3. Verifique se o endereço de e-mail do destinatário está correto.
4. Verifique se o modelo foi aprovado e se o formato de `TemplateData` está correto.
5. “You can only send emails using a template (Você só pode enviar e-mails usando um modelo)” indica que você não pode enviar um e-mail diretamente. Envie seu e-mail usando um modelo.

Se o problema persistir, entre em contato com a [equipe técnica da Tencent Cloud](https://console.cloud.tencent.com/workorder/category) para obter ajuda.

[](id:que8) 
### Qual é o mecanismo de cancelamento de assinatura?
Quando um usuário final cancelar a assinatura de e-mails enviados por um cliente, a Tencent Cloud notificará o cliente sobre o evento de cancelamento de assinatura e registrará o status de cancelamento de assinatura do usuário final. Além disso, o domínio de remetente correspondente não poderá mais enviar e-mails para esse usuário final.

[](id:que9) 
### Por que alguns e-mails são bloqueados?
A Tencent Cloud mantém um banco de dados com uma lista de endereços bloqueados e bloqueia o envio de e-mails para esses endereços. Isso ajuda os clientes a filtrarem solicitações de e-mail mal-intencionadas. Além disso, para proteger a reputação do remetente dos clientes, a Tencent Cloud adiciona os endereços de destinatários que foram rejeitados recentemente ao banco de dados da lista de bloqueados. O banco de dados da lista de bloqueados é compartilhado por todas as contas, portanto, as listas de endereços bloqueados geradas em contas diferentes são adicionadas ao mesmo banco de dados. Os endereços de e-mail no banco de dados da lista de bloqueados ficarão bloqueados por 14 dias. Você pode fazer login no [console do SES](https://console.cloud.tencent.com/ses/stats) ou chamar a API para desbloqueá-los. Se os endereços dos destinatários forem válidos e não estiverem na sua lista de bloqueados, eles poderão ser bloqueados por outras contas. Nesse caso, você pode entrar em contato com a [equipe técnica da Tencent Cloud](https://console.cloud.tencent.com/workorder/category) para desbloqueá-los.


[](id:use)
### Taxa de abertura do usuário
A taxa de abertura do usuário também é uma métrica importante para saber se um e-mail vai para a caixa de entrada. Quanto maior a taxa de engajamento do usuário, maior a probabilidade de o ISP aumentar a credibilidade do nome de domínio adequadamente. De um modo geral, é normal que a taxa de abertura de e-mails cadastrados seja superior a 80%. Para e-mails de notificação, essa métrica depende dos cenários de negócios. Para e-mails de marketing, você deve otimizar continuamente o assunto e o conteúdo do e-mail para engajar os usuários. Se essa métrica estiver abaixo de 50%, os e-mails enviados provavelmente vão para a caixa de spam.


