## Visão geral das configurações

Quando um usuário final solicita um recurso empresarial, é possível adicionar um cabeçalho personalizado na **mensagem de resposta** retornada, para implementar o compartilhamento de recursos entre origens.
O cabeçalho da resposta é configurado no nível de nomes de domínio. Assim que a configuração entrar em vigor, ela será sincronizada com a mensagem de resposta de cada recurso sob o nome de domínio. A configuração do cabeçalho de resposta faz alterações apenas na resposta do cliente (navegador), mas não no cache do nó do CDN.

## Guia de configuração

### Visualização da configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia **Advanced Configuration (Configurações avançadas)** para exibir a seção **Response Header Configuration (Configuração do cabeçalho de resposta)**. Por padrão, ela fica desativada. Você pode clicar em **Add Rule (Adicionar regra)** para adicionar regras de cabeçalho de resposta.
![img](https://main.qcloudimg.com/raw/979a6f3254776cdadd5ca4dc71d631a6.png)

### Operação

| Operação | Descrição                                                         |
| :------- | :----------------------------------------------------------- |
| Definir     | Altera o valor de um parâmetro de cabeçalho de resposta especificado.<br/>Se o cabeçalho de destino não existir, ele será adicionado após a alteração.<br/>Se o parâmetro do cabeçalho já existir, todas as duplicatas serão alteradas e mescladas em um cabeçalho. Por exemplo, após a regra "Set - `x-cdn: value1`" ser configurada, se uma solicitação contiver vários cabeçalhos `x-cdn`, os cabeçalhos serão alterados e mesclados em um cabeçalho `x-cdn: value1`. |
| Excluir     | Exclui um parâmetro de cabeçalho de resposta especificado.                                       |

> !
> - Alguns cabeçalhos não podem ser definidos ou excluídos por conta própria. Para a lista detalhada, consulte [Observações](#notice).
> - Podem ser configuradas até 10 regras de cabeçalho de resposta.
> - A prioridade da regra pode ser ajustada. As regras mais abaixo na lista têm prioridade mais alta. Se um parâmetro de cabeçalho for configurado com várias regras, a regra inferior terá efeito conforme as regras são executadas de baixo para cima.

### Parâmetro do cabeçalho

<table>
<thead>
<tr>
<th style="width:230px">Parâmetro do cabeçalho</th>
<th>Descrição</th>
</tr>
</thead>
<tbody><tr>
<td>Access-Control-Allow-Origin</td>
<td>Cabeçalho relacionado à permissão entre origens, que especifica o domínio com permissão para acessar os recursos. Até 10 domínios podem ser configurados. Se um host de solicitação de origem for configurado como um valor de parâmetro de cabeçalho, ele será preenchido no cabeçalho de resposta. Também é possível defini-lo como `*` para permitir que todos os domínios acessem os recursos. Para obter mais informações, consulte <a href="#acao">Descrição do modo de correspondência Access-Control-Allow-Origin</a>.<br>O curinga `*`, nomes de domínio e IPs são aceitos. Deve conter `http://` ou `https://`. Separe vários parâmetros com `,`, e até 66 entradas são aceitas. Por exemplo, `http://test.com,http://1.1.1.1`. </td>
</tr>
<tr>
<td>Access-Control-Allow-Methods</td>
<td>Especifica o método de solicitação HTTP entre origens e aceita vários métodos ao mesmo tempo: <br>`Access-Control-Allow-Methods: <code>POST, GET, OPTIONS`</code>.</td>
</tr>
<tr>
<td>Access-Control-Max-Age</td>
<td>Especifica o período de validade (em segundos) de uma solicitação de simulação.<br>Para uma solicitação não simples entre origens, uma solicitação de consulta HTTP, ou seja, a solicitação de simulação, é necessária antes da comunicação oficial para verificar se a solicitação entre origens é segura para ser aceita. Uma solicitação entre origens é não simples caso:<br>Não seja uma solicitação GET, HEAD ou POST, ou for uma POST, mas seu tipo de dados de solicitação é `application/xml`, `text/xml` ou qualquer outro tipo de dados, exceto `application/x-www-form-urlencoded`, `multipart/form-data` e `text/plain`.<br>Por exemplo, se um cabeçalho de solicitação personalizado for `Access-Control-Max-Age:1728000`, isso indica que não haverá outra solicitação de simulação enviada para o compartilhamento de recursos entre origens em 1.728.000 segundos (20 dias).</td>
</tr>
<tr>
<td>Access-Control-Expose-Headers</td>
<td>Especifica quais cabeçalhos podem ser expostos aos clientes como parte das respostas.<br>Por padrão, esses 6 cabeçalhos podem ser expostos aos clientes: `Cache-Control`, `Content-Language`, `Content-Type`, `Expires`, `Last-Modified` e `Pragma`.<br>Se quiser tornar outros cabeçalhos acessíveis aos clientes, você pode separar vários cabeçalhos com `,`, por exemplo, `Access-Control-Expose-Headers: Content-Length,X-My-Header`. Dessa forma, os clientes podem acessar os dois cabeçalhos `Content-Length` e `X-My-Header`.</td>
</tr>
<tr>
<td>Content-Disposition</td>
<td>Ativa o download no navegador e define o nome do arquivo padrão do recurso baixado.<br>Quando um servidor envia um arquivo para um navegador do cliente, se o tipo de arquivo for compatível com o navegador, como TXT e JPG, o arquivo será aberto diretamente no navegador por padrão. Se você quiser que o usuário salve o arquivo, pode configurar o campo `Content-Disposition` para substituir o comportamento padrão do navegador. A configuração comum é a seguinte:<br>`Content-Disposition:attachment;filename=FileName.txt`</td>
</tr>
<tr>
<td>Content-Language</td>
<td>Especifica o código do idioma usado na página. A configuração comum é a seguinte:<br>`Content-Language: zh-CN`<br>`Content-Language: en-US`</td>
</tr>
<tr>
<td>Personalizar</td>
<td>Aceita cabeçalho personalizado e configurações de par de valores-chave.<br>Requisitos para parâmetros de cabeçalho personalizados: consistir em 1 a 100 caracteres de letras maiúsculas e minúsculas, dígitos e hifens (-).<br>Requisitos para valores de cabeçalho personalizados: consistir em 1 a 1.000 caracteres; os caracteres chineses não são aceitos.</td>
</tr>
</tbody></table>

[](id:acao)
### Introdução ao modo de correspondência Access-Control-Allow-Origin

| **Modo de correspondência**   | **Valor de origem**                                                     | **Descrição**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Correspondência total         | *                                                            | Se for definido como `*`, o cabeçalho `Access-Control-Allow-Origin:*` será adicionado à resposta. |
| Correspondência fixa       | `http://cloud.tencent.com` `https://cloud.tencent.com` `http://www.b.com` | A origem `https://cloud.tencent.com` atinge a lista, então o cabeçalho `Access-Control-Allow-Origin: https://cloud.tencent.com` será adicionado à resposta. A origem `https://www.qq.com` não atinge a lista, então a resposta não mudará. |
| Correspondência de nome de domínio curinga de segundo nível | `http://*.tencent.com`                                       | A origem `https://cloud.tencent.com` atinge a lista, então o cabeçalho `Access-Control-Allow-Origin: https://cloud.tencent.com` será adicionado à resposta. A origem `https://cloud.qq.com` não atinge a lista, então a resposta não mudará. |
| Correspondência de porta       | `https://cloud.tencent.com:8080`                             | A origem `https://cloud.tencent.com:8080` atinge a lista, então o cabeçalho `Access-Control-Allow-Origin:https://cloud.tencent.com:8080` será adicionado à resposta. A origem `https://cloud.tencent.com` não atinge a lista, então a resposta não mudará. |

> ! Se houver portas especiais, será necessário inserir as informações relevantes na lista. A correspondência de porta arbitrária não é aceita e você deve especificar as portas.

[](id:notice)
### Observações

Os cabeçalhos abaixo não são aceitos e não terão efeito mesmo se configurados:

```
Date
Expires
Content-Type
Content-Encoding
Content-Length
Transfer-Encoding
Cache-Control
If-Modified-Since
Last-Modified
Connection
Content-Range
ETag
Accept-Ranges
Age
Authentication-Info
Proxy-Authenticate
Retry-After
Set-Cookie
Vary
WWW-Authenticate
Content-Location
Content-MD5
Content-Range
Meter
Allow
Error
```
