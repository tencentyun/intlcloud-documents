## Descrição do algoritmo
**Formato do URL de acesso**
`http://DomainName/Filename?sign=timestamp-rand-uid-md5hash`

>! O URL de acesso não pode conter caracteres chineses.

**Descrição do algoritmo**
- `timestamp`: um carimbo de data/hora decimal no formato UNIX.
- `rand`: uma string aleatória contendo de 0 a 100 dígitos, letras maiúsculas e minúsculas.
- `uid`: 0.
- `md5hash`: MD5 (caminho do arquivo-timestamp-rand-uid-chave personalizada).

**Exemplo de solicitação**
`http://cloud.tencent.com/test.jpg?sign=1582791032-im1acp76sx9sdqe601v-0-dd63f95e739ed4b47427a129d21ef4e3`

> ! Supondo que você esteja calculando o MD5 para o caminho da solicitação `http://cloud.tencent.com/test.jpg`, o caminho usado para o cálculo de MD5 será `/test.jpg`.

## Instruções
### Descrição do parâmetro
O TypeA requer as seguintes configurações:
![](https://main.qcloudimg.com/raw/b7da5881cba4ad972aa11f43bc2bc2ca.png))
**Authentication Key (Chave de autenticação)**: aceita de 6 a 40 letras maiúsculas e minúsculas e dígitos. A chave deve ser mantida privada e de posse apenas do cliente e servidor.
**Signature Parameter Name (Nome do parâmetro de assinatura)**: o `sign` no exemplo pode ser substituído por um nome de parâmetro contendo de 1 a 100 letras maiúsculas e minúsculas, dígitos e sublinhados. Após o CDN receber a solicitação, ele reconhecerá o valor do parâmetro de assinatura especificado e calculará o valor de MD5. Se o resultado corresponder ao antigo valor `md5hash`, a assinatura será verificada com sucesso. Caso contrário, um erro 403 será retornado de imediato.
**Valid Time (Tempo válido)**: decide se a solicitação expirou comparando o valor de `timestamp` na solicitação mais o período de validade configurado com a hora atual. Se tiver expirado, um erro 403 será retornado de imediato. O período de validade pode ser de até 630720000 segundos.

### Objeto
Depois de configurar a chave, o nome do parâmetro e o período de validade, o objeto de autenticação pode ser especificado conforme necessário. Os três modos de autenticação a seguir são compatíveis:
![](https://main.qcloudimg.com/raw/148f6319984b1f3d99ccb186666cb425.png)

+ Todos os arquivos sob um nome de domínio especificado precisam ser autenticados.
+ Todos os arquivos precisam ser autenticados, exceto aqueles de um tipo especificado.
+ Apenas arquivos de um tipo especificado precisam ser autenticados.

## Observações
**Taxa de acertos de cache**
Para nomes de domínio usando o modo de autenticação TypeA, o URL de acesso carregará o parâmetro de autenticação. Quando um nó do CDN armazena o recurso em cache, o parâmetro correspondente será ignorado e, portanto, não afetará a taxa de acertos do cache.
>!Como o parâmetro de autenticação será automaticamente ignorado, as chaves de cache dos arquivos a serem autenticados serão afetadas e a prioridade aqui é maior do que as regras de chave de cache em **Cache Configuration (Configuração de cache)** -> ***Cache Key Rule Configuration (Configuração de regra de chave de cache)**.
Por exemplo, nesse caso a configuração TypeA é a seguinte: "Parâmetro de autenticação: `sign`"; "Escopo de autenticação: `jpg`"; então o parâmetro `sign` será ignorado automaticamente para arquivos JPG, embora a configuração esteja como "Todos os arquivos: Não ignorar" em **Cache Configuration (Configuração de cache)** -> **Cache Key Rule Configuration (Configuração de regra de chave de cache)**.


**Política de pull de origem**
O formato de acesso de um nome de domínio com o modo de autenticação TypeA ativado é:
`http://DomainName/Filename?sign=timestamp-rand-uid-md5hash`

Se o nó do CDN não for atingido após a autenticação, ele iniciará uma solicitação de pull de origem, **que está no mesmo formato da solicitação de acesso com o parâmetro `sign` retido**. O servidor de origem pode ignorar ou executar a autenticação novamente se necessário.
