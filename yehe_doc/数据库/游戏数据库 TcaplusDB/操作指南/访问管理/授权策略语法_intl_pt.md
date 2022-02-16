<span id = "clyf"></span>
### Sintaxe da política
Política do CAM:
```
{	 
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"effect", 
              "action":["action"], 
              "resource":["resource"], 
               "condition": {"key":{"value"}} 
           } 
       ] 
} 
```

- A **version (versão)** é obrigatória. Atualmente, apenas o valor "2.0" é permitido.
- A **statement (instrução)** descreve os detalhes de uma ou mais permissões. Esse elemento contém uma permissão ou conjunto de permissões que é composto por outros elementos, como `effect`, `action`, `resource` e `condition`. Cada política tem um elemento de `statement`.
 - O **effect (efeito)** descreve se o resultado produzido pela instrução é "allow (permitir)" ou "deny (negar)". Esse elemento é obrigatório.
 - A **action (ação)** descreve a ação (operação) a ser permitida ou negada. Uma operação pode ser uma API ou um conjunto de funcionalidades (um conjunto de APIs específicas descrito com o prefixo `permid`). Esse elemento é obrigatório.
 - O **resource (recurso)** descreve os objetos que a instrução abrange. Um recurso é descrito em um formato de seis segmentos. As definições detalhadas dos recursos variam de acordo com o produto. Esse elemento é obrigatório.
 - A **condition (condição)** descreve a condição para que a política entre em vigor. Uma condição é composta por operador, chave da ação e valor da ação. Atualmente, o TcaplusDB não aceita condições especiais, portanto, esse item não é configurável. Esse elemento é obrigatório.

<span id = "cz"></span>
### Operações do TcaplusDB
Na instrução de uma política do CAM, você pode especificar qualquer operação de API de qualquer serviço que aceite o CAM. As APIs com o prefixo `name/tcaplusdb:` devem ser usadas para o TcaplusDB, como `name/tcaplusdb:DescribeClusters` ou `name/tcaplusdb:DeleteCluster`.
Para especificar várias operações em uma única instrução, separe-as com vírgulas, conforme mostrado abaixo:
```
"action":["name/tcaplusdb:action1","name/tcaplusdb:action2"]
```

Você também pode especificar várias operações usando um curinga. Por exemplo, você pode especificar todas as operações que começam com "Describe (Descrever)" no nome, conforme mostrado abaixo:
```
"action":["name/tcaplusdb:Describe*"]
```

Se você deseja especificar todas as operações no TcaplusDB, use um caractere curinga "*" conforme mostrado abaixo:
```
"action":["name/tcaplusdb:*"]
```

<span id = "zylj"></span> 
### Caminho de recursos do TcaplusDB

Cada instrução da política do TcaplusDB tem seus próprios recursos.
Geralmente, os caminhos de recursos estão no seguinte formato:

```
qcs:project_id:service_type:region:account:resource
```

O **project_id** descreve as informações do projeto, que são usadas apenas para permitir a compatibilidade com a lógica do CAM legada e podem ser deixadas em branco.
O **service_type** descreve a abreviatura de um produto, como `tcaplusdb`.
A **region (região)** descreve as [informações da região](https://intl.cloud.tencent.com/document/product/213/6091), como ap-shanghai. Se um recurso for especificado, não há necessidade de inserir a `region`.
A **account (conta)** é a conta raiz do proprietário do recurso, como `uin/164xxx472`.
O **resource (recurso)** descreve informações detalhadas sobre os recursos de cada produto, como cluster/19168929215 ou cluster/\* para recurso de cluster, em que o cluster, o grupo de tabelas e a tabela não podem ser autenticados em cascata. Se você deseja controlar o acesso a todas as tabelas ou grupos de tabelas em um cluster especificado, é necessário configurar a autenticação para as tabelas ou grupos de tabelas além do cluster. A tabela a seguir descreve os recursos que podem ser utilizados pelo TcaplusDB e os respectivos métodos de descrição dos recursos.


| Recurso   | Método de descrição de recurso na política de autorização                                     |
| ------ | ------------------------------------------------------------ |
| Cluster    | qcs::tcaplusdb:$region:$account:cluster/$clusterId           |
| Grupo de tabelas | qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId |
| Tabela    | qcs::tcaplusdb:$region:$account:table/$tableId |

Por exemplo, você pode especificar um recurso para um cluster específico (ID do cluster: 19168929215) em uma instrução, conforme mostrado abaixo:
```
"resource":[ "qcs::tcaplusdb:ap-shanghai:uin/164xxx472:cluster/19168929215"]
```

Você também pode usar o caractere curinga "*" para especificá-lo para todos os clusters na região de Xangai que pertencem a uma conta específica, conforme mostrado abaixo:
```
"resource":[ "qcs::tcaplusdb:ap-shanghai:uin/164xxx472:cluster/*"]
```

Se você deseja especificar todos os recursos ou se uma operação específica da API não aceitar o controle de permissão a nível de recurso, você pode usar o caractere curinga "*" no elemento `resource`, conforme mostrado abaixo:
```
"resource": ["*"]
```

Para especificar vários recursos em um único comando, separe-os com vírgulas. Veja abaixo um exemplo em que dois clusters são especificados:
```
"resource":["qcs::tcaplusdb::uin/164xxx472:cluster/19168929215","qcs::tcaplusdb::uin/164xxx472:cluster/21168929215"]
```
