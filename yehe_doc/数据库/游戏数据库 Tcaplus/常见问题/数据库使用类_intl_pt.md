
- [Como devo obter a definição dos códigos de erro em um pacote de resposta?](#42)
- [Como funciona o bloqueio otimista do TcaplusDB e como usá-lo?](#44)
- [Quais são os casos de uso e as precauções para a tabela LIST?](#45)
- [Qual é a diferença entre INSERT, UPDATE e REPLACE?](#46)
- [Como obtenho a quantidade de registros em uma tabela?](#47)
- [O TcaplusDB aceita operações de travessia?](#48)
- [O TcaplusDB aceita a atualização e a obtenção de campos parciais?](#49)
- [O TcaplusDB está preservando a ordem para as operações contínuas de uma única chave primária?](#50)
- [O TcaplusDB aceita alterações na definição da tabela?](#51)
- [Como posso saber se o empacotamento do pacote de resposta terminou?](#54)
- [Qual é a diferença entre GetRecordCount e GetRecordMatchCount?](#55)
- [O TcaplusDB tem um campo de passagem?](#56)
- [Qual é a função de SetResultFlag?](#57)
- [Posso realizar operações de aumento em vários campos de chave não primária de uma vez? E se a chave primária não existir?](#58)
- [Como faço para reduzir os custos de tráfego quando o TcaplusDB lê os registros?](#60)
- [O TcaplusDB aceita reversões? Qual é a granularidade de reversão aceita?](#64)
- [Qual é o nível de eficiência das consultas por chaves parciais (índices) com o TcaplusDB?](#70)
- [Qual é o mecanismo de tempo limite para a API do TcaplusDB? O que significa o erro "it is timeout (o tempo limite foi atingido)"?](#75)
- [Quais são os papéis das funções SendRequest, OnUpdate e ReceiveResponse da API do TcaplusDB?](#76)
- [Como o TcaplusDB realiza aumento automático global de campos?](#77)
- [Quais regras são definidas para consultas por chaves parciais (índices)?](#78)
- [Como faço para obter uma consulta bidirecional de ID e nome de uma única tabela?](#79)
- [A tcaplus_client aceita a exibição de campos no segundo nível de aninhamento ou acima?](#83)
- [O que deve ser observado ao alterar a tabela no TcaplusDB?](#86)
- [O que deve ser observado ao definir a tabela no TcaplusDB?](#87)

<span id="42"></span>
### Como devo obter a definição dos códigos de erro em um pacote de resposta?
Recomendamos chamar as funções de `TcapErrCode::TcapErrCodeInit` e `TcapErrCode::GetErrStr` no servidor do jogo para obter os códigos de erro, ou pesquisar os arquivos de cabeçalho da API do TcaplusDB localmente.

<span id="44"></span>
### Como funciona o bloqueio otimista do TcaplusDB e como usá-lo?
Vamos usar a compra de passagens de trem como exemplo:
1. 100 pessoas querem comprar a mesma passagem de trem. O número da versão registrada da passagem de trem é 10, e as 100 pessoas usam o mesmo número de versão registrado para comprar a passagem de trem.
2. 100 pessoas realizam operações de gravação nesta passagem. Depois que a operação de gravação for concluída, o número da versão registrada aumentará. Portanto, para a operação de uma única chave, as threads de trabalho tcapsvr são enfileiradas. Quando a primeira pessoa comprou a passagem com êxito, o número da versão registrada da passagem de trem mudou para 11, e o número da versão registrada das 99 pessoas restantes ainda é 10.
3. Quando o tcapsvr lidar com as solicitações de gravação das 99 pessoas, ocorrerá um erro porque o número da versão registrada no final de tcapsvr é inconsistente com o número da versão na solicitação. Os princípios concorrentes são os seguintes:
 - N solicitações. Se apenas a primeira solicitação for bem-sucedida e as N-1 solicitações restantes falharem, as regras de proteção de versão serão usadas.
 - N solicitações. Se todas as solicitações N tiverem que ser executadas, nenhuma regra de proteção de versão será necessária. O TcaplusDB opera na mesma chave.
 
Enfileire e chame a função `SetCheckDataVersionPolicy`, cujos valores incluem:
 - `CHECKDATAVERSION_AUTOINCREASE`: o número da versão registrada é detectado, o que só aumentará automaticamente se for o mesmo que o número da versão do servidor.
 - `NOCHECKDATAVERSION_OVERWRITE`: o número da versão registrada não é detectado e o número da versão registrada do cliente é gravado de forma forçada no servidor.
 - `NOCHECKDATAVERSION_AUTOINCREASE`: o número da versão registrada não é detectado e o número da versão registrada do servidor aumentará automaticamente.
 - É recomendável que você use o tipo padrão `CHECKDATAVERSION_AUTOINCREASE`.

<span id="45"></span>
### Quais são os casos de uso e as precauções para a tabela LIST?
Onde há um caso de uso 1:N, quando N < 1024, a tabela LIST é priorizada, como armazenar os 100 e-mails mais recentes do jogador, os 100 registros de batalha mais recentes e assim por diante. A tabela LIST aceita a inserção no início da fila e a remoção no final da fila, a inserção no final da fila e a remoção no início da fila, assim como as N operações principais classificadas por tempo de inserção. A quantidade de unidades em uma única chave pode ser aumentada modificando a tabela, porque os dados antigos precisam ser compatíveis e não podem ser modificados para se tornarem menores. Você pode obter a quantidade total de registros em uma única chave usando `listgetall`. É recomendável obter dados de acordo com o deslocamento e um limite que você definiu. Para `listreplace`, `listdelete` e `listdeletebatch`, você precisa especificar o índice correto. Para `listaddafter`, você precisa especificar a regra de eliminação quando a quantidade de unidades de elemento em uma única chave atinge o limite superior. Se a função `SetListShiftFlag` for chamada, a tabela LIST terá duas direções crescentes e duas direções de obtenção. Existem 4 possibilidades:
1. Consulte A, B, C, D, E como deslocamento = número positivo e limite = 2, e o resultado é A, B; C, D; E.
2. Consulte A, B, C, D, E como deslocamento = número negativo e limite = 2, e o resultado é D, E; B, C; A.
3. Consulte E, D, C, B, A como deslocamento = número positivo e limite = 2, e o resultado é E, D; C, B; A.
4. Consulte E, D, C, B, A como deslocamento = número negativo e limite = 2, e o resultado é B, A; D, C; E.

Além disso, chamar `GetRecordMatchCount` pode obter a quantidade total de registros.

<span id="46"></span>
### Qual é a diferença entre INSERT, UPDATE e REPLACE?
Para a operação INSERT, quando a chave não existe, uma operação INSERT é executada; quando a chave existe, um código de erro é retornado: `TcapErrCode::SVR_ERR_FAIL_RECORD_EXIST`.
Para a operação REPLACE, quando a chave não existe, uma operação INSERT é executada; quando a chave existe, se o bloqueio otimista é usado, operações diferentes são executadas com base no resultado do bloqueio otimista. Se a operação for bem-sucedida, a operação REPLACE será executada e, se falhar, um código de erro será retornado: `TcapErrCode::SVR_ERR_FAIL_INVALID_VERSION;`. Se o bloqueio otimista não for usado, a operação REPLACE será executada.
Para a operação UPDATE, quando a chave existe, se o bloqueio otimista é usado, diferentes operações são executadas com base no resultado do bloqueio otimista. Se a operação for bem-sucedida, a operação UPDATE será executada e, se falhar, um código de erro será retornado: `TcapErrCode::SVR_ERR_FAIL_INVALID_VERSION`. Se o bloqueio otimista não for usado, a operação UPDATE será executada. Quando a chave não existe, um código de erro é retornado: `TcapErrCode::TXHDB_ERR_RECORD_NOT_EXIST`.

<span id="47"></span>
### Como obtenho a quantidade de registros em uma tabela?
Há uma palavra de comando de contagem na API do TcaplusDB. Se `tcaplus_client` for usado, você pode usar o comando de nome da tabela `count` para obter a quantidade de registros na tabela.

<span id="48"></span>
### O TcaplusDB aceita operações de travessia?
O TcaplusDB aceita operações de travessia, incluindo operações de travessia para tabelas GENERIC e LIST. Você pode usar a API `SetOnlyReadFromSlave(bool flag)` para percorrer os dados do tcapsvr secundário, o que não afetará os serviços fornecidos pelo tcapsvr principal.

<span id="49"></span>
### O TcaplusDB aceita a atualização e a obtenção de campos parciais?
O TcaplusDB aceita a atualização de campos parciais. Ao atualizar e obter registros, é recomendado chamar explicitamente a API `SetFieldNames(IN const char* field_name[], IN const unsigned field_count)` para determinar os campos desta operação de leitura e gravação e reduzir a sobrecarga de tráfego de rede causada por campos inválidos.

<span id="50"></span>
### O TcaplusDB está preservando a ordem para as operações contínuas de uma única chave primária?
Para o mesmo servidor de jogo, as operações da mesma chave primária preservam a ordem, já as operações de chaves primárias diferentes não preservam a ordem. Para servidores de jogo diferentes, a ordem não é preservada.

<span id="51"></span>
### O TcaplusDB aceita alterações na definição da tabela?
O TcaplusDB aceita alterações na definição da tabela. Para adicionar campos de chave não primária e alterar macros, basta alterar a tabela. Para alterações mais complexas, você pode alterar a estrutura da tabela continuamente usando a migração de dados e os logs. Para usar essa funcionalidade, [envie um tíquete](https://console.cloud.tencent.com/workorder/category) e selecione **Other (Outro)** na página **Select the related product (Selecione o produto relacionado)**.

<span id="54"></span>
### Como posso saber se o empacotamento do pacote de resposta terminou?
Para a travessia, verifique se a travessia termina de acordo com o estado, ou seja, a API `GetState`. Para o resto dos cenários de empacotamento, verifique se o empacotamento termina de acordo com a função `HaveMoreResPkgs`.

<span id="55"></span>
### Qual é a diferença entre GetRecordCount e GetRecordMatchCount?
Uma solicitação pode ter N pacotes de resposta. Se houver vários pacotes, `GetRecordCount` se refere à quantidade de registros no pacote de resposta, e `GetRecordMatchCount` se refere aos registros de dados armazenados no tcapsvr (camada de armazenamento) (quantidade total de registros para uma única chave).

<span id="56"></span>
### O TcaplusDB tem um campo de passagem?
O protocolo CS do TcaplusDB está dividido em duas partes: cabeçalho e corpo. `UserBuff` (tamanho máximo é 1 KB), `AsyncID` e `Sequence` no cabeçalho são todos campos de passagem. Você pode usá-los adequadamente.

<span id="57"></span>
### Qual é a função de SetResultFlag?
Ao executar operações de gravação, o pacote de resposta permite o retorno de registros. Ao realizar operações de leitura, chamar esta função é inválido. Os valores específicos de `result_flag` são os seguintes:
0: retorna apenas se a operação foi bem-sucedida ou não sem retornar o campo de valor.
1: retorna dados consistentes com o campo de solicitação.
2: retorna os dados mais recentes para todos os campos do registro alterado.
3: retorna os dados antigos para todos os campos do registro alterado.

A API `SetResultFlagForSuccess` pode ser usada para retornar os dados se a operação for bem-sucedida; a API `SetResultFlagForFail` pode ser usada para retornar os dados se a operação falhar.

<span id="58"></span>
### Posso realizar operações de aumento em vários campos de chave não primária de uma vez? E se a chave primária não existir?
Para aumentar vários campos de chave não primária, esses campos precisam ser atribuídos com valores pela solicitação do servidor do jogo. Se uma das chaves não existir, você pode usar a função `SetAddableIncreaseFlag` para executar operações de aumento. Se não existir nenhuma chave, insira uma chave e, em seguida, execute operações de aumento, em que os campos não aumentados da chave não serão armazenados e assumirão o valor padrão quando o registro for lido. Se a chave existir, a operação de aumento pode ser executada imediatamente.

<span id="60"></span>
### Como faço para reduzir os custos de tráfego quando o TcaplusDB lê os registros?
Quando o TcaplusDB lê um registro, ele pode ser configurado para não retornar o campo de valor se o registro não tiver alteração em um período fixo, nem retornar o campo de valor se o número da versão do registro não mudar. Para obter mais informações, consulte a função `SetFlags`.

<span id="64"></span>
### O TcaplusDB aceita reversões? Qual é a granularidade de reversão aceita?
O TcaplusDB aceita reversões, incluindo reversão de todos os servidores/regiões, reversão de tabela única e pode reverter N registros de 100 bilhões de registros. Ele também aceita reversão manual de tempo de espera (mais recente 01:05:00), reversão de tempo precisa (em segundos) e reversão difusa (você pode especificar as regras de reversão). Para referência de velocidade, a reversão de tempo precisa leva cerca de 2 horas para uma reversão de dados de 300 GB e Ulog de 200 GB. O princípio da reversão manual de tempo de espera é substituir o arquivo do mecanismo. O princípio da reversão de tempo precisa é reverter o arquivo do mecanismo de tempo de espera manual + Ulog para o ponto de tempo necessário. Uma reversão baseada em chave requer que você bloqueie essas chaves primeiro e, em seguida, desbloqueie-as após o TcaplusDB terminar a reversão.

<span id="70"></span>
### Qual é o nível de eficiência das consultas por chaves parciais (índices) com o TcaplusDB?
É recomendável usar consultas por chaves parciais (índices) em cenários de aplicação 1:N (N > 1024). A quantidade de chaves primárias em uma única chave de índice é igual a 10 GB/o tamanho da chave primária de um único registro. Uma única operação de índice de leitura e gravação leva cerca de 100 ms (há mais de 100.000 partes de registros de dados em uma única chave de índice).

<span id="75"></span>
### Qual é o mecanismo de tempo limite para a API do TcaplusDB? O que significa o erro "it is timeout (o tempo limite foi atingido)"?
A API do TcaplusDB atribui um ID a cada solicitação. Depois de ser enviado com sucesso, o ID é enviado para a estrutura de avaliação de tempo limite. Se o pacote de resposta para a solicitação retornar, o ID será removido da estrutura. Se o pacote de resposta da solicitação não tiver sido processado pela camada de aplicativos em 3 segundos, um log de erro com a palavra-chave "it is timeout (o tempo limite foi atingido)" é impresso. Você precisará verificar se o servidor do jogo está bloqueado. Pode ser que o tcaproxy (camada de acesso) tenha removido os pacotes ao devolvê-los ao servidor do jogo, ou o pacote de resposta chegou ao servidor do jogo, mas o servidor do jogo não o processou a tempo.
O TcaplusDB recomenda que você mesmo implemente o mecanismo de tempo limite, que permite realizar novas tentativas e outros processos para solicitações de tempo limite.

<span id="76"></span>
### Quais são os papéis das funções SendRequest, OnUpdate e ReceiveResponse da API do TcaplusDB?
O papel de `SendRequest` é enviar solicitações. Esta solicitação pode ter sido enviada para a rede, ou pode estar bloqueada no canal de envio do servidor do jogo e um tcaproxy (camada de acesso). O papel de `ReceiveResponse` é obter o pacote de resposta da fila de recebimento local. O `OnUpdate` é responsável por enviar as solicitações da fila de envio para a rede e receber os pacotes de resposta da rede para a fila de recebimento. No modo de programação orientado por mensagens, o `OnUpdate` é recomendado para ser chamado uma vez a cada milissegundo.

<span id="77"></span>
### Como o TcaplusDB realiza aumento automático global de campos?
Você precisa definir uma única tabela e definir o tipo de campo de uma única chave e um único valor para int64_t (vários campos de valor podem implementar matrizes de contador). Vários servidores de jogos podem aumentar uma única chave simultaneamente (sem definir as regras de proteção de versão) e obter o resultado de aumento retornado para esta operação, então o resultado do aumento será um aumento automático global.

<span id="78"></span>
### Quais regras são definidas para consultas por chaves parciais (índices)?
A chave do índice deve fazer parte da chave primária, a chave do índice deve conter a shardkey e a chave do índice não pode ser a chave primária.

<span id="79"></span>
### Como faço para obter uma consulta bidirecional de ID e nome de uma única tabela?
O terceiro campo de chave x é usado como shardkey, e o índice é criado em ID e x, nome e x para obter essa funcionalidade. Por exemplo, ao armazenar informações do jogador, o distrito do jogador pode ser adicionado, ou seja, a chave primária é uin, nome, distrito e a chave de índice é uin e distrito, e nome e distrito.

<span id="83"></span>
### A tcaplus_client aceita a exibição de campos no segundo nível de aninhamento ou acima?
Sim. Você pode executar `help select` para ver como `select * into a.xml` é usado.

<span id="86"></span>
### O que deve ser observado ao alterar a tabela no TcaplusDB?
1. Você só pode adicionar novos campos. Você não pode modificar o tipo e o nome de um campo existente ou excluir um campo existente. Para modificá-los, você precisa modificar a estrutura da tabela dinamicamente.
2. O comprimento de uma matriz ou string em um campo de chave não primária pode ser aumentado, mas não reduzido. Para modificá-lo, você precisa modificar a estrutura da tabela dinamicamente.
3. O número da versão deve ser incrementado em 1 para cada novo campo, e o número da versão definido na parte superior do arquivo XML também deve ser incrementado em 1 (ou seja, o número da versão do arquivo XML deve ser o mesmo do novo campo). A tabela no TcaplusDB precisa ser alterada antes que a tabela no servidor do jogo seja alterada. O TcaplusDB permite a modificação dinâmica da estrutura da tabela e, para usar essa funcionalidade, [envie um tíquete](https://console.cloud.tencent.com/workorder/category) e selecione **Other (Outro)** na página **Select the related product (Selecione o produto relacionado)**.

<span id="87"></span>
### O que deve ser observado ao definir a tabela no TcaplusDB?
1. O campo `refer` precisa ser adicionado ao campo `count`.
2. A shardkey da tabela deve ser altamente discreta.
3. A chave do índice não pode ser igual à chave primária.


