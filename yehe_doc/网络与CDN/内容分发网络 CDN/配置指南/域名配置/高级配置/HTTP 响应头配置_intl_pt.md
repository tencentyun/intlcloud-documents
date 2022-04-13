## Visão geral das configurações

Quando um usuário final solicita um recurso empresarial, é possível adicionar um cabeçalho personalizado na **mensagem de resposta** para implementar o compartilhamento de recursos entre origens.
A configuração do cabeçalho de resposta pertence à dimensão do nome de domínio, portanto, assim que a configuração entrar em vigor, ela será sincronizada com a mensagem de resposta de cada recurso sob o nome de domínio. A configuração do cabeçalho de resposta faz alterações apenas na resposta do cliente (navegador), mas não no cache do nó do CDN.

## Instruções

### Visualização da configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar a sua página de configuração. Abra a aba **Advanced configuration (Configuração avançada)** para localizar a configuração **Response Header Configuration (Configuração do cabeçalho da resposta)** que está desabilitada por padrão. Você pode clicar em **Add Rule (Adicionar regra)** para adicionar regras de cabeçalho de resposta HTTP.
![](https://main.qcloudimg.com/raw/979a6f3254776cdadd5ca4dc71d631a6.png)

### Tipo de operação

| Operação | Descrição                                                         |
| :------- | :----------------------------------------------------------- |
| Definir     | Altera o valor de um parâmetro de cabeçalho de resposta especificado.<br/>Se o cabeçalho de destino não existir, ele será adicionado após a operação de alteração.<br>Se o parâmetro do cabeçalho já existir, todas as duplicatas serão alteradas e mescladas em um cabeçalho. Por exemplo, após a regra "Set - <code>x-cdn: value1</code>" ser configurada, se uma solicitação contiver vários cabeçalhos <code>x-cdn</code>, os cabeçalhos serão alterados e mesclados em um cabeçalho <code>x-cdn: value1</code>. |
| Excluir     | Exclui um parâmetro de cabeçalho de resposta especificado.                                       |

> !
> - Alguns cabeçalhos não podem ser definidos ou excluídos por conta própria. Para a lista detalhada, consulte [Observações](#notice).
> - Podem ser configuradas até 10 regras de cabeçalho de resposta HTTP.
> - A prioridade da regra pode ser ajustada. As regras na parte inferior da lista têm prioridade mais alta. Se um parâmetro de cabeçalho for configurado com várias regras, a regra inferior entrará em vigor à medida que as regras forem executadas de baixo para cima.

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
<td>Cabeçalho de compartilhamento de recursos de origem cruzada (CORS), que especifica o domínio com permissão para acessar recursos. Se um host de solicitação de origem for configurado como um valor de parâmetro de cabeçalho, ele será preenchido no cabeçalho de resposta. Também é possível defini-lo como <code>*</code> para permitir que todos os domínios acessem os recursos. Para obter mais informações, consulte <a href="#acao">Descrição do modo de correspondência Access-Control-Allow-Origin</a>.</br>O curinga <code>*</code>, nomes de domínio e IPs são compatíveis. <code>http://</code> ou <code>https://</code> devem estar contidos. Separe mais de um com <code>,</code>, e até 1000 caracteres são aceitos. Por exemplo <code>http://test.com,http://1.1.1.1</code>.</td>
</tr>
<tr>
<td>Access-Control-Allow-Methods</td>
<td>Especifica o método de solicitação HTTP CORS e suporta vários métodos ao mesmo tempo: <br>Access-Control-Allow-Methods: <code>POST, GET, OPTIONS</code>.</td>
</tr>
<tr>
<td>Access-Control-Max-Age</td>
<td>Especifica o período de validade (em segundos) de uma solicitação de simulação.<br>Para uma solicitação CPRS não simples, uma solicitação de consulta HTTP, ou seja, a solicitação de simulação, é necessária antes da comunicação oficial para verificar se a solicitação CORS é segura para ser aceita. Uma solicitação CORS é não simples caso:<br>Não seja uma solicitação GET, HEAD, ou POST, ou seja uma solicitação POST, mas o seu tipo de dados de solicitação é <code>application/xml</code>, <code>text/xml</code> ou qualquer outro tipo de dados, exceto <code>application/x-www-form-urlencoded</code>, <code>multipart/form-data</code>, e <code>text/plain</code>.<br>Por exemplo, se um cabeçalho de solicitação personalizado for <code>Access-Control-Max-Age:1728000</code>, não haverá outra solicitação de simulação CORS enviada em 1.728.000 segundos (20 dias).</td>
</tr>
<tr>
<td>Access-Control-Expose-Headers</td>
<td>Especifica quais cabeçalhos podem ser expostos aos clientes como parte das respostas.<br>Por padrão, esses 6 cabeçalhos podem ser expostos aos clientes: <code>Cache-Control</code>, <code>Content-Language</code>, <code>Content-Type</code>, <code>Expires</code>, <code>Last-Modified</code>, e <code>Pragma</code>.<br>Se você quiser tornar outros cabeçalhos acessíveis aos clientes, você pode separar vários cabeçalhos com <code>,</code>, por exemplo, <code>Access-Control-Expose-Headers: Content-Length,X-My-Header</code>. Dessa forma, os clientes podem acessar os dois cabeçalhos <code>Content-Length</code> e <code>X-My-Header</code>.</td>
</tr>
<tr>
<td>Content-Disposition</td>
<td>Ativa o download no navegador e define o nome do arquivo padrão do recurso baixado.<br>Quando um servidor envia arquivos para um navegador de um cliente, com tipos de arquivo compatíveis com o browser, como TXT e JPG, os arquivos serão abertos diretamente no navegador por padrão. Se você quiser que o usuário salve os arquivos, pode configurar o campo <code>Content-Disposition</code> para substituir o comportamento padrão do navegador. A configuração comum é a seguinte:<br><code>Content-Disposition:attachment;filename=FileName.txt</code></td>
</tr>
<tr>
<td>Content-Language</td>
<td>Especifica o código de idioma usado na página. A configuração comum é a seguinte:<br><code>Content-Language: zh-CN</code><br><code>Content-Language: en-US</code></td>
</tr>
<tr>
<td>Custom</td>
<td>Permite cabeçalho personalizado e configurações de par de valores-chave.<br>Um parâmetro de cabeçalho personalizado suporta de 1 a 100 caracteres de letras maiúsculas e minúsculas, dígitos e hifens (-).<br>O valor do parâmetro suporta de 1 a 1000 caracteres, excluindo caracteres chineses.</td>
</tr>
</tbody></table>


### Introdução ao modo de correspondência Access-Control-Allow-Origin[](id:acao)

| **Modo de correspondência**   | **Valor de origem**                                                     | **Descrição**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Correspondência total         | *                                                            | Se for definido como `*`, o cabeçalho `Access-Control-Allow-Origin:*` será adicionado à resposta. |
| Correspondência fixa       | `http://cloud.tencent.com` `https://cloud.tencent.com` `http://www.b.com` | A origem `https://cloud.tencent.com` consta na lista, então o cabeçalho `Access-Control-Allow-Origin: https://cloud.tencent.com` será adicionado à resposta. <br/>A origem `https://www.qq.com` não acerta a lista, então a resposta não será alterada. |
| Correspondência de nome de domínio curinga de segundo nível | `https://*.tencent.com` | A origem `https://cloud.tencent.com` acerta a lista, então o cabeçalho `Access-Control-Allow-Origin: https://cloud.tencent.com` será adicionado à resposta. <br/>A origem `https://cloud.qq.com` | ``  `Access-Control-Allow-Origin: ` .  `` não acerta a lista, então a resposta não será alterada. |
|  Correspondência de portas       | `https://cloud.tencent.com:8080`                             | A origem `https://cloud.tencent.com:8080` consta na lista, então o cabeçalho `Access-Control-Allow-Origin:https://cloud.tencent.com:8080` será adicionado à resposta. <br/>A origem `https://cloud.tencent.com` não acerta a lista, então a resposta não será alterada. |

> ! Se houver portas especiais, será necessário inserir as informações relevantes na lista. Você deve especificar a porta, pois a correspondência de porta arbitrária não é permitida.

### Observações[](id:noice)

Os cabeçalhos abaixo não são aceitos e não terão efeito se configurados:

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
