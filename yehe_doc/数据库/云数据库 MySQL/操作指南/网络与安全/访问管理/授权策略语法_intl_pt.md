<span id = "celueyufa"></span>
## Sintaxe da política
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
- A **version (versão)** é obrigatória. Atualmente, apenas a "2.0" é permitida.
- A **statement (instrução)** descreve os detalhes de uma ou mais permissões. Esse elemento contém uma permissão ou conjunto de permissões que é composto por outros elementos, como efeito, ação, recurso e condição. Cada política tem apenas um elemento de instrução.
 4. O **effect (efeito)** descreve se o resultado produzido pela instrução é "allowed (permitido)" ou "denied (negado)". Este elemento é obrigatório.
 - A **action (ação)** descreve a ação (operação) a ser permitida ou negada. Uma operação pode ser uma API (com o prefixo  "cdb:”). Esse elemento é obrigatório.
 - O **resource (recurso)** descreve os detalhes da autorização. Um recurso é descrito em um formato de seis segmentos. As definições detalhadas dos recursos variam de acordo com o produto. Esse elemento é obrigatório.
 3. A **condition (condição)** descreve a condição para que a política entre em vigor. Uma condição é composta por um operador, uma chave da ação e um valor da ação. Um valor da condição pode conter informações, como a hora e o endereço IP. Alguns serviços permitem que você especifique valores adicionais em uma condição. Esse elemento é obrigatório.

<span id = "caozuo"></span>
## Operações do TencentDB
Na instrução de uma política do TencentDB, você pode especificar qualquer ação de API de qualquer serviço que aceite o TencentDB. APIs prefixadas com "cdb:" devem ser usadas para TencentDB, como cdb:CreateDBInstance ou cdb:CreateAccounts.

Para especificar várias operações em uma única instrução, separe-as com vírgulas, conforme mostrado abaixo:
```
"action":["cdb:action1","cdb:action2"]
```
Você também pode especificar várias operações usando um curinga. Por exemplo, você pode especificar todas as operações que começam com "Describe (Descrever)" no nome, conforme mostrado abaixo:
```
"action":["cdb:Describe*"]
```
Se você deseja especificar todas as operações no TencentDB, use um caractere curinga conforme mostrado abaixo:
```
"action":["cdb:*"]
```

<span id = "ziyuanlujing"></span> 
## Recursos do TencentDB
Cada instrução da política do CAM tem seus próprios recursos.
Geralmente, os recursos estão no seguinte formato:
```
qcs:project_id:service_type:region:account:resource
```
- **project_id** descreve as informações do projeto, usado apenas para permitir a compatibilidade com a lógica do CAM legada e pode ser deixado em branco.
- **service_type** descreve a abreviatura de um produto, tal como COS.
- **region** descreve as informações da região, como ap-guangzhou.
- **account** é a conta raiz do proprietário do recurso, como uin/653339763.
- **resource** descreve informações detalhadas de recursos de cada produto, como instanceId/instance_id1 ou instanceId/*.


Por exemplo, você pode definir um recurso para uma instância específica (cdb-k05xdcta) na instrução da seguinte maneira:
```
“resource":[ "qcs::cdb:ap-guangzhou:uin/653339763:instanceId/cdb-k05xdcta"]
```
Você também pode usar o caractere curinga "*" para definir o recurso para todas as instâncias que pertencem a uma conta específica, conforme mostrado abaixo:
```
“resource":[ "qcs::cdb:ap-guangzhou:uin/653339763:instanceId/*"]
```
Se você deseja especificar todos os recursos ou uma operação de API específica não oferece compatibilidade com o controle de permissão no nível do recurso, você pode usar o caractere curinga "*" no elemento "resource" conforme mostrado abaixo:
```
"resource": ["*"]
```
Para especificar vários recursos em um único comando, separe-os com vírgulas. Veja abaixo um exemplo em que dois recursos são especificados:
```
"resource":["resource1","resource2"]
```

A tabela abaixo descreve os recursos que podem ser usados pelo TencentDB e os métodos de descrição de recursos correspondentes, onde as palavras prefixadas com $ são espaços reservados, `region` refere-se a uma região e `account` refere-se a um ID de conta.

| Recurso  | Método de descrição de recurso na política de autorização |
|-------|-------|
| Instância |  `qcs::cdb:$region:$account:instanceId/$instanceId`|
|VPC|  `qcs::vpc:$region:$account:vpc/$vpcId`|
| Grupo de segurança | qcs::cvm:$region:$account:sg/$sgId |
