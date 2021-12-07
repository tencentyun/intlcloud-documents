Ao vincular nomes de domínio com listeners do CLB, o [Web Application Firewall (WAF) do CLB](https://intl.cloud.tencent.com/document/product/627/17470) pode detectar e bloquear o tráfego HTTP ou HTTPS que passa pelos listeners do CLB. Este documento mostra como usar o WAF do CLB para aplicar a proteção de segurança da web para os nomes de domínio adicionados ao CLB.

## Pré-requisitos
- Atualmente, o WAF do CLB está na versão beta. Para testá-lo, envie uma requisição.
- Você criou com êxito um listener HTTP ou HTTPS e o nome de domínio pode ser acessado. Para obter mais informações, consulte [Introdução ao CLB](https://intl.cloud.tencent.com/document/product/214/8975).
- Você adquiriu com êxito o serviço WAF do CLB. Para obter mais informações, consulte o [Guia de compra](https://intl.cloud.tencent.com/document/product/627/11730).

## Limites
Atualmente, apenas as instâncias do CLB IPv4 são compatíveis com a proteção WAF para o CLB, este recurso não está disponível para IPv6 e NAT64.

## Instruções
<span id ="step1"></span>
### Etapa 1: Confirme a configuração do nome de domínio do CLB
Este documento usa o nome de domínio `www.example.com` como exemplo.
1. Faça login no [console do CLB](https://console.cloud.tencent.com/clb), clique em **CLB Instance List (Lista de instâncias do CLB)** na barra lateral esquerda para entrar na página **Instance Management (Gerenciamento de instâncias)**.
2. Selecione a região da instância e clique em **Configure Listener (Configurar listener)** à direita da instância de destino.
3. Selecione a guia **Listener Management (Gerenciamento de listener)**, na seção **HTTP/HTTPS Listener (Listener HTTP/HTTPS)**, clique no ícone **+** à esquerda do listener de destino para ver os detalhes do nome de domínio.
![](https://main.qcloudimg.com/raw/1d546d69bc1d88faf15ef7acc9270468.png)
4. Verifique a configuração do nome de domínio do CLB para corresponder ao seguinte: ID da instância do CLB: `lb-f8lm****`; nome do listener: `http-test`; nome do domínio: `www.example.com`; status de proteção do nome de domínio: **Not Enabled (Não habilitado)** (o ID, o nome e o nome de domínio estão sujeitos aos casos reais).

### Etapa 2: Adicione um nome de domínio no console do WAF e vincule-o a uma instância do CLB
Para aplicar proteção a um nome de domínio com o serviço de WAF do CLB, você precisa adicionar um nome de domínio de escuta do CLB no WAF e vinculá-lo a um listener do CLB.
1. Faça login no [Console do WAF](https://console.cloud.tencent.com/guanjia/waf/config), e selecione **Web Application Firewall** -> **Defense Settings (Configurações de defesa)** na barra lateral à esquerda.
2. Selecione a guia **CLB**.
3. Clique em **Add Domains (Adicionar domínios)**.
![](https://main.qcloudimg.com/raw/5dc4d9c0363a2fe2713f157606efce19.png)
4. Digite o nome do domínio e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/fadb7336503e5ee808fe8a02d9b12005.png)
5. Selecione a região de seu CLB e o nome de domínio na <a href="#step1">"Etapa 1: confirme a configuração do nome de domínio do CLB"</a>, e clique em **Select a Listener (Selecionar um listener)**.
![](https://main.qcloudimg.com/raw/4b632c6769bbbe105027e8bdf0b3ba1a.png)
6. Na janela pop-up, selecione o listener do CLB na <a href="#step1">"Etapa 1: confirme a configuração do nome de domínio do CLB "</a>, e clique em **OK**.
![](https://main.qcloudimg.com/raw/2793320edb9a79b0c46e4ea4e92e38f6.png)
7. Clique em **Finish (Concluir)** na etapa **Select a Listener (Selecionar um listener)** para concluir a vinculação de um nome de domínio ao listener do CLB no WAF.
8. De volta à página **Lista de Domínios**, verifique o nome do domínio, região, ID da instância CLB vinculada, listener e outras informações.

### Etapa 3: Verificar o resultado
1. Siga as instruções na <a href="#step1">"Etapa 1: confirme a configuração do nome de domínio do CLB"</a> para conferir o nome de domínio. A proteção do nome de domínio é ativada se a proteção do nome de domínio for **Enabled (Ativada)** e o modo de tráfego for **Mirror (Espelho)**.
 - Se você não configurou a resolução DNS para seu nome de domínio, consulte [Etapa 2. Execute o teste local](https://intl.cloud.tencent.com/document/product/627/35652) para verificar se a proteção WAF está habilitada.
 - Se você tiver configurado a resolução DNS para seu nome de domínio, siga as instruções abaixo para verificar se a proteção WAF está ativada.
1. Visite `http://www.example.com/?test=alert(123)` através de um navegador.
2. Faça login no [Console do WAF](https://console.cloud.tencent.com/guanjia/waf/config), e selecione **Log Services (Serviços de log)** -> **Attack Log (Log de ataques)** na barra lateral esquerda.
3. Selecione a guia **Log Search (Busca de log)**, selecione o nome de domínio de proteção adicionado `www.example.com` e clique em **Search (Buscar)**. A proteção WAF para o nome de domínio configurado no CLB estará em vigor se houver logs de **Ataque XSS** na lista de logs.

