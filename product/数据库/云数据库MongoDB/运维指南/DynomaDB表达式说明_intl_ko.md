

DynomaDB는 다음 3가지 식 구문을 지원합니다. ConditionExpression, UpdateExpression, 및 ProjectExpression입니다. Tencent Cloud 데이터베이스와의 호환 상황은 다음과 같습니다.
### ConditionExpression
```
DynamoDBConditionExpression구문은 다음과 같습니다.
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
설명:
1. operand1 comparator operand2 구문에서 operand1은 반드시 속성 필드여야 하며 operand2는 반드시 값 필드여야 합니다. 
2. operand1 BETWEEN operand2 AND operand3 구문에서 operand1은 반드시 속성 필드여야 하며 operand2 및 operand3은 반드시 값 필드여야 합니다. 
3. operand1 IN(operand2(',' operand3(, ...) )) 구문에서, operand1은 반드시 속성 필드여야 하며 operand2와 operand3은 반드시 값 필드여야 합니다.
4. function 구문에서, attribute_exists(path), attribute_not_exists(path), begins_with(path, substr) 및 contains(path, operand)는 완전히 호환됩니다. attribute_type(path, type)는 type->S, N, B, BOOL, NULL을 지원하지만 type->SS, NS, BS, L, M을 지원하지 않습니다. size(path)를 지원하지 않습니다.


### UpdateExpression
```
update-expression 구문은 다음과 같습니다.
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
설명:
[set-action]
1. SET key = value, key는 반드시 속성 필드여야 하며 value는 반드시 값 필드여야 합니다. 
```
SET a =:b    //지원
SET #a = #b  //지원하지 않음
```
2. SET key1 = key2 + value, key1 및 key2는 반드시 속성 필드여야 하며 같은 이름이어야 합니다. value는 반드시 값 필드여야 합니다. 
```
SET a = a + :b //지원
SET a = b + :b //지원하지 않음
```
3. SET key1[NUM] = value, key1는 반드시 속성 필드여야 하며 value는 반드시 값 필드여야 합니다. num은 반드시 음이 아닌 정수야야 합니다.
4. SET key1[NUM] = key2[NUM] + value, 지원하지 않음.
5. SET key1[NUM] = key2[NUM] - value, 지원하지 않음.
6. SET key1 = if_not_exists(key2, value), 지원하지 않음
7. SET key1 = list_append(value, key2), key1과 key2는 반드시 값 유형이어야 하며 같은 이름이어야 합니다. value는 반드시 속성 유형이어야 합니다.
8. SET key1 = list_append(key2, value), key1과 key2는 반드시 값 유형이어야 하며 같은 이름이어야 합니다. value는 반드시 속성 유형이어야 합니다.

[remove-action]
1. REMOVE key, key는 반드시 속성 필드여야 하고 완전히 호환되어야 합니다
2. REMOVE key[NUM], 지원하지 않음.

[delete-action]
1. DELETE key value, key는 반드시 속성 유형이어야 합니다. value는 반드시 값 유형이어야 하고 완전히 호환되어야 합니다

[add-action]
1. ADD key value, key는 반드시 속성 유형이어야 합니다. value는 반드시 값 유형이어야 합니다. 

### ProjectExpression
```
Projec-expression 구문은 다음과 같습니다.
stat ::= sections
sections ::= section, sections
section ::= key|  key[num]
```
설명: 2차원 배열 section ::= key[num][num]를 제외하고 상기 구문을 모두 지원합니다.

