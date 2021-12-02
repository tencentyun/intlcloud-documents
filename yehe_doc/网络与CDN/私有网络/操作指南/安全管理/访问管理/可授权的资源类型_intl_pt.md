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

- a **version (versão)** é obrigatória. Atualmente, apenas o valor "2.0" é permitido.
- a **statement (instrução)** descreve os detalhes de uma ou mais permissões. Esse elemento contém uma permissão ou conjunto de permissões que é composto por outros elementos, como efeito, ação, recurso e condição. Cada política tem um elemento de instrução.
 1. **action (ação)** descreve a ação a ser permitida ou negada. Uma ação pode ser uma API (descrita com o prefixo "name") ou um conjunto de funcionalidades (um conjunto de APIs específicas descrito com o prefixo "permid"). Esse elemento é obrigatório.
 2. **resource (recurso)** descreve os detalhes da autorização. Um recurso é descrito em um formato de seis partes. As definições detalhadas dos recursos variam de acordo com o produto. Para obter mais informações sobre como especificar um recurso, consulte a documentação do produto cujos recursos você está escrevendo uma instrução. Esse elemento é obrigatório.
 3. A **condition (condição)** descreve a condição para que a política entre em vigor. Uma condição é composta por um operador, uma chave da ação e um valor da ação. Um valor da condição pode conter informações, como a hora e o endereço IP. Alguns serviços permitem que você especifique valores adicionais em uma condição. Esse elemento é opcional.
 4. O **effect (efeito)** descreve se o resultado produzido pela instrução é "allow (permitir)" ou "deny (negar)". Este elemento é obrigatório.

## Operações do VPC
Na instrução de uma política do CAM, você pode especificar qualquer ação de API de qualquer serviço que aceite o CAM. Para o VPC, use APIs com o prefixo "name/vpc:", por exemplo, name/vpc:Describe ou name/vpc:CreateRoute.
Para especificar várias ações em uma única instrução, separe-as com vírgulas, conforme mostrado abaixo:
```
"action":["name/vpc:action1","name/vpc:action2"]
```

2. Você também pode especificar várias ações usando um caractere curinga. Por exemplo, você pode especificar todas as ações cujos nomes começam com "Describe", conforme mostrado abaixo:
```
"action":["name/vpc:Describe*"]
```

Para especificar todas as ações no VPC, use o caractere curinga "*" da seguinte forma:
```
"action": ["name/vpc:*"]
```

## Caminhos de recursos do VPC
Cada instrução da política do CAM tem seus próprios recursos.
O formato geral de um caminho de recursos é o seguinte:
```
****qcs**:project_id:service_type:region:account:resource**
```

- **project_id**: informações do projeto. Este elemento é usado apenas para permitir a compatibilidade com a lógica do CAM legada e pode ser deixado em branco.
- **service_type**: abreviatura de um produto, como VPC.
-**region**: informações da região, como bj.
- **account**: a conta raiz do proprietário do recurso, como uin/164256472.
- **resource**: detalhes de recursos de cada produto, como vpc/vpc_id1 ou vpc/*.

Por exemplo, você pode especificar uma instância (vpc-d08sl2zr neste caso) na instrução, conforme mostrado abaixo:
```
"resource":[ "qcs::vpc:bj:uin/164256472:instance/vpc-d08sl2zr"]
```

Você também pode usar o caractere curinga "*" para definir todas as instâncias de uma conta específica, conforme mostrado abaixo:
```
"resource":[ "qcs::vpc:bj:uin/164256472:instance/*"]
```

Para especificar todos os recursos ou se alguma ação da API não for compatível com permissões em nível de recurso, você pode usar o caractere curinga "*" no elemento de recurso, conforme mostrado abaixo:
```
"resource": ["*"]
```

Para especificar vários recursos em uma instrução, separe-os com vírgulas. No exemplo a seguir, dois recursos foram especificados:
```
"resource":["resource1","resource2"]
```


A tabela a seguir descreve os recursos que podem ser usados pelo VPC e os métodos correspondentes para descrever esses recursos.

Na tabela abaixo, as palavras prefixadas com "$" são nomes alternativos.
- `project` indica o ID do projeto.
- `region` indica a região.
- `account` indica o ID da conta.

| Recurso | Método de descrição de recursos na política de autorização |
| ------ | ------------------------------------------ |
| VPC | qcs::vpc:$region:$account:vpc/$vpcId |
| Sub-rede | qcs::vpc:$region:$account:subnet/$subnetId |
| Grupo de segurança | qcs::cvm:$region:$account:sg/$sgId |
| EIP | qcs::cvm:$region:$account:eip/* |
