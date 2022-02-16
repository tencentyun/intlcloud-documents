O TencentDB for TcaplusDB é compatível com duas linguagens de definição de tabela:  o Protocol Buffers (Protobuf) e a representação de dados de Tencent (TDR). O Protobuf é um método de serialização de dados estruturados desenvolvido pelo Google, que enfatiza a simplicidade e o desempenho. O TDR é uma linguagem de descrição de dados neutra em relação à plataforma e desenvolvida pela Tencent, que combina as vantagens do XML, linguagem binária e mapeamento objeto-relacional (ORM); é amplamente utilizado em cenários de serialização de dados de jogos da Tencent. Ambas as linguagens são igualmente vantajosas. Use qualquer uma delas de acordo com as suas preferências. Este documento descreve como definir tabelas no Protobuf.

## Definição de tabelas no Protobuf
Para criar uma tabela no TcaplusDB, primeiro é necessário usar uma linguagem de descrição de tabela para definir o formato da tabela e gravar o conteúdo de definição da tabela em um arquivo de descrição IDL da tabela.
O arquivo de descrição IDL da tabela define a tabela com base nas regras do Protocol Buffers.
As informações de definição são divididas basicamente em três tipos:
- Informações de definição de arquivo
- Informações de definição de tabela
- Informações de tipo aninhado

## Definição de arquivo
A área de informações de definição de arquivo define principalmente as informações comuns do arquivo de descrição da tabela atual, que contém os três tipos de conteúdo a seguir:

| Nome da opção | Descrição | Valor de amostra | Obrigatório |
| --- | --- | --- | --- |
| syntax | Especifica a versão da especificação de sintaxe para gravar o arquivo atual. | proto2, proto3 | Sim |
| package | Especifica o nome do pacote personalizado do arquivo atual, o que ajuda a evitar conflitos de nome com mensagens. | Informações do nome do pacote | Sim |
| importIt | Indica algumas informações comuns importadas para a tabela do TcaplusDB, que devem ser importadas na definição da tabela. | tcaplusservice.optionv1.proto | Sim |


## Definição de tabela

Nas informações de definição da tabela, o formato da tabela (incluindo informações estendidas e informações de campos) é definido em uma mensagem.
#### Definição de informações estendidas
As informações de definição da tabela podem ser estendidas por `option (opção)` com base na sintaxe do Protobuf, que pode implementar funcionalidades semânticas mais avançadas. O conteúdo definível é mostrado abaixo:
O formato de definição detalhada é `option(tcaplusservice.option) = "value";`.

| Nome da opção | Descrição | Exemplo de configuração | Obrigatório |
| --- | --- | --- | --- |
| tcaplus_primary_key | Define o campo de chave primária da tabela do TcaplusDB. | option(tcaplusservice.tcaplus_primary_key) = "uin,name,region"; | Sim |
| tcaplus_index | Define o campo da chave do índice da tabela do TcaplusDB. | option(tcaplusservice.tcaplus_index) = "index_1(uin,region)"; | Não |
| tcaplus_sharding_key | Você pode personalizar o shardkey da tabela. | option(tcaplusservice.tcaplus_sharding_key) = "uin"; | Não |
| tcaplus_field_cipher_suite | É necessário se a funcionalidade de criptografia de campo for usada. Para especificar seu algoritmo de criptografia personalizado, consulte o exemplo na documentação da API. | option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; | Não |
| tcaplus_cipher_md5 | O MD5 (usado para criptografar a string de senha, que é armazenada no usuário) deve ser definido se a funcionalidade de criptografia de campo for usada. | option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; | Não |

#### Definição de informações de campos

O formato de definição de campo do TcaplusDB é `field modifier field type field name = identifier[special definition];`.
##### Modificador de campo
O proto2 aceita três modificadores de limitação, já o proto3 não aceita mais o modificador `REQUIRED` e usa o `OPTIONAL` como o modificador padrão.
- REQUIRED (OBRIGATÓRIO): indica que este campo é obrigatório. No proto2, os campos de chave primária devem ser declarados com `REQUIRED`.
- OPTIONAL (OPCIONAL): indica que este campo é opcional. Você pode definir um valor padrão para um campo opcional.
- REPEATED (REPETIDO): indica que este campo pode conter de 0 a N elementos. Suas funcionalidades são iguais às do `OPTIONAL`, mas pode conter vários valores ao mesmo tempo, que podem ser considerados como uma matriz. A definição especial de `[packed = true]` deve ser especificada.

##### Tipo de campo
O TcaplusDB aceita campos gerais e campos aninhados. Para obter mais informações, consulte os [Tipos de dados](https://intl.cloud.tencent.com/document/product/1016/38659).
##### Nome do campo
Você pode nomear um campo de acordo com seu atributo vigente. O nome pode conter letras, dígitos e sublinhados e não pode começar com um dígito. É recomendável usar minúsculas concatenadas para o nome.
##### Identificador
Intervalo de valores do identificador: [1, 2^29 - 1]
Os identificadores dentro de [19000, 19999] não podem ser usados, pois são reservados no Protocol Buffers. Caso use algum deles, um erro será gerado.
Cada campo ocupará memória ao ser codificado, e o tamanho da memória ocupada está sujeito ao identificador:
- Um campo com um identificador dentro de [1, 15] ocupa 1 byte durante a codificação.
- Um campo com um identificador dentro de [16, 2047] ocupa 2 bytes durante a codificação.
##### Definição especial
- Você pode usar `packed=true` para especificar um campo declarado com o modificador `REPEATED`. A descrição da sintaxe é:
```
repeated int64 lockid = 6 [packed = true]; 
```
- Você pode usar `default = 1` para especificar o valor padrão para um campo declarado com o modificador `OPTIONAL`. A descrição da sintaxe é:
```
optional int32 logintime = 5 [default = 1];
```
- Você pode especificar os campos em tipos de string e bytes como campos criptografados. A descrição da sintaxe é:
```
required string name = 2[(tcaplusservice.tcaplus_crypto) = true];
```

#### Informações de tipo aninhado
O TcaplusDB aceita tipos aninhados. Um tipo aninhado pode conter outro como seu campo. Você também pode definir um novo tipo aninhado em outro.
Semelhante à definição da tabela, a definição do tipo aninhado também é declarada com uma mensagem, mas a estrutura do tipo aninhado não pode conter definições de informações estendidas, como "primary key (chave primária)" e "index (índice)".
O TcaplusDB aceita até 128 níveis de aninhamento consecutivo; no entanto, não é recomendável usar uma grande quantidade de níveis de aninhamento, pois isso comprometerá o desempenho do acesso aos dados.

## Código de exemplo para o arquivo de descrição de tabela no proto2

Veja abaixo um arquivo de descrição de tabela em conformidade com a especificação de sintaxe do proto2:

```
syntax = "proto2";                      // Indica a conformidade com a especificação de sintaxe do proto2.
package myTcaplusTable;                 // Nome do pacote personalizado

import "tcaplusservice.optionv1.proto"; // Define algumas informações comuns da tabela TcaplusDB, que devem ser importadas em sua definição de tabela.

message player {  // Usa uma message para definir a tabela e o nome da message é o nome da tabela.

    // Somente a message para a qual a opção de chave primária (tcaplusservice.tcaplus_primary_key) é especificada pode ser reconhecida como uma tabela de dados de negócios TcaplusDB. Caso contrário, a message é apenas uma estrutura.
    // A opção de chave primária especifica a lista de nomes de campo de chave primária separados por vírgulas. Até quatro campos podem ser especificados como chaves primárias.
    option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";

    // Usa a opção "tcaplusservice.tcaplus_index" para especificar o índice TcaplusDB.
    // As chaves de índice incluídas em cada índice devem ser chaves primárias e a interseção de todos os conjuntos de campos de índice não pode estar vazia.
    option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";
    option(tcaplusservice.tcaplus_index) = "index_2(uin,name)";

    // "option(tcaplusservice.tcaplus_sharding_key) = "uin";". Você pode definir explicitamente o campo de fragmentação do índice. Se você não definir explicitamente, o sistema usará um campo de chave primária como o campo de fragmentação por padrão.

    option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; // Usa a função de criptografia padrão "DefaultAesCipherSuite". Esse parâmetro é opcional.
    option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; // Define o valor MD5 da string de senha de criptografia. Esse parâmetro é opcional.

    // A seguir mostra a definição de campos de tabela.
    // Uma tabela TcaplusDB suporta os seguintes tipos de dados:
    // Tipos aninhados: int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, bytes
    // Tipo aninhado: message
    // TcaplusDB aceita três modificadores de campo: REQUIRED, OPTIONAL e REPEATED.

    // (Até quatro) campos de chave primária
    required int64 uin = 1;  // Os campos de chave primária devem ser declarados com o modificador REQUIRED. Tipos de dados aninhados não são compatíveis.
    required string name = 2[(tcaplusservice.tcaplus_crypto) = true]; // Os campos do tipo string e do tipo bytes em uma message podem ser especificados como campos criptografados. Esse parâmetro é opcional.
    required int32 region = 3;
    // Uma tabela pode conter até quatro campos de chave primária.

    // Campo de valor geral.
    required int32 gamesvrid = 4; // Campos gerais podem ser declarados com os modificadores REQUIRED, OPTIONAL e REPEATED.
    optional int32 logintime = 5 [default = 1];
    repeated int64 lockid = 6 [packed = true]; // A opção "packed=true" deve ser especificada para os campos declarados com o modificador REPEATED.
    optional bool is_available = 7 [default = false]; // Você pode especificar um valor padrão para um campo OPTIONAL.
    optional pay_info pay = 8; // Os campos de valor podem estar em tipos de estrutura personalizados.
}

message pay_info { // Usa uma message para definir a estrutura.

    required int64 pay_id = 1;
    optional uint64 total_money = 2;
    optional uint64 pay_times = 3;
    optional pay_auth_info auth = 4;

    message pay_auth_info { // Os tipos de estrutura suportam definição aninhada.
        required string pay_keys = 1;
        optional int64 update_time = 2;
    }
}
```


## Código de exemplo para o arquivo de descrição de tabela no proto3
Veja abaixo um arquivo de descrição de tabela em conformidade com a especificação de sintaxe do proto3:
```
syntax = "proto3";                      // Indica a conformidade com a especificação de sintaxe do proto3.
package myTcaplusTable;                 // Nome do pacote personalizado

import "tcaplusservice.optionv1.proto"; // Define algumas informações comuns da tabela TcaplusDB, que devem ser importadas em sua definição de tabela.

message player {  // Usa uma message para definir a tabela e o nome da message é o nome da tabela.

    // Somente a message para a qual a opção de chave primária (tcaplusservice.tcaplus_primary_key) é especificada pode ser reconhecida como uma tabela de dados de negócios TcaplusDB. Caso contrário, a message é apenas uma estrutura.
    // A opção de chave primária especifica a lista de nomes de campo de chave primária separados por vírgulas. Até quatro campos podem ser especificados como chaves primárias.
    option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";

    // Usa a opção "tcaplusservice.tcaplus_index" para especificar o índice TcaplusDB.
    // As chaves de índice incluídas em cada índice devem ser chaves primárias e a interseção de todos os conjuntos de campos de índice não pode estar vazia.
    option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";
    option(tcaplusservice.tcaplus_index) = "index_2(uin,name)";

    // "option(tcaplusservice.tcaplus_sharding_key) = "uin";". Você pode definir explicitamente o campo de fragmentação. Se você não definir explicitamente, o sistema usará um campo de chave primária como o campo de fragmentação por padrão.

    option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; // Usa a função de criptografia padrão "DefaultAesCipherSuite". Esse parâmetro é opcional.
    option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; // Define o valor MD5 da string de senha de criptografia. Esse parâmetro é opcional.

    // A seguir mostra a definição de campos de tabela.
    // Uma tabela TcaplusDB suporta os seguintes tipos de dados:
    // Tipos aninhados: int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, bytes
    // Tipo aninhado: message

    // (Até quatro) campos de chave primária
    int64 uin = 1;  // Os campos de chave primária devem estar em tipos não aninhados.
    string name = 2[(tcaplusservice.tcaplus_crypto) = true]; // Os campos do tipo string e do tipo bytes em uma message podem ser especificados como campos criptografados. Esse parâmetro é opcional.
    int32 region = 3;
    // Uma tabela pode conter até quatro campos de chave primária.

    // Campo de valor geral.
    int32 gamesvrid = 4;
    int32 logintime = 5;
    int64 lockid = 6;
    bool is_available = 7;
    pay_info pay = 8; // Os campos de valor podem estar em tipos de estrutura personalizados.
}

message pay_info { // Usa uma message para definir a estrutura.

    int64 pay_id = 1;
    uint64 total_money = 2;
    uint64 pay_times = 3;
    pay_auth_info auth = 4;

    message pay_auth_info { // Os tipos de estrutura suportam definição aninhada.
        string pay_keys = 1;
        int64 update_time = 2;
    }
}
```