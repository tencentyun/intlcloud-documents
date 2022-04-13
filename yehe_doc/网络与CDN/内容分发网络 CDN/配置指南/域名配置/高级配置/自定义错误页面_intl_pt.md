## Visão geral da funcionalidade

É possível configurar a página de erro personalizada e redirecionar as solicitações com o código de status especificado para o URL especificado.

Atualmente, os códigos de status aceitos são os seguintes:
- 4XX: 400, 403, 404, 405, 414, 416 e 451
- 5XX: 500, 501, 502, 503 e 504

>! 
>- Essa funcionalidade pode não estar disponível em algumas plataformas. Concluiremos a atualização do servidor o mais breve possível.
>- Essa funcionalidade é apenas para redirecionar os códigos de status de solicitações encontrados durante o pull de origem, mas não se aplica a solicitações com códigos de status retornados por quaisquer funcionalidades de controle de acesso, como a configuração de lista de bloqueio/lista de permissões do UA.

## Guia de configuração

### Visualização da configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Mude para a guia **Advanced Configuration (Configuração avançada)** para localizar a seção **Custom Error Page Configuration (Configuração da página de erro personalizada)**.

A configuração da página de erro personalizada fica desativada por padrão.
![](https://main.qcloudimg.com/raw/ad8f4340f2f7c67247e9730a12e6d27b.png)



### Adição de regras

Você pode clicar em **Add Rule (Adicionar regra)** para adicionar regras de páginas de erro personalizadas, conforme necessário.
<img src="https://main.qcloudimg.com/raw/7af17d161ec2f4e499a5740383d4658e.jpg" style="height:220px"/>



**Limitações de configuração**

- Cada código de status pode ter apenas uma regra exclusiva.
- Redirecionamento: 301 ou 302.
- URL de destino: `http://` ou `https://` é obrigatório.
- O conteúdo pode conter até 1.024 caracteres e os caracteres chineses não são aceitos.
