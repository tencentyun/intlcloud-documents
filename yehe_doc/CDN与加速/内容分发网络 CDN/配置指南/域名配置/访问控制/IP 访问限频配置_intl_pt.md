## Visão geral das configurações
Para controlar a fonte de acesso aos seus recursos empresariais, a funcionalidade de limite de acesso de IP no CDN pode ser usada. Ao limitar a quantidade de solicitações de acesso a um nó por segundo de um IP de cliente, você se defende contra ataques CC de alta frequência e evitar hotlinking por usuários mal-intencionados.


## Guia de configuração
### Visualização da configuração
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia **Access Control (Controle de acesso)** para exibir a seção **IP Access Limit Configuration (Configuração de limite de acesso de IP)**. Por padrão, ela fica desativada se não tiver nenhum valor definido:
![](https://main.qcloudimg.com/raw/647b73c63e867b31dfc1116fec3225b0.png)

### Ativação da configuração

Ative o botão de alternância, defina o limite e clique em **OK**.
![](https://main.qcloudimg.com/raw/15303948df14017a03ed7b5890c3673a.png)
**Descrição da configuração**

+ Depois que a configuração for habilitada, um erro 514 será retornado para solicitações que excederem o limite de QPS. Um limite de frequência baixo de acesso pode afetar o uso normal dos usuários mais ativos da sua empresa. Configure um limite de frequência adequado de acordo com suas condições empresariais e cenários de uso reais.
+ O limite de acesso de IP é eficaz contra ataques de um único IP a um único nó. Se um usuário mal-intencionado usar uma grande quantidade de IPs para atacar nós em toda a sua rede, essa funcionalidade não será mais aplicável.

### Desativação da configuração
Você pode desativar o botão de alternância para desabilitar essa funcionalidade. Quando o botão de alternância estiver desativado, essa funcionalidade não terá efeito no ambiente de produção, mesmo se houver uma configuração existente. Quando o botão de alternância estiver ativado, essa configuração entrará em vigor em toda a rede:
![](https://main.qcloudimg.com/raw/1f3c1893aed28e3845a1adaea9abf1d9.png)

> !Se o seu nome de domínio de aceleração estiver configurado para a aceleração global, a configuração de limite de acesso de IP terá efeito global. Essa configuração não faz distinção entre solicitações de regiões dentro e fora da China Continental.

## Exemplo de configuração
O limite de acesso de IP para o nome de domínio de aceleração `www.test.com` é:
![](https://main.qcloudimg.com/raw/0d78c86a122b3b58c35ca2ba8b3316b6.png)
Então, o acesso real será:
1. Um usuário com o IP de cliente `1.1.1.1` solicita o recurso `http://www.test.com/1.jpg` dez vezes em um segundo, e todas as solicitações de acesso são feitas a um servidor no nó de cache A do CDN. Serão gerados dez logs de acesso nesse servidor, nove deles excedem o limite de QPS. O código de status "514" será retornado.
2. Um usuário com o IP de cliente `2.2.2.2` solicita o recurso `http://www.test.com/1.jpg` duas vezes em um segundo, e as solicitações de acesso podem ser distribuídas para dois nós de cache do CDN para processamento devido às condições da rede. Cada nó retornará o conteúdo normalmente.

