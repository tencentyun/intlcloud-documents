## Index Overview
You can create an index for a table and use it to quickly get desired data from a database, which delivers higher flexibility in data query for your application.

TcaplusDB supports two types of indexes:
- Local index: it must be composed of primary key fields and allows you to quickly query data by using a primary key as a filter.
- Global index: it can be composed of any fields except those in `message` type and allows you to quickly query data by using a field configured in the global index as a filter.

TcaplusDB supports up to 1 global index and 6 local indexes.

### Local index
A local index can be defined only during table creation and can consist of only primary key fields. The intersection of all index field sets cannot be empty.
For example, the `HeroInfo` table below has 4 primary key fields: `heroId`, `heroName`, `heroFightingType`, and `heroQuality`.
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
For the table above, you can use any combination of the 4 primary key fields to create indexes, but the intersection of all created indexes cannot be empty. For example, if `heroId` is used as the intersection field for index designing, the following indexes can be created:
- heroId,heroName
- heroId,heroFightingType
- heroId,heroQuality
- heroId,heroName,heroFightingType
- heroId,heroFightingType,heroQuality
- heroId,heroName,heroFightingType,heroQuality
You can query data by the fields in the created indexes. Please create indexes based on your actual business needs; otherwise, the performance will be compromised due to index redundancy.

### Global index
In the `HeroInfo` table above, you can query data entries by using a field in a created local index as a filter. For example, if you want to query data by information such as `heroLevel` and `heroskin`, you can add them to the global index and use the fields in it to query data.
Please note that the global index does not support nested types either, such as the `heroSkill` field in the sample table above.
