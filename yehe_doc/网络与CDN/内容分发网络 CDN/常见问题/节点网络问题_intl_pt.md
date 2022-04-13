
[](id:q1)
### Qual é o tempo limite padrão para os nós do CDN da Tencent Cloud?
O tempo limite padrão é de 10 segundos.

[](id:q2)
### O que acontecerá com os arquivos nos nós do CDN se eu desabilitar o nome de domínio conectado no console do CDN?
Se você desabilitar o serviço do CDN de um nome de domínio conectado, os nós do CDN manterão as configurações de conexão do nome de domínio, o tráfego do CDN não será mais gerado e o nome de domínio ficará inacessível.

[](id:q3)
### O que eu devo fazer se não conseguir abrir meu site depois de conectá-lo ao CDN?
Primeiro, como o site não pode ser aberto quando o status do CDN do nome de domínio conectado for **Disabled (Desabilitado)**, verifique o status. Se o status não for **Desabilitado (Desabilitado)**, você pode prosseguir com uma verificação:
+ Execute `ping` ou `nslookup` para verificar se a resolução do CNAME do nome de domínio entrou em vigor. Se o CNAME ainda não tiver sido adicionado, acesse o seu provedor de DNS e adicione o CNAME conforme as instruções em [Configuração do CNAME](https://intl.cloud.tencent.com/document/product/228/3121).
+ Depois que o CNAME entrar em vigor, você pode verificar se o servidor de origem está acessível.

Se o problema persistir, [envie um tíquete](https://console.cloud.tencent.com/workorder/category) para obter ajuda.

[](id:q4)
### Como eu determino qual nó do CDN foi acessado pelos usuários?
Ao executar os comandos `nslookup` e `ping`, é possível obter informações básicas de solução de problemas, como IP, latência e perda de pacotes do nó CDN acessado pelos usuários.

[](id:q5)
### Por que eu tenho uma taxa de acertos baixa?
Normalmente, isso ocorre pelos seguintes motivos:
+ Há um problema de configuração do cache, como um período curto de validade do cache.
+ O cabeçalho HTTP impede o cache. Verifique as configurações de `Cache-Control` ou `Expires` do servidor de origem.
+ Existem poucos conteúdos armazenáveis em cache para o tipo de servidor de origem.
+ O site tem poucas visitas e o período de validade é curto. A taxa de acertos baixa para os arquivos leva a solicitações frequentes de pull de origem.

[](id:q6)
### Por que a conexão dos usuários é lenta quando acessam o CDN?
Verifique a velocidade de download para arquivos grandes e a latência para arquivos pequenos. Primeiro, obtenha o URL de acesso lento para os usuários e determine se o acesso está lento usando sites de teste de velocidade como [17ce](http://www.17ce.com) (recomendado).
Se o resultado do teste confirmar a velocidade lenta e o servidor de origem for um servidor de origem externo, [envie um tíquete](https://console.cloud.tencent.com/workorder/category). Ajudaremos os usuários a verificar se a carga e a largura de banda estão restritas na máquina do servidor de origem.

[](id:q7)
### Como eu posso saber se o acesso do usuário acertou o cache do CDN?
Consulte as informações de `X-Cache-Lookup` no cabeçalho do retorno da solicitação. Se várias entradas `X-Cache-Lookup` forem retornadas ao mesmo tempo, isso é normal. Se `Cache Hit`/`Hit From MemCache`/`Hit From Disktank` for retornado, significa que o cache do CDN foi atingido.
![](https://mc.qcloudimg.com/static/img/64ac912c895b36f0241a927df6da3543/image.png)
+ `X-Cache-Lookup:Hit From MemCache`: a memória do nó do CDN foi atingida.
+ `X-Cache-Lookup:Hit From Disktank`: o disco do nó do CDN foi atingido.

[](id:q8)
### Por que os arquivos com o mesmo nome retornados pelo nó têm tamanhos diferentes?
Como todos os tipos de arquivo são armazenados em cache por padrão, pode haver versões diferentes de um arquivo no nó do CDN. Para resolver esse problema, você pode:
+ Limpar manualmente os arquivos e atualizar o cache imediatamente.
+ Usar um número de versão, como `http://www.xxx.com/xxx.js?version=1`.
+ Mudar os nomes dos arquivos para evitar o uso de arquivos com o mesmo nome.

Se o problema persistir, [envie um tíquete](https://console.cloud.tencent.com/workorder/category) para obter ajuda.

[](id:q9)
### O que eu devo fazer se meu site não puder ser acessado depois que a lista de permissões de proteção de hotlink for configurada no CDN?

Selecione **Allow blank referer (Permitir referenciador em branco)** ao configurar a lista de permissões de proteção de hotlink, para que o site possa ser aberto normalmente em um navegador (com um referenciador em branco).
![Image description](https://main.qcloudimg.com/raw/3ec77732d4f5266278af2e8f569b08a2.png)

[](id:q10)
### A configuração do limite de tráfego pode proteger contra ataques DDoS?

O CDN se concentra principalmente na aceleração da entrega de conteúdo, e não na proteção de DDoS. É possível usar a funcionalidade de limite de largura de banda do CDN para coletar automaticamente as estatísticas de uso de largura de banda em 5 minutos. Se o limite máximo for atingido, o CDN responderá de acordo com a configuração. **O limite máximo é 10.000 Tbps.** Para proteger seu site contra ataques DDoS, use [Secure Content Delivery Network](https://intl.cloud.tencent.com/products/scdn).

[](id:q11)
### O CDN pode fornecer todos os seus IPs de nós? 
Não. Por questões de segurança, o CDN não pode fornecer uma lista completa de IPs de nós. No entanto, você pode consultar a região de IP na página **Verify Tencent Cloud CDN IP (Verificar IP do CDN da Tencent Cloud)**. Para obter mais informações, consulte [Verificar IPs da Tencent](https://intl.cloud.tencent.com/document/product/228/10747).
