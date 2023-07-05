## Descrição do problema

O acesso aos sites está lento.

## Análise do problema

Uma solicitação HTTP completa inclui resolver o nome de domínio, estabelecer a conexão TCP, iniciar a solicitação, o CVM receber e processar a solicitação, retornar o resultado, o navegador analisar o código HTML, solicitar outros recursos e renderizar a página. Esses processos envolvem o cliente local, os nós de rede entre o cliente e o servidor, e o servidor. Um problema com qualquer um deles pode causar latência de acesso à rede.

## Soluções

### Verifique o cliente local
1. Acesse o [site de teste de rede](https://ping.huatuo.qq.com) para testar a velocidade de acesso a diferentes nomes de domínio do cliente local.
2. Com base no resultado do teste, verifique se a rede local apresenta algum erro.
Veja como exemplo um resultado de teste mostrado abaixo:
![](https://main.qcloudimg.com/raw/1dfe4866d4572d82841225b60d127a1c.png)
O resultado do teste mostra a latência de acesso para cada nome de domínio e se a rede está normal.
 - Se a rede apresente algum erro, entre em contato com seu ISP para localizar e resolver o problema.
 - Se a rede estiver normal, [verifique a ligação da rede](#CheckNetworkLink).

<span id="CheckNetworkLink"></span>
### Verifique a ligação da rede

1. Execute ping no IP público do servidor do cliente local para verificar se há perda de pacotes ou alta latência.
 - Se algum dos problemas ocorrer, use o MTR para solucionar o problema. Para mais informações, consulte [Latência da rede e perda de pacotes do CVM](https://intl.cloud.tencent.com/document/product/213/14638).
 - Se o teste de ping não mostrar perda de pacotes ou alta latência, realize a [Etapa 2](#CheckNetworkLink_step2).
2. <span id="CheckNetworkLink_step2">Use o comando `dig/nslookup` para verificar se o problema é causado pela resolução do DNS. </span>
Você também pode acessar a página diretamente com o IP da rede pública para verificar se o DNS causou latência de acesso.
- Se o DNS apresentar algum erro, verifique a resolução do DNS.
- Se o DNS estiver normal, [verifique o servidor](#CheckServer).
<span id="CheckServer"></span>
### Verifique o servidor

1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Clique no ID/nome da instância que você deseja verificar para acessar a sua página de detalhes.
3. Selecione a guia **Monitoring (Monitoramento)** na página de detalhes para exibir o uso de recursos da instância, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/b8396a4507dd6a9808f9907b90e881fa.png)
 - Se o uso de CPU/memória for muito alto, consulte [Falha ao fazer login em um CVM do Windows devido ao alto uso de CPU e memória](https://intl.cloud.tencent.com/document/product/213/32405) e [Falha ao fazer login em um CVM do Linux devido ao alto uso de CPU e memória](https://intl.cloud.tencent.com/document/product/213/32387) para solucionar o problema.
 - Se o uso da largura de banda for muito alto, consulte [Falha ao fazer login devido à alta ocupação da largura de banda](https://intl.cloud.tencent.com/document/product/213/32542) para solucionar o problema. 
 - Se o uso de recursos da instância for normal, [verifique outros problemas](#CheckOtherProblems).

<span id="CheckOtherProblems"></span>
### Verifique outros problemas

Com base no uso de recursos da instância, verifique se o aumento no consumo de recursos é causado pela carga do servidor.
 - Se for, recomendamos que você otimize os processos da empresa, [altere a configuração da instância](https://intl.cloud.tencent.com/document/product/213/2178) ou adquira novos servidores para reduzir a pressão sobre os servidores atuais.
 - Se não for, recomendamos que você verifique os arquivos de log para localizar o problema e realizar a otimização direcionada.

