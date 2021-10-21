## Visão geral do CDN

O Content Delivery Network (CDN) é uma nova camada de arquitetura de rede criada na internet existente. Ele consiste em nós de cache de alto desempenho distribuídos internacionalmente para acelerar a entrega de conteúdo da internet. Esses nós armazenam seu conteúdo com base em políticas de cache. Quando um usuário faz uma solicitação de conteúdo, ela é roteada para o nó mais próximo do usuário, reduzindo o atraso no acesso e melhorando a disponibilidade.

O CDN fornece uma solução eficaz para os seguintes problemas de rede:
1. A grande distância física entre o usuário e o servidor empresarial requer que a solicitação seja encaminhada várias vezes, resultando em alta latência e instabilidade.
2. O ISP usado pelo usuário é diferente do usado pelo servidor empresarial, portanto, a solicitação precisa ser encaminhada entre os ISPs depois que eles são interconectados.
3. O servidor empresarial tem largura de banda e recursos de processamento limitados, resultando em uma resposta mais lenta e menor disponibilidade quando há grandes quantidades de solicitações de usuários.

O CDN é fácil de usar. Não é necessário ajustar sua estrutura empresarial ou gerenciar configurações complexas. Para obter mais informações, consulte [Introdução](https://intl.cloud.tencent.com/document/product/228/32978).

## Como funciona a aceleração
Por exemplo, se o nome de domínio do servidor de origem da sua empresa for  `www.test.com` e tiver sido conectado ao CDN para ativar o serviço de aceleração, quando um usuário fizer uma solicitação HTTP, ela será processada conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/c155f8268c6ebdcc84f50cfb06f1f638.png)

**O processo está detalhado abaixo:**
1. Quando um usuário faz uma solicitação de acesso para um recurso de imagem (por exemplo, 1.jpg) em `www.test.com`, uma solicitação de resolução de nome de domínio será iniciada para o DNS local.
2. Quando o DNS local resolver `www.test.com`, ele encontrará que o `www.test.com.cdn.dnsv1.com` do CNAME foi configurado, então a solicitação de resolução será enviada ao Tencent DNS (GSLB), o sistema de agendamento proprietário do Tencent Cloud que atribuirá o IP do nó ideal para a solicitação.
3. O DNS local recebe o IP resolvido retornado pelo Tencent DNS.
4. O usuário recebe o IP resolvido.
5. O usuário faz uma solicitação de acesso de 1.jpg ao IP recebido.
6. Se o nó do CDN correspondente ao IP já tiver armazenado 1.jpg em cache, os dados serão devolvidos diretamente ao usuário (10) e a solicitação será encerrada. Caso contrário, o nó do CDN iniciará uma solicitação de 1.jpg para o servidor de origem (6, 7 e 8). Depois de receber o recurso, o nó do CDN vai armazená-lo em cache (9) com base na política de cache configurada (consulte [Configuração de expiração do cache](https://intl.cloud.tencent.com/document/product/228/35317) e devolvê-lo ao usuário (10) para encerrar a solicitação.
