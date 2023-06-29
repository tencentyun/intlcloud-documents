## Autenticação Remota

### Visão geral

Para impedir o acesso não autorizado, a Tencent Cloud oferece suporte à autenticação remota, além da [autenticação de carimbo de data/hora avançada](https://intl.cloud.tencent.com/document/product/228/35237) na borda do CDN.

Veja a seguir como funciona a autenticação remota:

![](https://qcloudimg.tencent-cloud.cn/raw/8f8d75de26e96ebaf58676eee0ca084a.png)

1. O usuário final inicia uma solicitação.
2. O CDN encaminha a solicitação para o servidor de autenticação remoto.
3. O servidor de autenticação retorna um código de status como resultado da autenticação.
4. O nó CDN responde ao solicitante de acordo com o código de retorno.

> !
> - Quando o código de retorno é `200`/`206`/`304`, a autenticação foi bem-sucedida. Para uma autenticação bem-sucedida, a solicitação é permitida com o código 200 retornado; para uma falha de autenticação, ele é bloqueado com o código 403 retornado.
> - Por enquanto, apenas a autenticação remota sincronizada é compatível, o que significa que o CDN responde após receber o resultado da autenticação do servidor de autenticação remoto.
> - Observe que a autenticação remota NÃO é compatível em algumas regiões fora da China continental.
> - A autenticação remota não está disponível para recursos de áudio e vídeo



### Instruções

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda. Clique em **Manage (Gerenciar)** à direita do nome de domínio para entrar na página de configuração. Configure a autenticação remota na guia **Access Control (Controle de acesso)**.

- **Server Address (Endereço do Servidor)**: insira um nome de domínio HTTP/HTTPS ou um endereço IP.
- **Request Method (Método de solicitação)**: selecione um método de solicitação. Você pode optar por seguir a solicitação do cliente ou especificar um método de solicitação (GET/POST/HEAD).
- **File Type (Tipo de arquivo)**: defina o escopo de autenticação. Você pode escolher **All content (Todo o conteúdo)**/**Specified File Extension (Extensão de arquivo especificada)**/**Specified File (Arquivo especificado)**.
- **Timeout Period (Período de tempo limite)**: defina a quantidade de tempo limite de resposta para o servidor de autenticação remoto. O valor máximo é 30.000 ms.
- **Timeout Action (Ação de tempo limite)**: a ação tomada após encerrado o tempo de resposta.
 O valor padrão é **Allow**.

<img src="https://qcloudimg.tencent-cloud.cn/raw/02def6deb735b7defbbd26a86be9b022.png" width="60%">



## Exemplo

Suponha que o nome de domínio de aceleração seja `www.example.com` e sua autenticação remota esteja configurada da seguinte forma:

- **Server Address (Endereço do servidor)**: `www.remoteauth.com`
- **Request Method (Método de solicitação)**: Seguir solicitação do cliente
- **File Type (Tipo de arquivo)**: Todos os conteúdos
- **Timeout Period (Período de tempo limite)**: 1.500 ms
- **Timeout Action (Ação de tempo limite)**: Bloquear

O CDN responderá à solicitação do usuário da seguinte forma:
1. O usuário inicia uma solicitação GET: `http://www.example.com/v001/test.txt?token=Gf6Gq04ymjdSTXusvTmh8yalO82YsuKUQb63ToXOFc&e=1467565695283&sign=854124740723b575a7cfa4fc40f0be30`
2. O CDN recebe a solicitação e a encaminha para o servidor de autenticação remoto: `http://www.remoteauth.com/v001/test.txt?token=Gf6Gq04ymjdSTXusvTmh8yalO82YsuKUQb63ToXOFc&e=1467565695283&sign=854124740723b575a7cfa4fc40f0be30`
3. O servidor de autenticação remoto retorna um código de status.
4. O CDN responde normalmente com 200 se o código de status retornado for 200 (ou seja, a autenticação foi aprovada).


