### Visão geral

Uma **tag** é um par de chave-valor fornecido pela Tencent Cloud para identificar um recurso na nuvem. Para obter mais informações, consulte [Visão geral de tags](http://intl.cloud.tencent.com/document/product/651/13334).
Você pode gerenciar os recursos do TencentDB for MySQL de maneira categorizada, usando vários tipos de tags, como as de negócios, de objetivo e de responsável, facilitando a localização dos recursos adequados. As tags não possuem significado semântico para a Tencent Cloud e são analisadas e combinadas estritamente com base em strings. Durante o uso, você só precisa prestar atenção aos [limites de uso](http://intl.cloud.tencent.com/document/product/651/13354) aplicáveis.
Veja abaixo um caso de uso específico que mostra como uma tag é usada.

## Contexto do caso de uso
Uma empresa possui 10 instâncias do TencentDB for MySQL na Tencent Cloud. Distribuídas em três departamentos (comércio eletrônico, jogos e entretenimento), essas instâncias são usadas para atender a linhas de negócios internas, como marketing, jogo A, jogo B e pós-produção. Os proprietários de OPS dos três departamentos são John, Jane e Harry, respectivamente.

## Definição de tag
Para facilitar o gerenciamento, a empresa categoriza seus recursos do TencentDB for MySQL com tags e define os seguintes pares de chave-valor de tag:

| Chave da tag  | Valor da tag|
| :---------- | ---------------------------------- |
| Departamento      | E-commerce, jogos, e entretenimento                   |
| Negócio       | Marketing, jogo A, jogo B, e pós-produção |
| Proprietário de OPS | John, Jane, e Harry                   |

Essas chaves/valores de tag são vinculados a instâncias do TencentDB for MySQL da seguinte maneira:

|instance-id	|Departamento	|Negócio	|Proprietário de OPS|
|----------------|-------|----|--------------|
|cdb-abcdef1	|E-commerce	|Marketing	|Harry|
|cdb-abcdef2	|E-commerce	|Marketing	|Harry|
|cdb-abcdef3|Jogos|Jogo A|John|
|cdb-abcdef3|Jogos|Jogo B|John|
|cdb-abcdef4|Jogos|Jogo B|John|
|cdb-abcdef5|Jogos|Jogo B|Jane|
|cdb-abcdef6|Jogos|Jogo B|Jane|
|cdb-abcdef7|Jogos|Jogo B|Jane|
|cdb-abcdef8	|Entretenimento	|Pós-produção|	Harry|
|cdb-abcdef9	|Entretenimento	|Pós-produção|	Harry|
|cdb-abcdef10|	Entretenimento	|Pós-produção|	Harry|

### Uso de uma tag
Para obter mais informações sobre como criar e excluir uma tag, consulte [Guia de operação](https://intl.cloud.tencent.com/document/product/651/41684).

Para obter mais informações sobre como editar uma tag no TencentDB for MySQL, consulte [Edição de tags](https://intl.cloud.tencent.com/document/product/236/31918).

