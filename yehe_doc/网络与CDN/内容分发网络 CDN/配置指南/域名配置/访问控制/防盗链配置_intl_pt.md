## Visão geral das configurações
Para controlar a fonte de acesso aos seus recursos empresariais, é possível usar a funcionalidade de proteção de hotlink referencial no CDN do Tencent Cloud.

Ao configurar uma política de controle de acesso no valor do campo de referencial no cabeçalho da solicitação HTTP, é possível controlar a fonte de acesso para evitar hotlinking por usuários mal-intencionados.


## Guia de configuração
### Visualização da configuração
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia **Access Control (Controle de acesso)** para exibir a seção **Hotlink Protection Configuration (Configuração da proteção de hotlink)**. Por padrão, ela fica desativada.
![](https://main.qcloudimg.com/raw/53cfa056e5574aae9c912db36fcbf67b.png)

### Ativação da configuração

Ative o botão de alternância, selecione um tipo de proteção de hotlink, marque **Allow blank referer (Permitir referencial em branco)** conforme necessário, insira um IP ou nome de domínio na caixa de entrada e clique em **OK**.
![](https://main.qcloudimg.com/raw/951eb25d77110a01fcd91ab9bfcd1cad.png)
**Lista de bloqueio de referencial**:

- Se o campo de referencial de uma solicitação corresponder à string configurada na lista de bloqueio, o nó do CDN não retornará as informações solicitadas e um código de status 403 será retornado.
- Se o campo de referencial de uma solicitação não corresponder à string configurada na lista de bloqueio, o nó do CDN retornará as informações solicitadas.
- Se **Allow blank referer (Permitir referencial em branco)** estiver marcado, o nó do CDN não retornará as informações solicitadas e um código de status 403 será retornado se o campo de referencial estiver vazio ou não existir em uma solicitação (como uma solicitação de navegador).

**Lista de permissões de referencial**:
- Se o campo de referencial de uma solicitação corresponder à string configurada na lista de permissões, o nó do CDN retornará as informações solicitadas.
- Se o campo de referencial de uma solicitação não corresponder à string configurada na lista de permissões, o nó do CDN não retornará as informações solicitadas e um código de status 403 será retornado.
- Depois que a lista de permissões for configurada, o nó do CDN só poderá retornar solicitações que correspondam à string configurada na lista de permissões.
- Se **Allow blank referer (Permitir referencial em branco)** estiver marcado, o nó do CDN retornará as informações solicitadas se o campo de referencial estiver vazio ou não existir em uma solicitação (como uma solicitação de navegador).

**Limitações de configuração**:
+ A proteção de hotlink aceita regras de nome de domínio/IP (se uma regra de IP for usada, a correspondência de prefixo estará disponível; se uma regra de nome de domínio for usada, a correspondência de prefixo não será aceita). Por exemplo, se `www.abc.com` estiver configurado, então `www.abc.com/123` será correspondido, mas `www.abc.com.cn` não; se `127.0.0.1` estiver configurado, então `127.0.0.1/123` será correspondido.
+ A proteção de hotlink aceita a correspondência de curinga, por exemplo, se `*.qq.com` estiver configurado, então `www.qq.com` e `a.qq.com` serão correspondidos.

### Desativação da configuração
Você pode desativar o botão de alternância para desabilitar essa funcionalidade. Quando o botão de alternância estiver desativado, essa funcionalidade não terá efeito no ambiente de produção, mesmo se houver uma configuração existente. Se você ativar o botão de alternância, a configuração entrará em vigor em toda a rede após a confirmação da ação.
![](https://main.qcloudimg.com/raw/0eff7fac96363892b1b95f53fbadf47d.png)

### Configuração específica da região
Se o seu nome de domínio de aceleração estiver configurado para a aceleração global e você quiser configurar a aceleração dentro e fora da China Continental com configurações diferentes de proteção de hotlink de referencial, você pode clicar em **Add Special Configuration (Adicionar configuração especial)**.
![](https://main.qcloudimg.com/raw/31d414d5adf37f8a2deadce688962645.png)

> !Atualmente, os itens de configuração específicos da região não podem ser excluídos depois de adicionados, mas podem ser desativados.

## Exemplo de configuração

Se a configuração da proteção de hotlink do nome de domínio de aceleração `www.test.com` for a seguinte:
![](https://main.qcloudimg.com/raw/027832bf7f5df50370257cce662105d8.png)
Então, o acesso real será:

1. Se um usuário na China Continental iniciar uma solicitação com o campo de referencial sendo `1.1.1.1`, que corresponde à lista de permissões configurada para a China Continental, o conteúdo solicitado será retornado diretamente.
2. Se um usuário fora da China Continental iniciar uma solicitação com um referencial em branco, que corresponda à lista de bloqueio configurada para regiões fora da China Continental, um código de status 403 será retornado.

