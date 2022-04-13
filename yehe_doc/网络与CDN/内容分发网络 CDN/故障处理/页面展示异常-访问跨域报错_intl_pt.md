
## Descrição do erro

Um erro CORS é relatado, o que resulta em erro de página ou exibição de página excepcional. Consulte a figura abaixo:

![](https://main.qcloudimg.com/raw/af636dbb5bba454bb79234cd7b49dca2.png)

## Motivos possíveis

O erro CORS é causado pela política de mesma origem do navegador. Para a segurança da página da Web, quando a resposta para esta solicitação é bloqueada pelo navegador, o que resultará em erro de front-end ou exibição de página excepcional. Quando o protocolo, nome de domínio ou porta da URL de solicitação é diferente da URL da página solicitada, a solicitação é considerada uma solicitação entre sites.

## Soluções

1. Verifique se o problema é causado por solicitação entre sites. Consulte a figura abaixo:
![](https://main.qcloudimg.com/raw/78d05383b9040d313c05add33a1737df.png)
2. Configure o cabeçalho de resposta HTTP correspondente no console CDN e defina os domínios com permissão para acessar esse recurso.

## Procedimento de solução de problemas

1. Faça login no <a href="https://console.cloud.tencent.com/cdn/domains">Console do CDN</a>, vá para **Domain Name Management (Gerenciamento de nome de domínio)** - **Advanced Configuration (Configuração avançada)** - **HTTP Response Header (Cabeçalho de resposta HTTP)**, conclua a configuração do parâmetro **Access-Control-Allow-Origin** conforme abaixo para permitir solicitações entre sites de todos os domínios. Para obter mais informações, consulte [Descrição do modo de correspondência Access-Control-Allow-Origin](#ac).

2. Você também pode configurar para permitir solicitações entre regiões de um único ou vários nomes de domínio/IPs especificados.
Você também pode configurar parâmetros de cabeçalho, como Access-Control-Request-Method, Access-Control-Request-Headers e Access-Control-Max-Age para especificar os métodos e cabeçalhos de solicitação permitidos e por quanto tempo os resultados de uma solicitação de comprovação podem ser armazenado em cache. Para obter mais informações, consulte [Lista de parâmetros compatíveis](#ap).


>! Se você configurou o acesso entre regiões no bucket COS, configure as regras entre regiões no <a href="https://intl.cloud.tencent.com/document/product/228/35320">Cabeçalho de resposta HTTP<a href="https://intl.cloud.tencent.com/document/product/228/35320"> no console CDN.

[](id:ap)
### Lista de parâmetros compatíveis

| Parâmetro de cabeçalho                      | Descrição |
| :---------------------------- | :----------------------------------------------------------- |
| Access-Control-Allow-Origin   | Especifica quais origens têm permissão para acessar o recurso. Para solicitações das origens permitidas, o host é adicionado ao cabeçalho da solicitação. Você também pode configurá-lo para `*`, permitindo solicitações de todas as origens. Para obter mais informações, consulte [Descrição do modo de correspondência Access-Control-Allow-Origin]|(#ac). Você pode inserir nomes de domínio, IPs e ambos. Observe que `http://` ou `https://` devem ser incluídos (por exemplo, `http://test.com`, `http://1.1.1.1`). Separe várias entradas com vírgulas, até 1.000 caracteres são permitidos.|
| Access-Control-Allow-Methods  | Indica os métodos HTTP permitidos para solicitações de origem cruzada. Você pode configurar um ou mais métodos, conforme mostrado abaixo: Access-Control-Allow-Methods: `POST, GET, OPTIONS`. |
| Access-Control-Max-Age        | Especifica o período de validade (em segundos) de uma solicitação de simulação. Para uma solicitação de origem cruzada não simples, uma solicitação de consulta HTTP, ou seja, a solicitação de simulação, é necessária antes da comunicação oficial para verificar se a solicitação de origem cruzada pode ser aceita com segurança. Uma solicitação de origem cruzada não é simples se: não for uma solicitação GET, HEAD ou POST, ou for uma solicitação POST, mas seu tipo de dados de solicitação for application/xml, text/xml ou qualquer outro tipo de dados exceto application/x-www-form-urlencoded, multipart/form-data e text/plain. Por exemplo, se um cabeçalho de solicitação personalizado for Access-Control-Max-Age:`1728000`, não haverá outra solicitação de simulação enviada para este CORS em 1.728.000 segundos (20 dias). |
| Access-Control-Expose-Headers | Isso especifica quais cabeçalhos podem ser expostos aos clientes como parte das respostas. Por padrão, esses 6 cabeçalhos podem ser expostos aos clientes: Cache-Control, Content-Language, Content-Type, Expires, Last-Modified e Pragma. Se você quiser tornar outros cabeçalhos acessíveis aos clientes, você pode separar vários cabeçalhos com uma vírgula, por exemplo, Access-Control-Expose-Headers:
 Content-Length, X-My-Header. Dessa forma, os clientes podem acessar os dois cabeçalhos `Content-Length` e `X-My-Header`.|

[](id:q1)
### Access-Control-Allow-Origin Configuration

| **Modo** | **Valor/Exemplo**                                                     | **Descrição**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Permitir todos         | `*`                                                            | Quando estiver definido como `*`, o cabeçalho `Access-Control-Allow-Origin:*` será adicionado à resposta, o que significa permitir solicitações de todas as origens. |
| Domínio especificado      | `http://cloud.tencent.com` `https://cloud.tencent.com` `http://www.b.com` | Quando uma solicitação é iniciada de `https://cloud.tencent.com`, que acerta a regra, o cabeçalho `Access-Control-Allow-Origin: https://cloud.tencent.com` é adicionado à resposta. Porém, quando há uma requisição de `https://www.qq.com`, que não acerta a regra, a resposta não é alterada. |
| Nome de domínio de segundo nível especificado | `https://*.tencent.com`                                       | Quando uma solicitação é iniciada de `https://cloud.tencent.com`, que acerta a regra, o cabeçalho `Access-Control-Allow-Origin: https://cloud.tencent.com` é adicionado à resposta. Porém, quando há uma requisição de `https://cloud.qq.com`, que não acerta a regra, a resposta não é alterada. |
| Porta especificada       | `https://cloud.tencent.com:8080`                             | Quando uma solicitação é iniciada de `https://cloud.tencent.com:8080`, que acerta a regra, o cabeçalho `Access-Control-Allow-Origin:https://cloud.tencent.com:8080` é adicionado à resposta. Porém, quando há uma solicitação de `https://cloud.tencent.com`, que não acerta a regra, a resposta não é alterada. |

> ! Se houver portas especiais, será necessário inserir as informações relevantes na lista. Você deve especificar a porta, pois a correspondência de porta arbitrária não é suportada.
