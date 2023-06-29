
## Visão geral das configurações

Por padrão, o CDN é compatível com as portas 80, 8080 e 443. É possível desativá-las, se necessário.

>! 
>- No momento, a configuração da porta está disponível apenas na China Continental. Se um nome de domínio estiver configurado para a aceleração global, as alterações na configuração entrarão em vigor apenas na China Continental.
>- Essa funcionalidade pode não estar disponível em algumas plataformas. Concluiremos a atualização do servidor o mais breve possível.

## Guia de configuração

### Visualização da configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia **Access Control (Controle de acesso)** para localizar a seção **Chinese Mainland Access Port Configuration (Configuração da porta de acesso da China Continental)**.

As portas 80, 8080 e 443 ficam ativadas por padrão.
![](https://main.qcloudimg.com/raw/a9f3930bb87a720acd8a09fb07f333d2.png)

### Modificação da configuração

É possível desativar e ativar as portas conforme necessário.

**Limitações de modificação**

- Se o acesso HTTPS ou o redirecionamento forçado de HTTPS estiver ativo para um nome de domínio, a porta 443 não pode ser desativada.
- A porta 80 ou 8080 deve ficar aberta.



## Exemplos de configuração

Se a **Chinese Mainland Access Port Configuration (Configuração da porta de acesso da China Continental)** do nome de domínio de aceleração `www.test.com` for a seguinte:
![](https://main.qcloudimg.com/raw/a420e4f25d322855ee04b41c408ea9ab.png)

Então, o acesso real será:

Os nós do CDN negam todas as solicitações de acesso da porta 8080.
- Se um nome de domínio estiver configurado para a aceleração global, a configuração só terá efeito na China Continental, o que significa que os nós do CDN negarão as solicitações de acesso da porta 8080.

