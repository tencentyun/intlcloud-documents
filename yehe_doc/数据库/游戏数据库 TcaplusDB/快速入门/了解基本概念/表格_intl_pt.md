## Visão geral de tabelas
Como em outros bancos de dados, uma tabela no TcaplusDB é um conjunto de dados como uma combinação de dados de linhas armazenados com base na definição da tabela.
Do ponto de vista de negócios de jogos, uma tabela pode gerenciar um conjunto de dados correlacionados de um módulo de linha, como tabela de usuários e tabela de itens.

Por exemplo, a tabela de jogadores abaixo pode armazenar as informações de todos os jogadores em um jogo, como o nome do personagem do jogo, o gênero, a raça, o nível, a força, as engrenagens, a montaria e os itens.
```
{
player_id:11474,
player_name: "Test account 2",
gender:0,
ethnicity:"Elf",
FightingPower:10,
equipment:
	{
		helmet:0,
		Warframe:0,
		gloves:0,
		necklace:0,
		pants:0,
		Shoes:0
	},
horse:"0"
}，
{
player_id:11475,
player_name: "Test account 1",
gender:1,
ethnicity:"Orc",
FightingPower:1477,
equipment:
	{
		helmet:1478,
		Warframe:21,
		gloves:554,
		necklace:12,
		pants:64,
		Shoes:122
	},
horse:"3"
}
```


### Registro
Um registro é um conjunto de valores de campo do mesmo objeto. No exemplo da tabela do personagem do jogador acima, todas as informações consistem em vários valores de campo de atributos, que juntos representam o conjunto de informações do personagem do jogador no jogo. Um registro pode conter até 1 MB de dados.

### Campo
Um campo descreve um atributo de um objeto especificado. No exemplo da tabela do personagem do jogador acima, um atributo, independente de um personagem do jogador, é chamado de campo, como `player_name` e `ethnicity`.

#### Campo de chave primária
Como pode ser encontrado no exemplo da tabela acima, cada registro possui um campo que marca sua exclusividade. Esse campo é denominado campo de chave primária. Na tabela do personagem do jogador acima, os campos de chave primária são `player_id` e `player_name`. O TcaplusDB aceita até 4 campos de chave primária.

#### Campo geral
Além dos campos que marcam a exclusividade do registro, cada registro também possui outros atributos chamados de campos gerais. No exemplo da tabela do personagem do jogador acima, os campos gerais incluem `equipment` e `FightingPower`. O TcaplusDB aceita até 128 campos gerais.

#### Campo de fragmentação
O TcaplusDB é um sistema de banco de dados distribuídos que pode fornecer maior capacidade de solicitações simultâneas para tabelas. Se você definir um campo de fragmentação, o TcaplusDB calculará seu valor de hash para ajustar automaticamente os fragmentos da tabela com base nas condições atuais de acesso à tabela; caso contrário, o sistema usará um campo de chave primária como o campo de fragmentação.

A configuração do campo de fragmentação está sujeita à distribuição de dados de back-end. Você precisa avaliar se os valores de campo usado como campo de fragmentação são discretos. Não é recomendável definir um campo com valores limitados (ex.: gênero e dia da semana) como o campo de fragmentação; em vez disso, é recomendável usar campos como ID e nome.

#### Tipo de campo
O TcaplusDB aceita vários tipos de dados, conforme detalhado abaixo:

| Tipo de campo | Descrição |
|----------|--------------|
| int32 | Inteiro com sinal de comprimento variável que pode representar um valor entre \-2^31 e \+2^31. De certa forma é ineficiente para representar um número negativo. |
| int64 | Inteiro com sinal de comprimento variável que pode representar um valor entre \-2^63 e \+2^63. |
| uint32 | Inteiro sem sinal de comprimento variável que pode representar um valor entre 0 e 2^32. |
| uint64 | Inteiro sem sinal de comprimento variável que pode representar um valor entre 0 e 2^64. |
| sint32 | Valor `int` com sinal de comprimento variável, que é mais eficiente para representar um número negativo do que o `int32` regular. |
| sint64 | Valor `int` com sinal de comprimento variável, que é mais eficiente para representar um número negativo do que o `int64` regular. |
| bool | Valor booleano que representa `True` ou `False`. |
| fixed32 | Tipo numérico de comprimento fixo sempre ocupando 4 bytes. É mais eficiente do que o `uint32` se o valor estiver normalmente acima de 2^28. |
| fixed64 | Tipo numérico de comprimento fixo sempre ocupando 8 bytes. É mais eficiente do que o `uint64` se o valor estiver normalmente acima de 2^56. |
| sfixed32 | Tipo numérico de comprimento fixo sempre ocupando 4 bytes. |
| sfixed64 | Tipo numérico de comprimento fixo sempre ocupando 8 bytes. |
| float | Ponto flutuante binário de 32 bits ocupando 4 bytes. |
| double | Ponto flutuante binário de dupla precisão de 64 bits ocupando 8 bytes. |
| strings | String codificada com UTF\-8 ou ASCII de 7 bits que não pode exceder 2^32 de comprimento. |
| bytes | Sequência de bytes de comprimento abaixo de 2^32. |
| message | Tipo aninhado. Ele aceita até 128 níveis de aninhamento consecutivos. Uma grande quantidade de níveis de aninhamento afetará o desempenho. |

### Formato de definição de tabela
O TcaplusDB aceita o Protocol Buffers, que é um formato de armazenamento de dados estruturados leve e eficiente, usado principalmente para armazenar dados estruturados sequencialmente.
Para obter mais informações sobre formatos de tabelas, consulte [Linguagem de descrição de tabelas](https://intl.cloud.tencent.com/document/product/1016/36559).
