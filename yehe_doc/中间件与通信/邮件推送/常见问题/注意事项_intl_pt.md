[](id:dns)
### Verificação da validade do DNS

Você pode usar o [DNS Checker](https://www.whatsmydns.net/) para verificar se sua configuração de DNS é válida.

[](id:add)
### Validade do endereço de e-mail
A taxa de devolução de e-mails é uma métrica rígida para a pontuação de e-mail por ISPs. O motivo mais possível para a devolução de e-mail é um endereço de e-mail inválido; ou seja, o e-mail foi enviado para um endereço incorreto. Se a taxa de devolução permanecer alta, o ISP decretará o remetente como mal-intencionado e, em seguida, enviará os e-mails para a pasta de spam ou bloqueará os IPs do remetente. Uma boa taxa de devolução não deve exceder 5%. Se os endereços de seus destinatários forem de baixa qualidade, você precisará processá-los e filtrá-los com antecedência.

[](id:garbage)
### Pasta de spam
Nenhum remetente pode garantir que um e-mail não vá para a pasta de spam do destinatário. Especialmente, quando o nome de domínio do remetente foi registrado recentemente e, portanto, não tem reputação com o ISP, é normal que os e-mails vão para a pasta de spam. É necessário um bom warm-up e engajamento de usuários para melhorar a reputação do nome de domínio. O ISP ajustará de forma dinâmica a política de spam com base na reputação e, eventualmente, enviará os e-mails para a caixa de entrada do destinatário. Portanto, recomendamos que você adicione o aviso “If you don’t see the email, please check your spam folder (Se você não encontrar o e-mail, verifique sua pasta de spam)”.

[](id:avoid)
### Medidas para evitar que os e-mails sejam marcados como spam
1. Escreva assuntos de e-mail apropriados e evite usar palavras incomuns ou muito usadas em marketing.
2. Evite “spam” óbvio, conteúdo ilegal e palavras excessivamente comercializadas, como sorteio para recarga, jogos de azar, pornografia, drogas e obscenidade.
3. Equilibre a quantidade de palavras e imagens, não use muitas imagens e evite e-mails onde há apenas uma imagem grande sem texto.
4. É melhor não adicionar URLs no conteúdo do e-mail; caso contrário, o e-mail pode ser facilmente identificado como spam.
5. Use fontes regulares em vez de várias cores ou fontes artísticas no conteúdo do e-mail.
6. Adicione um botão de cancelamento de assinatura visível no conteúdo do e-mail. Isso pode impedir que os usuários fiquem aborrecidos com seus e-mails quando não precisarem dos produtos ou serviços que você fornece, pois basta clicar no botão de cancelamento de assinatura em vez de denunciar ou bloquear seus e-mails. Isso deixará uma impressão positiva nos usuários e reduzirá a chance de seus e-mails serem reconhecidos como spam.
7. Padronize o código HTML do e-mail, pois um código não compatível pode ser identificado como spam pelo filtro de e-mail. Você precisa ter codificadores profissionais ou usar modelos de e-mail profissionais.
8. Incentive os clientes a adicionar você como amigo ou contato. Dessa forma, seus e-mails vão com certeza para a caixa de entrada deles em vez da pasta de spam.
9. Limpe a lista de destinatários regularmente. Quando seu e-mail não for entregue a muitos destinatários, os filtros de spam da maioria dos provedores de serviços de e-mail darão ao seu nome de domínio ou IP uma pontuação de índice de spam mais alta.
10. Realize testes antes de enviar e-mails formalmente. Antes de enviar seus e-mails aos destinatários formalmente, é possível usar sua própria conta para testar a entrega. Dessa forma, você também pode inferir que tipo de e-mail tem mais probabilidade de ser reconhecido como spam e otimizar o conteúdo de acordo.

[](id:multiple)
### Envio em lote
1. A funcionalidade **Batch (Em lote)** no console é adequada para envio em lote de e-mails de marketing ou de notificação. Para enviar e-mails baseados em gatilhos (como e-mails transacionais e de autenticação), é recomendável chamar a API `SendEmail`.
2. O warm-up automático é integrado à funcionalidade de envio em lote para determinar de forma inteligente a reputação do domínio/IP do remetente e a quantidade máxima permitida de e-mails enviados por dia. Quando esse limite diário for atingido, o envio de e-mails será interrompido e os demais e-mails entrarão na fila de cache e serão enviados 24 horas depois. Para saber o limite diário de e-mail de um domínio/IP para o qual não foi feito o warm-up, consulte o [Plano de warm-up padrão](https://intl.cloud.tencent.com/document/product/1084/43285#default).
3. Você pode usar um único domínio para várias tarefas de envio. Quando o volume total de e-mails exceder a quantidade máxima permitida por dia, os demais e-mails entrarão na fila de cache e serão enviados no dia seguinte.
4. Quando uma tarefa entra na fila de cache, seu status é **Paused (Pausado)** e a barra de progresso de envio permanece inalterada. Depois de reiniciar a tarefa no dia seguinte, seu status se torna **Sending (Enviando)** e a barra de progresso aumenta.
