O TencentDB for TcaplusDB é compatível com duas linguagens de definição de tabela: o Protocol Buffers (Protobuf) e a representação de dados de Tencent (TDR).
O Protobuf é um método de serialização de dados estruturados desenvolvido pelo Google, que enfatiza a simplicidade e o desempenho.
O TDR é uma linguagem de descrição de dados neutra em relação à plataforma e desenvolvida pela Tencent, que combina as vantagens do XML, linguagem binária e mapeamento objeto-relacional (ORM); é amplamente utilizado em cenários de serialização de dados de jogos da Tencent.
Ambas as linguagens são igualmente vantajosas. Use qualquer uma delas de acordo com as suas preferências.
Este documento descreve como definir tabelas no TDR.

## Definição de tabela no TDR

O TDR aceita tabelas GENERIC e tabelas LIST. As tabelas GENERIC representam os atributos de elementos na forma de tabelas, como alunos, empregadores e jogadores. As tabelas LIST são uma lista de registros, tais como placares de líderes de jogos e e-mails dentro do jogo (geralmente os últimos 100 e-mails).

Você pode criar diferentes tipos de tabelas em um arquivo XML.

## Definição de tabela
- O elemento `metalib` é o elemento raiz dos arquivos XML.
- O atributo `tagsetversion` deve ser um.
- O elemento `struct` com o atributo `primarykey` precisa ser definido como uma tabela, do contrário será apenas uma estrutura.
- Cada vez que a estrutura da tabela é alterada, o atributo de versão precisa ser incrementado em 1. O valor inicial do atributo de versão é sempre 1.
- O atributo `primarykey` é usado para especificar o campo de chave primária. Uma tabela GENERIC aceita até quatro campos de chave primária e uma tabela LIST aceita até três.
- O atributo `splittablekey` funciona como uma shardkey para fragmentar uma tabela do TcaplusDB em vários fragmentos e armazená-los em vários nós. O `splittablekey` deve ser um dos campos de chave primária. Como um `splittablekey` altamente discreto tem melhor desempenho e uma ampla faixa de valores, recomendamos uma STRING `splittablekey`.
- O atributo `desc` descreve o elemento.
- O elemento `entry` define um campo. Valores válidos: int32, string, char, int64, double, short.
- O elemento `index` define um índice que deve conter o `splittablekey`. Como a chave primária pode ser usada para consultar tabelas, o índice deve ter um atributo diferente da chave primária.

## Código de exemplo para o arquivo de descrição de tabela no TDR

```
<?xml version="1.0" encoding="utf-8" standalone="yes" ?>
 
<metalib name="tcaplus_tb" tagsetversion="1" version="1">
 
  <!-- generic_table `users`, store the user' information -->
  <!-- an user may has many roles -->
  <struct name="users" version="1" primarykey="user_id,username,role_id" splittablekey="user_id" desc="user table">
    <entry name="user_id" type="uint64" desc="user id"/>
    <entry name="username" type="string" size="64" desc="login username"/>
    <entry name="role_id" type="int32" desc="a user can have multiple roles"/>
 
    <entry name="level" type="int32" defaultvalue="1" desc="role's level"/>
    <entry name="role_name" type="string" size="1024" desc="role's name"/>
    <entry name="last_login_time" type="string" size="64" defaultvalue="" desc="user login timestamp"/>
    <entry name="last_logout_time" type="string" size="64" defaultvalue="" desc="user logout timestamp"/>
 
    <index name="index1" column="user_id"/>
  </struct>
 
  <!-- list_table `mails`, store the role's mails -->
  <struct name="mails" version="1" primarykey="user_id,role_id" desc="mail table">
    <entry name="user_id" type="uint64" desc="user id"/>
    <entry name="role_id" type="int32" desc="a user may has many roles"/>
 
    <entry name="text" type="string" size="2048" desc="mail text"/>
    <entry name="send_time" type="string" size="64" defaultvalue="" desc="timestamp of the mail sent"/>
    <entry name="read_time" type="string" size="64" defaultvalue="" desc="timestamp of the mall read"/>
  </struct>
 
</metalib>
```
Além disso, você pode usar `union` para criar dados de tipo aninhado.

O elemento `union` define um tipo simples como uma coleção (união) de valores de tipos de dados simples especificados, como INT e STRING. Você pode usar o `union` como um tipo de dados personalizado.
A tag `Macro` é usada para definir constantes.

```
<macro name="DB_MAX_USER_MSG_LEN" value="301" desc="Max length of the message that user can define"/>
 <union name="DBPlayerMsg" version="1" desc="DB Player message">
   <entry name="SysMsgID"     type="uint8"         desc="Message ID" />
   <entry name="UsrMsg"       type="string"        size="DB_MAX_USER_MSG_LEN"   desc="player created message" />
 </union>
```