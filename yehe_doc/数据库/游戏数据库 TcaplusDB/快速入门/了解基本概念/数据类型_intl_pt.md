O TencentDB for TcaplusDB aceita tipos de dados do Protocol Buffers.

## Mapeamento entre o proto3 e os tipos de dados em outras linguagens de programação

| .proto | C++ | Java | Python | Go | Ruby | C\# | PHP| Dart | Observações |    
| ------------ | ---------- | ---------- | ----------- | -------- | ---------------- | ---------- | -------------- | --------- | ----------- |
| double       | double     | double     | float       | float64  | float    | double     | float          | double    |     -     |
| float        | float      | float      | float       | float32  | float               | float      | float          | double    |  -  |
| int32        | int32      | int        | int         | int32    | fixnum/<br>bignum<br>(conforme necessário) | int        | integer        | int       | Usa codificação de comprimento variável.<br>Ineficiente para codificação de números negativos. Se é provável que seu campo tenha valores negativos, use o sint32 em vez dele. |
| int64        | int64      | long       | int/long    | int64    | bignum                        | long       | integer/<br>string | Int64     | Usa codificação de comprimento variável.<br>Ineficiente para codificação de números negativos. Se é provável que seu campo tenha valores negativos, use o sint64 em vez dele. |
| uint32       | uint32     | int        | int/long    | uint32   | fixnum/<br>bignum<br>(conforme necessário) | uint       | integer        | int       | Usa codificação de comprimento variável.                                           |
| uint64       | uint64     | long       | int/long    | uint64   | bignum                        | ulong      | integer/<br>string | Int64     | Usa codificação de comprimento variável.                                           |
| sint32       | int32      | int        | int         | int32    | fixnum/<br>bignum<br>(conforme necessário)| int        | integer        | int       | Usa codificação de comprimento variável.                                           |
| sint64       | int64      | long       | int/long    | int64    | bignum                        | long       | integer/<br>string | Int64     | Usa codificação de comprimento variável.<br>Valor int com sinal. Eles codificam números negativos com mais eficiência do que os int32s regulares. |
| fixed32      | uint32     | int        | int/long    | uint32   | fixnum/<br>bignum<br>(conforme necessário)| uint       | integer        | int       | Sempre quatro bytes.<br>Mais eficiente do que o uint32 se os valores forem normalmente maiores do que 2^28.     |
| fixed64      | uint64     | long       | int/long    | uint64   | bignum                        | ulong      | integer/<br>string | Int64     | Sempre oito bytes.<br>Mais eficiente do que o uint64 se os valores forem normalmente maiores do que 2^56.      |
| sfixed32     | int32      | int        | int         | int32    | fixnum/<br>bignum<br>(conforme necessário)| int        | integer        | int       | Sempre quatro bytes.                                             |
| sfixed64     | int64      | long       | int/long    | int64    | bignum                        | long       | integer/<br>string | Int64     | Sempre oito bytes.                                             |
| bool         | bool       | boolean    | bool        | bool     | trueClass/<br>falseClass          | bool       | boolean        | bool      |           -             |
| string       | string     | String     | str/unicode | string   | string<br>(UTF -8)            | string     | string      | string    | Uma string deve sempre conter texto codificado em UTF-8 ou ASCII de 7 bits e não pode ser maior que 2^32. |
| bytes        | string     | ByteString | str         | byte | string<br>(ASCII-8BIT)        | bytestring | string      |  -         | Pode conter qualquer sequência arbitrária de bytes que não seja maior que 2^32.                          |


## Mapeamento entre o proto2 e os tipos de dados em outras linguagens de programação

| .proto | C++ | Java  | Python               | Go   | Observações                       |
| ------------ | ---------- | ---------- | ---------------- | --------- | ---------------------------------- |
| double       | double     | double     | float                                    | \*float64 |   -            |
| float        | float      | float      | float                                    | \*float32 |                -    |
| int32        | int32      | int        | int                                      | \*int32   | Usa codificação de comprimento variável. Ineficiente para codificação de números negativos. Se é provável que seu campo tenha valores negativos, use o sint32 em vez dele. |
| int64        | int64      | long       | int/long                                 | \*int64   | Usa codificação de comprimento variável. Ineficiente para codificação de números negativos. Se é provável que seu campo tenha valores negativos, use o sint64 em vez dele. |
| uint32       | uint32     | int        | int/long                                 | \*uint32  | Usa codificação de comprimento variável.                                           |
| uint64       | uint64     | long       | int/long                                 | \*uint64  | Usa codificação de comprimento variável.                                           |
| sint32       | int32      | int        | int                                      | \*int32   | Usa codificação de comprimento variável. Valor de int com sinal. Eles codificam números negativos com mais eficiência do que os int32s regulares. |
| sint64       | int64      | long       | int/long                                 | \*int64   | Usa codificação de comprimento variável. Valor de int com sinal. Eles codificam números negativos com mais eficiência do que os int64s regulares. |
| fixed32      | uint32     | int        | int/long                                 | \*uint32  | Sempre quatro bytes. Mais eficiente do que o uint32 se os valores forem normalmente maiores do que 2^28.      |
| fixed64      | uint64     | long       | int/long                                 | \*uint64  | Sempre oito bytes. Mais eficiente do que o uint64 se os valores forem normalmente maiores do que 2^56.      |
| sfixed32     | int32      | int        | int                                      | \*int32   | Sempre quatro bytes.                                             |
| sfixed64     | int64      | long       | int/long                                 | \*int64   | Sempre oito bytes.                                             |
| bool         | bool       | boolean    | bool                                     | \*bool    |   -                        |
| string       | string     | String     | unicode(Python 2)<br>ou<br>str(Python 3) | \*string  | Uma string deve sempre conter texto codificado em UTF-8 ou ASCII de 7 bits.                 |
| bytes        | string     | ByteString | bytes                                    | byte  | Pode conter qualquer sequência arbitrária de bytes.                                       |

