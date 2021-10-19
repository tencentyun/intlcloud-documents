### O que devo fazer se um erro 423 for relatado no CDN?
O código de status 423 é um código de status personalizado do CDN do Tencent Cloud. O CDN relatará um erro 423 ao detectar uma solicitação de loopback. Recomendamos que você verifique o seguinte:
1. Verifique o servidor de origem configurado no [console do CDN](https://console.cloud.tencent.com/cdn). Se seu servidor de origem também for um nome de domínio de aceleração do CDN do Tencent Cloud, isso pode causar solicitações de loopback.
2. Se o servidor de origem estiver configurado com redirecionamento 301/302 HTTP para HTTP e a função seguir 301/302 estiver habilitada no console do CDN, um erro 423 pode ocorrer. Recomendamos que você desative a função seguir 301/302.
>!Observação: se você usar este método, recomendamos que habilite a configuração do HTTPS para forçar o redirecionamento HTTPS e alterar o método de pull de origem para seguir o protocolo. Caso contrário, podem ocorrer vários redirecionamentos. Para as etapas de configuração, consulte [Guia da configuração de aceleração HTTPS](https://intl.cloud.tencent.com/document/product/228/35213).

### O que devo fazer se um código de status 514 for retornado no CDN?

Isso é causado pelo limite de acesso de IP configurado no console do CDN conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/6422e6288811635c64052ab8daa389fc.png)

>? 
> - O limite de acesso de IP foi criado para restringir a quantidade de vezes que um IP tem permissão para acessar um nó em um segundo. Se o limite for excedido, um erro 514 será retornado.
> - Definir um limite baixo pode afetar o uso da sua empresa por usuários normais de alta frequência. Portanto, defina um limite razoável. Para obter mais informações, consulte [Configuração de limite de acesso de IP](https://intl.cloud.tencent.com/document/product/228/6420).

### O que devo fazer se um código de status 404 for retornado por um nome de domínio do CDN?
Verifique o seguinte:
1. Verifique se o servidor de origem pode ser acessado normalmente.
2. Verifique se as informações do servidor de origem e o domínio de origem foram modificados no console do CDN. Isso pode ter causado o erro 404 durante o pull de origem.


### O CDN aceita a mudança para sem pull de origem automaticamente e retorna o conteúdo armazenado em cache em um nó no caso de exceção do servidor de origem?
No caso de exceção do servidor de origem, se o cache no nó do CDN acessado pela solicitação do usuário não tiver expirado, o nó retornará diretamente o conteúdo solicitado ao cliente. Se o cache tiver expirado, ele não responderá e uma solicitação de pull de origem será iniciada.
