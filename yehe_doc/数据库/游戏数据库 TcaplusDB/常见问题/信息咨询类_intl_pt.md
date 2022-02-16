- [O TcaplusDB permite a remoção de dados?](#41)
- [Quais são as estruturas de dados do TcaplusDB?](#43)
- [Qual é a capacidade de memória de instância única e a utilização da CPU do SDK do TcaplusDB?](#67)
- [Quantas tabelas há em um grupo de tabelas no TcaplusDB?](#68)
- [Quais são as restrições nos campos de chave e valor no TcaplusDB?](#69)
- [Por quanto tempo o arquivo de backup do TcaplusDB é retido?](#72)
- [O servidor do jogo está conectado a todos os tcaproxy (camada de acesso)?](#73)
- [Como realizo a análise dos dados do TcaplusDB?](#74)
- [Qual é o tamanho máximo de uma única tabela no TcaplusDB? Qual é o limite da quantidade de registros?](#82)
- [O TcaplusDB permite operações de transações de várias tabelas e operações de gravação em lote?](#85)
- [A atualização da API do TcaplusDB é compatível com versões anteriores?](#88)

<span id="41"></span>
### O TcaplusDB permite a remoção de dados?
O TcaplusDB permite a remoção de dados em nível de tabela, em que os dados são removidos de acordo com a última vez que foram gravados.

<span id="43"></span>
### Quais são as estruturas de dados do TcaplusDB?
O TcaplusDB aceita estruturas de dados como matriz de lista, consultas por parte de chaves (índices), chave-valor, chave-objeto (isto é, o valor de uma única chave pode ser estruturas de dados arbitrárias, por exemplo, o servidor do jogo pode serializar `lua table` no campo de valor).

<span id="67"></span>
### Qual é a capacidade de memória de instância única e a utilização da CPU do SDK do TcaplusDB?
O consumo máximo de memória de instância única é 73 MB e a utilização máxima da CPU é 30%.

<span id="68"></span>
### Quantas tabelas há em um grupo de tabelas no TcaplusDB?
No TcaplusDB, um grupo de tabelas pode ter até 256 tabelas. Se houver mais de 256 tabelas em um grupo, você pode adicionar um novo grupo de tabelas ou mesclar as tabelas. Se você precisar de ajuda técnica, [envie um tíquete](https://console.cloud.tencent.com/workorder/category) e selecione **Other (Outro)** na página **Select the related product (Selecione o produto relacionado)**.

<span id="69"></span>
### Quais são as restrições nos campos de chave e valor no TcaplusDB?
A quantidade de campos de chave da tabela genérica é 4, a quantidade de campos de chave da tabela de lista é 3 e o tamanho de um único campo de chave é 1.024 B. A quantidade de campos de valor da tabela genérica é 128, a quantidade de campos de valor da tabela de lista é 127, o tamanho de um único campo de valor é 256 KB e o tamanho máximo de um registro é 1 MB.

<span id="72"></span>
### Por quanto tempo o arquivo de backup do TcaplusDB é retido?
Os arquivos do mecanismo com backup pelo TcaplusDB são retidos por 7 dias, e o Ulog é salvo por 7 dias. Os períodos de retenção variam com o ambiente do TcaplusDB. Para obter o período de retenção de um ambiente do TcaplusDB específico, você pode [entrar em contato com o atendimento ao cliente](https://intl.cloud.tencent.com/support).

<span id="73"></span>
### O servidor do jogo está conectado a todos os tcaproxy (camada de acesso)?
Para reduzir o custo de manutenção das conexões TCP entre o servidor do jogo e o tcaproxy (camada de acesso), o servidor do jogo permite a seleção de alguns tcaproxy (camada de acesso) para estabelecer as conexões.

<span id="74"></span>
### Como realizo a análise dos dados do TcaplusDB?
Os dados do TcaplusDB podem ser exportados em qualquer formato, incluindo json, pb e outros formatos, e podem ser importados para sistemas de análise de dados como o TDW. O TcaplusDB permite a importação de dados em tempo real em bancos de dados MySQL, etc.

<span id="82"></span>
### Qual é o tamanho máximo de uma única tabela no TcaplusDB? Qual é o limite da quantidade de registros?
Uma única tabela pode ser subdividida em 10.000 fragmentos de dados, cada fragmento de dados tem 256 GB, ou seja, o tamanho total de uma única tabela é 10.000 * 256 GB. Uma única tabela não tem limite para a quantidade de registros, e a quantidade de registros em uma única tabela está relacionada ao tamanho de um único registro.

<span id="85"></span>
### O TcaplusDB permite operações de transações de várias tabelas e operações de gravação em lote?
O TcaplusDB não permite operações de transações de várias tabelas nem operações de gravação em lote. Para realizar operações de transações de várias tabelas, as alterações devem ser feitas no seu negócio. No TcaplusDB, as operações devem ser feitas em sequência. Por exemplo, quando várias operações são enviadas ao mesmo tempo, todas as operações concluídas são revertidas se uma das operações posteriores falhar. Após a reversão, você pode enviar essas operações novamente. Para operações importantes, recomendamos manter os logs.

<span id="88"></span>
### A atualização da API do TcaplusDB é compatível com versões anteriores?
A atualização da API do TcaplusDB é compatível com versões anteriores, e as APIs, as palavras de comando e as funcionalidades existentes não serão modificadas.
