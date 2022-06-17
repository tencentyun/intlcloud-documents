[](id:que1) 
### O SES pode acessar os e-mails que envio e recebo? 

O SES usa tecnologias internas antispam para filtrar os e-mails com conteúdo ruim. Além disso, ele verifica todos os e-mails contendo anexos com relação a vírus e outros conteúdos maliciosos. No entanto, ele não salvará seu conteúdo de e-mail.

[](id:que2) 
### Meus e-mails podem ser criptografados?
Durante a transferência de e-mail, o SES criptografará o conteúdo de seus e-mails.

[](id:que3) 
### O SES usa o Transport Layer Security (TLS) para enviar e-mails por uma conexão criptografada?
O SES aceita o TLS 1.2, TLS 1.1 e TLS 1.0 para conexão TLS.

Por padrão, o SES usa o TLS. Isso significa que o SES sempre tentará estabelecer uma conexão segura com o servidor de e-mail do destinatário. Se não conseguir estabelecer uma conexão segura, ele enviará o e-mail de maneira não criptografada. Você pode alterar essa opção para que o SES só envie e-mails quando uma conexão segura puder ser estabelecida.

[](id:que4) 
### Como o SES garante que os e-mails recebidos não sejam spam e estejam livres de vírus?
O SES adota muitas medidas de proteção contra spam e vírus. A Tencent Cloud mantém especificamente uma biblioteca de endereços de e-mail bloqueados e bloqueia os e-mails desses endereços para ajudar a filtrar e-mails mal-intencionados. O SES verifica todos os e-mails recebidos contendo anexos em busca de vírus. Ele fornece vários métodos de detecção de spam; por exemplo, além dos resultados da verificação de spam e vírus, ele também fornece resultados de verificação DKIM e SPF.

[](id:que5) 
### Quais tecnologias podem impedir que os usuários do SES enviem spam? 

O SES usa tecnologias internas de filtragem de conteúdo para detectar spam. Além disso, também fornece ferramentas de pontuação de qualidade de e-mail para ajudar você a verificar o conteúdo do e-mail por conta própria. Se descobrir que uma conta está enviando spam ou conteúdo mal-intencionado, ele suspenderá a capacidade da conta de enviar outros e-mails.
>! O e-mail pode ser encaminhado para as pastas de spam mesmo que não seja, efetivamente, um spam. A pontuação de qualidade do e-mail é apenas para referência. Os fatores como o conteúdo do e-mail, a reputação do domínio, a taxa de abertura e as reclamações dos usuários determinam se um e-mail vai para as pastas de spam. Cada provedor de serviços de e-mail tem políticas de pasta de spam diferentes, sobre as quais não temos controle. No entanto, o SES pode garantir a qualidade dos IPs do remetente.

