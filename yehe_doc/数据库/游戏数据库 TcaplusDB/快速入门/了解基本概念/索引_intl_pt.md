## Visão geral do índice
Você pode criar um índice para uma tabela e usá-lo para obter rapidamente os dados desejados de um banco de dados, o que oferece maior flexibilidade na consulta de dados para sua aplicação.

O TcaplusDB aceita dois tipos de índices:
- Índice local: deve ser composto de campos de chave primária e permite consultar dados rapidamente usando uma chave primária como filtro.
- Índice global: pode ser composto por quaisquer campos exceto aqueles do tipo `message` e permite consultar dados rapidamente usando um campo configurado no índice global como filtro.

O TcaplusDB aceita até um índice global e seis índices locais.

### Índice local
Um índice local pode ser definido apenas durante a criação da tabela e pode consistir apenas em campos de chave primária. A interseção de todos os conjuntos de campos de índice não pode estar vazia.
Por exemplo, a tabela `HeroInfo` abaixo possui quatro campos de chave primária: `heroId`, `heroName`, `heroFightingType` e `heroQuality`.
```
{
	heroId:1,
	heroName:"Arthur",
	heroFightingType:1,
	heroQuality:3
	heroSkill:{
		BasicSkill1:1,
		BasicSkill2:2,
		SpecialSkill:3
	},
	heroLevel:12,
	heroskin:2,
	heroAttackpower:141,
	heroPhysicalDefense: 283,
	heroMagicdefense:124
}
{
	heroId:4,
	heroName:"Shooter",
	heroFightingType:3,
	heroQuality:4
	heroSkill:{
		BasicSkill1:1,
		BasicSkill2:2,
		SpecialSkill:3
	},
	heroLevel:11,
	heroskin:1,
	heroAttackpower:225,
	heroPhysicalDefense: 57,
	heroMagicdefense:41
}
```
Para a tabela acima, você pode usar qualquer combinação dos quatro campos de chave primária para criar índices, mas a interseção de todos os índices criados não pode estar vazia. Por exemplo, se `heroId` for usado como o campo de interseção para o design do índice, os seguintes índices podem ser criados:
- heroId,heroName
- heroId,heroFightingType
- heroId,heroQuality
- heroId,heroName,heroFightingType
- heroId,heroFightingType,heroQuality
- heroId,heroName,heroFightingType,heroQuality
Você pode consultar dados por meio dos campos dos índices criados. Crie índices com base nas suas necessidades reais de negócios; caso contrário, o desempenho será comprometido devido à redundância do índice.

### Índice global
Na tabela `HeroInfo` acima, você pode consultar as entradas de dados usando um campo em um índice local criado como um filtro. Por exemplo, se você deseja consultar dados por informações como `heroLevel` e `heroskin`, você pode adicioná-las ao índice global e usar os campos nele para consultar os dados.
Observe que o índice global também não aceita tipos aninhados, como o campo `heroSkill` na tabela de exemplo acima.
