## Descrição do algoritmo
**Formato do URL de acesso**
`http://DomainName/FileName?sign=md5hash&t=timestamp`

**Descrição do algoritmo**
- `timestamp`: um carimbo de data/hora decimal ou hexadecimal no formato UNIX.
- `md5hash`: MD5 (chave personalizada + caminho do arquivo + timestamp).

**Solicitação de exemplo**
`http://cloud.tenloud.tencent.com/test.jpg?sign=0f8201d814dfaf64cf54e74c5f7dbcb0&t=1582791032`

> !Quando o valor MD5 é calculado, se o caminho da solicitação for `http://cloud.tencent.com/test.jpg`, então, o caminho usado para o cálculo de MD5 será `/test.jpg`.

## Guia de configuração
### Descrição do parâmetro
O TypeD requer as seguintes configurações:
![](https://main.qcloudimg.com/raw/6caae33f26a263699003ccb2e4e562c5.png)
**Chave de autenticação personalizada**: composta por 6 a 40 dígitos e letras maiúsculas e minúsculas. A chave deve ser mantida privada e de posse apenas do cliente e servidor.
**Nome do parâmetro de autenticação e nome do parâmetro de carimbo de data/hora personalizados**: o `sign` no exemplo pode ser substituído por um nome de parâmetro composto de 1 a 100 letras maiúsculas e minúsculas, dígitos e sublinhados. Após o CDN receber a solicitação, ele reconhecerá o valor do parâmetro de assinatura especificado e calculará o valor de MD5. Se o resultado corresponder ao antigo valor `md5hash`, a assinatura será verificada com sucesso. Caso contrário, um erro 403 será retornado de imediato.
**Período de validade personalizado**: o valor de `timestamp` no parâmetro de carimbo de data/hora, mais o período de validade configurado, é comparado com a hora atual para determinar se a solicitação expirou. Se tiver expirado, um erro 403 será retornado de imediato. O intervalo de validade acontece em segundos. 

### Objeto
Depois de configurar a chave, o nome do parâmetro e o período de validade, o objeto de autenticação pode ser especificado conforme necessário. Os três modos de autenticação a seguir são compatíveis:
![](https://main.qcloudimg.com/raw/8a9b8c36cfc91a31cf96b31f0e6553c2.png)

+ Todos os arquivos sob um nome de domínio especificado precisam ser autenticados.
+ Todos os arquivos precisam ser autenticados, exceto aqueles de um tipo especificado.
+ Apenas arquivos de um tipo especificado precisam ser autenticados.

## Observações
**Taxa de acertos de cache**
Se você ativou o modo de autenticação TypeD para um nome de domínio, o URL de acesso carregará o parâmetro de autenticação. Quando um nó do CDN armazena o recurso em cache, ele ignora automaticamente o parâmetro correspondente e, portanto, não afeta a taxa de acertos do cache.
>!Como o parâmetro correspondente será ignorado automaticamente após a configuração, ou seja, os parâmetros de autenticação e de carimbo de data/hora configurados serão filtrados, as chaves de cache dos arquivos a serem autenticados serão afetadas e a prioridade aqui é maior do que as regras de chave de cache em **Cache Configuration (Configuração de cache)** -> ***Cache Key Rule Configuration (Configuração de regra de chave de cache)**.
Por exemplo, nesse caso a configuração TypeD é a seguinte: "Parâmetro de autenticação: `sigh`"; "Parâmetro de carimbo de data/hora: `t`"; "Escopo da autenticação: `jpg`"; então os parâmetros `sign` e `t` serão filtrados automaticamente para arquivos JPG, embora a configuração esteja como "Todos os arquivos: Não filtrar" em **Cache Configuration (Configuração de cache)** -> **Cache Key Rule Configuration (Configuração de regra de chave de cache)**.

**Política de pull de origem**
O formato de acesso de um nome de domínio com o modo de autenticação TypeD ativado é:
`http://DomainName/FileName?sign=md5hash&t=timestamp`

Se o nó do CDN não for atingido após a autenticação, ele iniciará uma solicitação de pull de origem, **que está no mesmo formato da solicitação de acesso com o parâmetro `sign/t` retido**. O servidor de origem pode ignorar ou executar a autenticação novamente se necessário.
