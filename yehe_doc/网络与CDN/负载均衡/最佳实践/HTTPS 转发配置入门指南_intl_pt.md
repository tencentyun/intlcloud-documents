## 1. Descrição da capacidade do CLB

Ao otimizar profundamente a pilha de protocolo e o servidor, o CLB do Tencent Cloud obtém uma grande melhoria no desempenho de HTTPS. Ao mesmo tempo, o Tencent Cloud reduz substancialmente os custos de certificados por meio da colaboração com autoridades de certificação internacionais. O CLB pode trazer benefícios significativos para o seu negócio nos seguintes aspectos:

1. O uso de HTTPS não afeta a velocidade de acesso do cliente.
2. O desempenho de criptografia e descriptografia SSL de um único servidor em um cluster pode sustentar handshakes completos de até 65.000 conexões por segundo (CPS), o que é pelo menos 3,5 vezes superior ao de uma CPU de alto desempenho. Isso reduz os custos do servidor, melhora muito a capacidade do serviço durante os picos de negócios e picos de tráfego e fortalece a capacidade anti-ataque baseada em computação.
3. O descarregamento e a conversão de vários protocolos são compatíveis, o que reduz o estresse da empresa na adaptação a vários protocolos de cliente. O back-end da empresa só precisa oferecer suporte a HTTP/1.1 para usar diferentes protocolos, como HTTP/2, SPDY, SSL 3.0 e TLS 1.2.
4. Serviços de requisição, monitoramento e substituição de certificado SSL em um só lugar são fornecidos. O Tencent Cloud coopera com a Comodo e SecureSite, duas autoridades que são líderes globais em certificação, para simplificar muito o processo de requisição de certificado e reduzir os custos envolvidos.
5. Os recursos Anti-CC e WAF são oferecidos para eliminar efetivamente os ataques à camada de aplicativos, como ataques HTTP lentos, ataques direcionados de alta frequência, injeção de SQL e cavalos de tróia em sites.

## 2. Identificadores de cabeçalho HTTP e HTTPS

O CLB atua como um proxy para HTTPS. As solicitações HTTP e HTTPS tornam-se solicitações HTTP quando encaminhadas para uma instância CVM de back-end pelo CLB. Nesse caso, você não consegue distinguir se uma solicitação de front-end está em HTTP ou HTTPS.

O CLB implanta `X-Client-Proto` no cabeçalho quando encaminha a solicitação para o servidor de back-end:

X-Client-Proto: http (solicitação HTTP no front-end)
X-Client-Proto: https (solicitação HTTPS no front-end)

## 3. Introdução


Suponha que você precise configurar o site `https://example.com`, para que os usuários finais possam visitá-lo com segurança via HTTPS quando entrarem diretamente em `www.example.com` no navegador.

Nesse caso, a solicitação de acesso a `www.example.com` inserida por um usuário final será encaminhada conforme abaixo:

1. A solicitação é transferida por HTTP e acessa a porta 80 do listener do CLB por meio do VIP. Em seguida, ele é encaminhado para a porta 8080 do servidor de back-end.

2. Com a configuração de reescrita em Nginx no servidor de back-end, a solicitação passa pela porta 8080 e é reescrita na página `https://example.com`.

3. Em seguida, o navegador envia a solicitação `https://example.com` ao site HTTPS correspondente novamente. A solicitação acessa a porta 443 do listener do CLB por meio do VIP e, em seguida, é encaminhada à porta 80 do servidor de back-end.

Neste ponto, o processo de encaminhamento da solicitação é concluído.

Essa operação reescreve uma solicitação HTTP do usuário do navegador em uma solicitação HTTPS mais segura e é imperceptível para o usuário. Para implementar a operação de encaminhamento de solicitação acima, você pode configurar o servidor de back-end da seguinte maneira:

```
server {

	listen 8080; 
	server_name example.qcloud.com;

	location / {

		#! customized_conf_begin;
		client_max_body_size 200m;
		rewrite ^/.(.*) https://$host/$1 redirect;

} 
}
```

Como alternativa, na nova versão do Nginx, redirecione a página Nginx HTTP para a página HTTPS usando o método de redirecionamento 301 recomendado:

```
server { 	
  	listen	  80;
  	server_name    example.qcloud.com;
  	return	  301 https://$server_name$request_uri;
}

server {
  	listen	  443 ssl;
 	server_name    example.qcloud.com;
	[....]
}
```
