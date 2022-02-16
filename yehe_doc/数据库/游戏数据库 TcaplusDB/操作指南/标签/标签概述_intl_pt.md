## Visão geral
Uma tag é um par de chave-valor fornecido pelo Tencent Cloud para identificar um recurso na nuvem. Para obter mais informações, consulte [Visão geral de tags](https://intl.cloud.tencent.com/document/product/651/13334).

Você pode gerenciar os recursos do TcaplusDB de maneira categorizada, usando tags em várias dimensões, como negócios, objetivo e responsável, facilitando a localização dos recursos adequados. As tags não possuem significado semântico para o Tencent Cloud e são analisadas e combinadas estritamente com base em strings. Durante o uso, você só precisa prestar atenção aos [limites de uso](https://intl.cloud.tencent.com/document/product/651/13354) aplicáveis.

Veja abaixo um caso de uso específico que mostra como uma tag é usada.

## Contexto do caso de uso
Uma empresa possui três clusters do TcaplusDB no Tencent Cloud, que são distribuídos em três linhas de jogos cujos proprietários de operações são John, Jane e Harry, respectivamente.

## Definição de tag
Para facilitar o gerenciamento, a empresa categoriza seus recursos do TcaplusDB com tags e define os seguintes pares de chave-valor de tag:

| Chave da tag | Valor da tag |
| :---------- | ---------------------------------- |
| Linha | Jogo 1, jogo 2 e jogo 3 |
| Proprietário de operações | John, Jane e Harry |

Essas tags são vinculadas aos recursos do TcaplusDB da seguinte forma:

| ID do recurso		| Linha	| Proprietário de operações |
|---------------------|----|--------------|
| tcaplus-abcdef1	| Jogo 1	| Harry |
| tcaplus-abcdef2	| Jogo 2 | Jane |
| tcaplus-abcdef3	| Jogo 3	| John |

## Uso de tag
- Para obter mais informações sobre como criar e excluir uma tag, consulte [Introdução às tags](https://intl.cloud.tencent.com/document/product/651/32582).
- Para obter mais informações sobre como editar uma tag no TcaplusDB, consulte [Edição de tags](https://intl.cloud.tencent.com/document/product/1016/36551).
