O CLB oferece suporte a três versões de IP: IPv4, IPv6 e IPv6 NAT64. O CLB IPv6 oferece suporte aos protocolos TCP, UDP, TCP SSL, HTTP e HTTPS e fornece recursos de encaminhamento flexíveis com base em nomes de domínio e caminhos de URL. Este documento visa orientá-lo sobre como começar a usar o CLB IPv6.
>?O CLB IPv6 está atualmente em teste beta. Se quiser usá-lo, [envie um tíquete](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1) para solicitar.

## Pré-requisitos
1. O CLB apenas encaminha o tráfego e não pode processar solicitações; portanto, é preciso criar uma instância do CVM que processe as solicitações do usuário primeiro e conclua a configuração do IPv6. 
2. Este documento usa o encaminhamento de HTTP como exemplo. O servidor da web correspondente (como Apache, Nginx ou IIS) deve ser implementado na instância do CVM e a porta usada pelo servidor precisa escutar no IPv6.

## Instruções
- Atualmente, as instâncias do CLB IPv6 podem ser criadas nas regiões de Guangzhou, Xangai, Nanjing, Pequim, Chengdu, Hong Kong (China), Cingapura e Virgínia.
- O CLB IPv6 não é compatível com o CLB da rede clássica.
- O CLB IPv6 oferece suporte à obtenção do endereço de origem IPv6 do cliente, que pode ser obtido diretamente pelo CLB IPv6 da camada 4 ou por meio do cabeçalho `X-Forwarded-For` do CLB IPv6 do HTTP da camada 7.
- Atualmente, o CLB IPv6 equilibra a carga inteiramente na rede pública. Os clientes no mesmo VPC não podem acessar o CLB IPv6 pela rede privada.
- As implementações do IPv6 ainda estão em estágio preliminar na Internet. Em caso de falha de acesso, [envie um tíquete](https://console.cloud.tencent.com/workorder/category). O SLA não é garantido durante o período de teste beta.

## Etapa 1. Crie uma instância do CVM e configure o IPv6
1. Acesse o [Console do CVM](https://console.cloud.tencent.com/cvm/instance/index?rid=1), faça login na instância do CVM e conclua a configuração IPv6 básica.
2. Na instância do CVM, execute os seguintes comandos em sequência para implementar e reiniciar o serviço Nginx.
```
yum install nginx
service nginx restart
```
3. <span id="check" />Verifique se o serviço Nginx implementado na instância do CVM está escutando no IPv6.
 1. Execute o seguinte comando para verificação.
```
netstat -tupln
```
![](https://main.qcloudimg.com/raw/5bbe14c9e654b5a451828fa1e4157ac8.png)
 2. Execute o seguinte comando para abrir o arquivo de configuração Nginx para verificação.
```
vim  /etc/nginx/nginx.conf
```
![](https://main.qcloudimg.com/raw/ff7718571c02a45f02646ab330c21ee2.png)

## Etapa 2. Crie uma instância do CLB IPv6
1. Faça login no site oficial do Tencent Cloud e acesse a [página de aquisição do CLB](https://buy.cloud.tencent.com/lb).
2. Selecione as opções para os seguintes parâmetros corretamente:
 - Billing Mode (Modo de faturamento): apenas o faturamento pay-as-you-go (com pagamento conforme o uso) é aceito.
 - Region (Região): selecione uma região.
 - IP Version (Versão do IP): IPv6.
 - ISP Type (Tipo de ISP): BGP.
 - Network (Rede): selecione um VPC e uma sub-rede que já tenham obtido o CIDR IPv6.
3. Selecione os respectivos itens de configuração na página de aquisição e clique em **Buy Now (Comprar agora)**.
4. Na página "CLB Instance List (Lista de instâncias do CLB)", selecione a região correspondente para visualizar a instância recém-criada.
![](https://main.qcloudimg.com/raw/f53a0d3da88b82071960522de6c2fdb8.png)

## Etapa 3. Crie um listener do CLB IPv6
### Configuração do protocolo e da porta do listener HTTP
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2. Na "CLB Instance List (Lista de instâncias do CLB)", encontre a instância do CLB criada e clique na respectiva ID para entrar na página de detalhes.
3. No módulo "Basic Information (Informações básicas)", você pode clicar no ícone de modificação ao lado do nome da instância para renomeá-la.
4. Em **HTTP/HTTPS Listeners (Listeners HTTP/HTTPS)** em "Listener Management" (Gerenciamento de listener), clique em **Create (Criar)** para criar um listener do CLB.
![](https://main.qcloudimg.com/raw/301fbda84ff54f2026f79cf7063d3413.png)
5. Na caixa pop-up, configure o seguinte:
 - Defina o nome como "IPv6test", por exemplo.
 - Defina o protocolo do listener e a porta como `HTTP:80`.
6. Clique em **Submit (Enviar)** para criar o listener do CLB.

### Configuração da regra de encaminhamento do listener
1. Em "Listener Management (Gerenciamento de listener)", selecione o novo IPv6test do listener e clique em **+** para adicionar uma regra.
2. Na caixa pop-up, configure o nome do domínio, o caminho do URL, o método de balanceamento e clique em **Next (Avançar)**.
  - Nome de domínio: o nome de domínio usado por seu servidor de back-end, que pode conter um curinga. Neste exemplo, é usado `www.qcloudipv6test.com`. Para obter mais informações, consulte [Regras de URL e encaminhamento de nome de domínio da camada 7](https://intl.cloud.tencent.com/document/product/214/9032).
  - Caminho do URL: caminho de acesso do seu servidor de back-end. `/` é usado neste exemplo.
  - Selecione "WRR" para o modo de balanceamento de carga.
![](https://main.qcloudimg.com/raw/9061484f81b8a09bf194b8e0935d28b9.png)
3. Configurar a verificação de integridade: ative a verificação de integridade, verifique o encaminhamento de nome de domínio padrão e o caminho usado pelo nome de domínio e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/f55355ac26ed08260c631d4e665efbd6.png)
4. Configurar a persistência da sessão: habilite a persistência da sessão, configure o período de persistência e clique em **Submit (Enviar)**.
![](https://main.qcloudimg.com/raw/e5f710e4dd821a06ef4a6f3d77e0370f.png)

Para obter mais informações sobre listeners do CLB, consulte [Visão geral do listener do CLB](https://intl.cloud.tencent.com/document/product/214/6151).
>?
> - Um listener (ou seja, protocolo de escuta:porta) pode ser configurado com vários nomes de domínio e um nome de domínio pode ser configurado com vários caminhos de URL. Selecione um listener ou nome de domínio e clique em **+** para criar uma nova regra.
> - Persistência da sessão: se a persistência da sessão for desativada e um método round-robin for usado para programação, as solicitações serão atribuídas a diferentes servidores de back-end em sequência; se a persistência da sessão estiver ativada, ou desativada, mas a programação ip_hash for usada, as solicitações sempre serão atribuídas ao mesmo servidor de back-end.

### Vinculação da instância do CVM
>?Antes de vincular o listener a uma instância do CVM, verifique se ela obteve um endereço IPv6.

1. Na página "Listener Management (Gerenciamento de listener)", selecione e expanda o listener recém-criado e selecione o nome de domínio e o caminho do URL, e as informações IPv6 da instância do CVM associada ao caminho do URL serão exibidas à direita. Clique em **Bind (Vincular)**.
2. Na caixa pop-up, selecione a instância do CVM, defina a porta de serviço Nginx padrão para 80, defina o peso (10 por padrão) e clique em **OK**.
![](https://main.qcloudimg.com/raw/463dfdd5c8bb6772374597673614f2d9.png)
3. Depois que a instância do CVM for vinculada com sucesso, execute o seguinte:
 - Verifique se o status da porta está "íntegro"; e em caso afirmativo, prossiga para a [Etapa 4. Teste CLB IPv6](#.E6.AD.A5.E9.AA.A44.EF.BC.9A.E6.B5.8B.E8.AF.95-ipv6-.E8.B4.9F.E8.BD.BD.E5.9D.87.E8.A1.A1).
 ![](https://main.qcloudimg.com/raw/1e3fe96b91748271b04f191e7be5a7a6.png)
 - Se o status da porta for "excepcional", verifique se o listener está vinculado à porta de serviço Nginx correta da instância do CVM e faça login na instância do CVM para verificar se a porta está escutando normalmente no IPv6. É possível realizar a verificação conforme as instruções na [subetapa 3 na etapa 1](#check) para realizar a verificação. 
![](https://main.qcloudimg.com/raw/c28a8b4fc331127b8fc5fcc1294f0df9.png)

## Etapa 4. Teste CLB IPv6
Depois de configurar uma instância do CLB IPv6, você pode conferir se a arquitetura entra em vigor verificando se diferentes nomes de domínio e URLs na instância do CLB podem acessar diferentes servidores de back-end, ou seja, verificando se o recurso de roteamento baseado em conteúdo está disponível.

Use um cliente com recursos de acesso à rede pública IPv6 para acessar o nome de domínio ou endereço IPv6 da instância do CLB. Se ele conseguir acessar o serviço web da instância do CVM adequadamente, a instância do CLB IPv6 está funcionando normalmente.
