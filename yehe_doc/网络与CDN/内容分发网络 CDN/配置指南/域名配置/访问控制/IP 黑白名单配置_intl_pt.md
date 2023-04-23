## Visão geral das configurações
Para controlar a fonte de acesso aos seus recursos empresariais, é possível usar a funcionalidade de lista de bloqueio/permissões de IP no CDN do Tencent Cloud.

Ao configurar uma política de controle de acesso em IPs de solicitações de usuários, é possível controlar efetivamente a fonte de acesso, evitando hotlinking por IPs mal-intencionados, ataques, etc.

## Guia de configuração

### Visualização da configuração
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia **Access Control (Controle de acesso)** para exibir a seção **IP Blocklist/Allowlist Configuration (Configuração de lista de bloqueio/permissões de IP)**. Por padrão, ela fica desativada.
![](https://main.qcloudimg.com/raw/f151317bd14f053a125bf0c3841da033.png)

### Ativação da configuração

Ative o botão de alternância, marque **Blocklist (Lista de bloqueio)** ou **Allowlist (Lista de permissões)**, insira a lista de IPs ou os intervalos de IP e clique em **OK**:
![](https://main.qcloudimg.com/raw/0b278589542a7022b3525f80ecadd2e3.png)
**Lista de bloqueio de IP**
Se um IP de cliente corresponder a um IP ou intervalo de IP na lista de bloqueio, o nó do CDN acessado retornará código de status 514 imediatamente.
**Lista de permissões de IP**
Se um IP de cliente não corresponder a nenhum IP ou intervalo de IP na lista de permissões, o nó do CDN acessado retornará diretamente um código de status 514.
**Limitações de configuração**

- A lista de bloqueio e a lista de permissões de IP são mutuamente exclusivas e não podem ser configuradas ao mesmo tempo.
- Até 200 entradas podem ser adicionadas à lista de bloqueio e à lista de permissões, respectivamente.
- Apenas os intervalos de IP `/8`, `/16` e `/24` são aceitos.
- O formato `IP:Port` não é compatível.

### Desativação da configuração
Você pode desativar o botão de alternância para desabilitar essa funcionalidade. Quando o botão de alternância estiver desativado, essa funcionalidade não terá efeito no ambiente de produção, mesmo se houver uma configuração existente. Se você ativar o botão de alternância, a configuração entrará em vigor em toda a rede após a confirmação da ação.
![](https://main.qcloudimg.com/raw/24a3de16131fd945c05307493eb768f0.png)

>!Se o seu nome de domínio de aceleração estiver configurado para a aceleração global, a lista de bloqueio/permissões de IP terá efeito global. Essa configuração não faz distinção entre solicitações de regiões dentro e fora da China Continental.

## Exemplo de configuração

Se a configuração da lista de bloqueio/permissões de IP do nome de domínio `www.test.com` for a seguinte:
![](https://main.qcloudimg.com/raw/29a9307902d03f686345eef2964c5ec2.png)
Então, o acesso real será:
1. Um usuário com o IP de cliente `1.1.1.1` acessa o recurso `http://www.test.com/test.txt`. Quando o IP corresponder a um IP na lista de permissões, o conteúdo solicitado será retornado.
2. Um usuário com o IP de cliente `2.1.1.1` acessa o recurso `http://www.test.com/test.txt`. Como o IP não corresponde a nenhum IP na lista de permissões, um código de status 514 será retornado.

