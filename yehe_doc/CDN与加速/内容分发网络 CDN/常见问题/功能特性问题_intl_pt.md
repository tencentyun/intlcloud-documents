[](id:q1)
### O CDN do Tencent Cloud aceita a aceleração global?
Sim. A Tencent tem criado nós há mais de uma década. O CDN do Tencent Cloud fornece mais de 8,00 nós no exterior em mais de 70 países e regiões para ajudar na globalização da sua empresa.

[](id:q2)
### Depois de conectar ao CDN, é necessário fazer alterações no servidor de origem para que o serviço de aceleração entre em vigor?
Não. No entanto, para obter um melhor resultado de aceleração, é recomendável atribuir arquivos estáticos e dinâmicos a nomes de domínio diferentes e apenas acelerar os recursos estáticos.

[](id:q3)
### O CDN do Tencent Cloud permite o acesso entre regiões?
Sim. Se o acesso entre regiões for necessário para o seu site, basta configurar o campo `Access-Control-Allow-Origin` no site ou configurar cabeçalhos entre regiões para seu nome de domínio no console do CDN. Para obter mais informações, consulte [Cabeçalho de resposta HTTP](https://intl.cloud.tencent.com/document/product/228/35320).

[](id:q4)
### Onde eu posso baixar os logs de acesso do CDN?
Você pode baixar os logs de acesso no console do CDN. Para obter instruções detalhadas, consulte [Download de log](https://intl.cloud.tencent.com/document/product/228/6316).

[](id:q5)
### Como eu utilizo a ferramenta de autodiagnóstico do CDN?
A ferramenta de autodiagnóstico fornece uma variedade de funcionalidades de diagnóstico, como teste de resolução de DNS, qualidade de vinculação, disponibilidade de site e consistência de acesso a dados para o nome de domínio acessado. Para obter mais informações, consulte [Ferramenta de autodiagnóstico](https://intl.cloud.tencent.com/document/product/228/6304). A ferramenta está sujeita à configuração do ambiente de rede local e não pode representar totalmente os resultados do teste da rede inteira.

[](id:q6)
### Qual é a diferença entre o diagnóstico de acesso local e o diagnóstico de acesso do usuário?
Diagnóstico de acesso local: ao encontrar uma exceção em um de seus acessos aos recursos, é possível iniciar um teste com "local access diagnosis (diagnóstico de acesso local)".
Diagnóstico de acesso do usuário: quando seus usuários relatam uma exceção com seus acessos aos recursos, é possível identificar o problema por meio do "user access diagnosis (diagnóstico de acesso do usuário)" e solucionar o problema de acordo com as sugestões do Tencent Cloud.

[](id:q7)
### O CDN é compatível com solicitações POST?
Sim.

[](id:q8)
### O CDN aceita a configuração de Cache-Control do servidor de origem?
Sim. Por padrão, o CDN aceita a configuração de Cache-Control do servidor de origem.

[](id:q9)
### O CDN aceita a compactação gzip?
Sim. Para ajudar você a economizar tráfego, o CDN compacta arquivos entre 256 bytes e 2.048 KB com extensões de nome de arquivo .js, .html, .css, .xml, .json, .shtml e .htm em arquivos gzip.

[](id:q10)
### A aceleração do CDN aceita outras portas além da 80?
Sim. A aceleração do CDN aceita as portas 80, 443 e 8080.

[](id:q11)
### O que é um servidor intermediário do CDN?
Um servidor intermediário do CDN é um servidor de pull de origem, de camada intermediária, localizado entre o servidor de negócios e o nó do CDN. O servidor intermediário converge as solicitações de pull de origem do nó para reduzir a pressão de pull de origem em seu servidor de origem.

[](id:q12)
### Como eu obtenho o IP real do cliente?
Depois que uma solicitação passa por um servidor de borda, um cabeçalho `x-forward-for` que inclui as informações de IP reais do cliente será adicionado à solicitação.

[](id:q13)
### Como eu configuro subusuários do CDN?
Os subusuários não precisam se registrar no Tencent Cloud nem ativar o serviço do CDN. Eles são adicionados à lista de subusuários pelo criador. Existem dois tipos de subusuários:
1. Destinatários de mensagens.
2. Usuários do console. Para obter mais informações sobre como criar e configurar um subusuário, consulte [Permissões do console](https://intl.cloud.tencent.com/document/product/228/35229).

[](id:q14)
### Como eu configuro uma lista de bloqueio/permissões de IP no CDN?
O CDN permite a configuração de lista de bloqueio/permissões de IP. É possível criar políticas de filtragem para IPs de origem de solicitações de usuários com base em suas necessidades empresariais, ajudando a evitar hotlinking e ataques de IPs mal-intencionados. Para obter mais informações, consulte [Configuração da lista de bloqueio/permissões de IP](https://intl.cloud.tencent.com/document/product/228/6298).

Para obter mais informações sobre essa configuração, consulte [Configuração de limite de acesso de IP](https://intl.cloud.tencent.com/document/product/228/6420) e [Configuração da proteção de hotlink](https://intl.cloud.tencent.com/document/product/228/6292).

[](id:q15)
### Como eu configuro Range GETs no CDN?
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita do nome de domínio que deseja editar. Para obter mais informações, consulte [Configuração de Range GETs](https://intl.cloud.tencent.com/document/product/228/7184). 
![](https://main.qcloudimg.com/raw/af642b65bed86a97fadaf229e26aceac.png)
Clique em **Origin Configuration (Configuração da origem)** e você verá o módulo "Range GETs Configuration (Configuração de Range GETs)". ![](https://main.qcloudimg.com/raw/79d08718f1399b735b9b2dc804bf383e.png)

[](id:q16)
### Por que o CDN não consegue ocultar um IP completamente?
1. O IP já estava exposto antes de o CDN ser usado.
2. O IP ainda pode ser percebido por meios técnicos mesmo após o CDN ser usado.
3. Existem vários sites no servidor e, se outros nomes de domínio não estiverem conectados ao CDN, o IP pode ser exposto.

[](id:q17)
### O que um servidor de origem de backup dinâmico faz?
Se o seu servidor de origem principal for externo, é possível adicionar um servidor de origem de backup dinâmico. Todas as solicitações de pull de origem serão encaminhadas primeiro ao servidor de origem principal. Se um código de erro 4XX ou 5XX for retornado ou uma exceção como tempo limite de conexão ou incompatibilidade de protocolo ocorrer, as solicitações serão encaminhadas ao servidor de origem de backup dinâmico para efetuar pull de recursos, garantindo a alta disponibilidade de pull de origem.

[](id:q18)
### O CDN aceita nomes de domínio .top?
Sim. O CDN já aceita nomes de domínio com sufixo .pw ou .top.

[](id:q19)
### Existe um limite de tamanho para um arquivo carregado no CDN?
Sim. Por padrão, o tamanho máximo de um arquivo que pode ser carregado no CDN é 32 MB.

[](id:q20)
### O CDN aceita nomes de domínio com caracteres chineses?
Não. Atualmente, o CDN não aceita nomes de domínio com caracteres chineses (mesmo após a transcodificação).

[](id:q21)
### O CDN pode encaminhar solicitações ao servidor de origem pela rede privada?
Não. Atualmente, o CDN só pode encaminhar solicitações ao servidor de origem pela rede pública.

[](id:q22)
### O CDN aceita scripts de borda para implementar a configuração programável?
Sim. Atualmente, o CDN usa scripts Lua para implementar a configuração programável, que costumam ser usados para a personalização e escritos e lançados pela equipe de suporte técnico do CDN.

[](id:q23)
### O CDN aceita a configuração de servidores de origem diferentes para solicitações diferentes de clientes?
Sim. O pull de origem baseado em região do IP do cliente está em beta. Fique atento ao lançamento oficial.

[](id:q24)
### O CDN aceita a configuração de pull de origem dinâmico e o enfileiramento de pull de origem?
Se o servidor de origem principal responder excepcionalmente, ele pode redirecionar as solicitações para o servidor de origem de backup configurado em sequência para solicitar novamente.
