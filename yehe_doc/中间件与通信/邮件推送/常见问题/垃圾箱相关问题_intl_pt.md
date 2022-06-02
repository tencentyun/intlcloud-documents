[](id:que1) 
### Por que meus e-mails podem ir para as pastas de spam?
Uma pasta de spam é uma política abrangente de verificação dos destinatários. Se seus e-mails acabarem em pastas de spam, a Tencent Cloud recomenda que você verifique as seguintes situações para a solução do problema:

<table id="case">
<tr><th width=8%>Nº</th><th>Descrição</th></tr>
<tr>
<td>Caso 1</td>
<td>Você está usando um domínio público ou IP público para enviar e-mails. Nesse caso, sua reputação é compartilhada e não está bem protegida. Portanto, seus e-mails podem ser considerados spams por outros provedores de serviços de e-mail e colocados em pastas de spam.</td>
</tr><tr>
<td>Caso 2</td>
<td>Você está usando um domínio ou IP novo. Como um IP novo não tem reputação, seus e-mails têm uma certa chance de ir para pastas de spam no início. No entanto, todo provedor de serviços de e-mail tem um processo de autoaprendizagem. Quando eles descobrirem que seus e-mails são confiáveis, como e-mails de verificação, eles os moverão gradualmente para a caixa de entrada.</td>
</tr><tr>
<td>Caso 3</td>
<td>Você enviou uma grande quantidade de e-mails em um curto período usando um IP novo sem um processo de warm-up, por exemplo, enviando 100 mil e-mails no primeiro dia. Nesse caso, é muito provável que os provedores de serviços de e-mail com restrições rígidas, como Hotmail e Yahoo Mail, rejeitem e considerem esses e-mails como spam.</td>
</tr><tr>
<td>Caso 4</td>
<td>A taxa de invalidação do seu endereço de e-mail é alta, o que prejudicará muito a reputação do seu remetente. A Tencent Cloud pode impedir de forma automática que você envie e-mails quando 8% dos seus e-mails estiverem na lista de bloqueados, a fim de proteger a reputação do seu IP.</td>
</tr><tr>
<td>Caso 5</td>
<td>Seus e-mails são identificados como spam pelos provedores de serviços de e-mail porque contêm conteúdo restrito, como pornografia ou anúncios. Recomendamos que você crie seus e-mails com base na proporção 2:8 de imagens para texto, com no máximo três imagens em um e-mail (não inclua conteúdo como pornografia e anúncios).</td>
</tr></table>

[](id:que2) 
### O que posso fazer para evitar que os e-mails vão para as pastas de spam?
A melhor maneira de evitar que os e-mails vão para as pastas de spam é **evitar os [cinco casos](#case) mencionados acima**.
Os fatores como o conteúdo do e-mail, a reputação do domínio, a taxa de abertura e as reclamações dos usuários determinam se um e-mail vai para as pastas de spam. Cada provedor de serviços de e-mail tem políticas de pasta de spam diferentes, sobre as quais não temos controle. No entanto, o SES da Tencent Cloud pode garantir a qualidade dos IPs do remetente.
Um domínio novo não tem reputação com os provedores de serviços de e-mail, por isso é normal que os e-mails enviados a partir dele vão para as pastas de spam. Se não houver nenhum problema com o conteúdo do seu e-mail, a situação melhorará desde que você faça um warm-up por pelo menos um mês, preste atenção na taxa de abertura e reduza a taxa de reclamações.

[](id:que3) 
### Como sei que um e-mail foi para as pastas de spam?
Você pode usar seu endereço de e-mail para testar ou fazer login no console e verificar a taxa de entrega de e-mail e a taxa de abertura para determinar se seu e-mail foi para as pastas de spam. Se a taxa de entrega de e-mail e a taxa de abertura forem baixas, provavelmente seu e-mail foi para pastas de spam.

[](id:que4) 
### O que devo fazer se meus e-mails forem para pastas de spam durante a fase de teste?
Uma pasta de spam é uma política abrangente de verificação dos destinatários. Siga as instruções abaixo:
1. Verifique se você não usou seu domínio para enviar spams anteriormente. Se a reputação do seu domínio for ruim, seus e-mails podem ir automaticamente para as pastas de spam.
2. Os destinatários podem considerar seus e-mails como spam devido ao assunto e conteúdo inadequados do e-mail. Você pode [usar a ferramenta mail-tester](https://www.mail-tester.com/) para testar o conteúdo do e-mail até obter uma pontuação superior a 8.
