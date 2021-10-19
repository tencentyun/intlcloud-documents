## Descrição do algoritmo
**Formato do URL de acesso**
`http://DomainName/md5hash/timestamp/FileName`

**Descrição do algoritmo**
- timestamp: um carimbo de data/hora hexadecimal no formato UNIX.
- md5hash: MD5 (chave personalizada + caminho do arquivo + timestamp).

**Solicitação de exemplo**
`http://cloud.tencent.com/8fe9b5597c809d7ace147468c7c7eadb/5e577978/test.jpg`

> !Quando o valor MD5 é calculado, se o caminho da solicitação for `http://cloud.tencent.com/test.jpg`, então, o caminho usado para o cálculo de MD5 será `/test.jpg`.

## Guia de configuração
### Descrição do parâmetro
O TypeC requer as seguintes configurações:
![](https://main.qcloudimg.com/raw/d7b8d589f8690f1e4c33985d6bcd3f09.png)
**Chave de autenticação personalizada**: pode conter de 6 a 40 dígitos, maiúsculas e minúsculas. Deve ser mantida em sigilo e divulgada apenas para o cliente e o servidor.
**Período de validade personalizado**: o valor de `timestamp` no caminho da solicitação mais o período de validade configurado é comparado com a hora atual para determinar se a solicitação expirou; em caso afirmativo, um erro 403 será retornado diretamente.

### Objeto
Depois de configurar a chave, o nome do parâmetro e o período de validade, o objeto de autenticação pode ser especificado conforme necessário. Os três modos de autenticação a seguir são compatíveis:
![](https://main.qcloudimg.com/raw/34d27c8908808cacddfde94c8a3f1d81.png)
+ Todos os arquivos sob um nome de domínio especificado precisam ser autenticados.
+ Todos os arquivos, exceto aqueles de um tipo especificado, precisam ser autenticados.
+ Apenas arquivos de um tipo especificado precisam ser autenticados.

## Observações:
**Taxa de acertos de cache**
Se você ativou a autenticação TypeC para um nome de domínio, a assinatura e o carimbo de data/hora serão transportados no caminho do URL de acesso. Quando um nó do CDN armazena em cache um recurso, ele ignora o caminho de autenticação automaticamente e, portanto, não afeta a taxa de acertos do cache.
**Política de pull de origem**
O formato de acesso de um nome de domínio com o modo de autenticação TypeC ativado é:
`http://DomainName/md5hash/timestamp/FileName`

Se nenhum acerto for encontrado no nó do CDN após a autenticação, o nó iniciará uma solicitação de pull de origem, **na qual `md5hash` e `timestamp` serão removidos do caminho.** O servidor de origem não requer nenhuma configuração.
