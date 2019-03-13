

DynomaDBはConditionExpression、UpdateExpression、ProjectExpressionをサポートします。TencentDBとの互換性は以下のように
### ConditionExpression
```
DynamoDBConditionExpression構文は次のとおりです。
condition-expression ::=
    | operand comparator operand
    | operand BETWEEN operand AND operand
    | operand IN ( operand (',' operand (, ...) ))
    | function 
    | condition AND condition 
    | condition OR condition
    | NOT condition 
    | ( condition )

comparator ::=
    | = 
    | <>
    | <
    | <= 
    | >
    | >=

function ::=
    | attribute_exists (path) 
    | attribute_not_exists (path) 
    | attribute_type (path, type) 
    | begins_with (path, substr) 
    | contains (path, operand)
    | size (path)

```
説明：
1.operand1 comparator operand2の構文では、operand1が属性フィールド、operand2は値フィールドでなければなりません 
2.operand1 BETWEEN operand2 AND operand3の構文では、operand1は属性フィールド、operand2とoperand3は値フィールドでなければなりません 
3.operand1 IN ( operand2 (',' operand3 (, ...) ))の構文では、operand1は属性フィールド、operand2とoperand3は値フィールドでなければなりません
4.functionの構文では、attribute_exists (path)、attribute_not_exists (path)、begins_with (path, substr)、contains (path, operand)と完全に互換性があります。attribute_type (path, type)はtype->S,N, B, BOOL,NULLをサポートしますが、type->SS, NS, BS, L,Mをサポートしません。size (path)をサポートしません


### UpdateExpression
```
update-expression構文は次のとおりです。
update-expression ::=
    | SET set-action , ... 
    | REMOVE remove-action , ...  
    | ADD add-action , ... 
    | DELETE delete-action , ...

set-action ::=
path = value

value ::=
    | operand
    | operand '+' operand 
    | operand '-' operand

operand ::=
path | function

remove-action ::=
path

add-action ::=
path value

delete-action ::=
path value 

function ::=
if_not_exists (path, operand) | list_append (operand, operand)
```
説明：
[set-action]
1.SET key = value、keyは属性フィールド、valueは値フィールドでなければなりません 
```
SET a =:b    //対応
SET #a = #b  //未対応
```
2.SET key1 = key2 + value、key1とkey2は属性フィールド、かつkey1とkey2の名前が同じで、valueは値フィールドでなければなりません 
```
SET a = a + :b //対応
SET a = b + :b //未対応
```
3.SET key1[NUM] = value、key1は属性フィールド、valueは値フィールド、numは非負整数でなければなりません
4.SET key1[NUM] = key2[NUM] + value、未対応
5.SET key1[NUM] = key2[NUM] - value、未対応
6.SET key1 = if_not_exists(key2, value)、未対応
7.SET key1 = list_append(value, key2)、key1とkey2は値タイプかつkey1とkey2の名前が同じ、valueは属性タイプでなければなりません
8.SET key1 = list_append(key2, value)、key1とkey2は値タイプかつkey1とkey2の名前が同じ、valueは属性タイプでなければなりません

[remove-action]
1.REMOVE key、keyは属性フィールドでなければなりません。完全な互換性があります
2.REMOVE key[NUM]、未対応

[delete-action]
1.DELETE key value、keyは属性タイプ、valueは値タイプでなければなりません。完全な互換性があります

[add-action]
1.ADD key value、keyは属性タイプ、valueは値タイプでなければなりませ 

### ProjectExpression
```
Projec-expression 構文は次のとおりです。
stat ::= sections
sections ::= section, sections
section ::= key|  key[num]
```
説明：2次元配列section ::= key[num][num]を除き、以上の構文をサポートします

