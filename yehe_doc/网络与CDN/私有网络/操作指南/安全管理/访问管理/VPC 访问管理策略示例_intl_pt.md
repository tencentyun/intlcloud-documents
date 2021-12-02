## Política de permissão de leitura e gravação completa do VPC
A seguinte política permite criar e gerenciar instâncias do VPC. É possível associar esta política a um grupo de administradores de rede. O elemento `Action (Ação)` especifica todas as APIs relacionadas ao VPC.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/vpc:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
## Política de permissão de somente leitura do VPC
A política a seguir permite que você consulte seu VPC e os recursos relevantes. No entanto, não é possível criar, atualizar ou excluí-los com esta política.
Recomendamos que você conceda a permissão de somente leitura do VPC para os usuários, porque assim eles conseguem visualizar o recurso para operá-lo no console.

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/vpc:Describe*",
                "name/vpc:Inquiry*",
                "name/vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

## Permissão para gerenciar apenas um único VPC por uma subconta
A seguinte política permite que um usuário visualize todas as instâncias do VPC, mas apenas consiga operar o VPC A (por exemplo, o VPC A com um ID de vpc-d08sl2zr) e os recursos de rede no VPC A (como sub-redes e tabelas de rotas, mas excluindo Cloud Virtual Machines (CVMs) e bancos de dados). Em outras palavras, o usuário não tem permissão para gerenciar outras instâncias do VPC.
Esta versão não aceita **permitir que o usuário visualize apenas o VPC A**. Isso será possível em versões futuras.

```
{
    "version": "2.0",
    "statement": [
        {
            "action": "name/vpc:*",
            "resource": "*",
            "effect": "allow",
            "condition": {
                "string_equal_if_exist": {  //Julgamento condicional: apenas instâncias elegíveis podem ser gerenciadas
                    "vpc:vpc": [
                    "vpc-d08sl2zr"
                    ],
                    "vpc:accepter_vpc": [
                     "vpc-d08sl2zr"
                    ],
                     "vpc:requester_vpc": [
                     "vpc-d08sl2zr"
                    ]
                }
            }
        }
    ]
}
```

## Permissão para um usuário gerenciar instâncias do VPC, exceto operar tabelas de rotas
A seguinte política permite que um usuário leia e grave instâncias do VPC e recursos relevantes, mas não permite que o usuário opere tabelas de rotas.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/vpc:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "name/vpc:AssociateRouteTable",
                "name/vpc:CreateRoute",
                "name/vpc:CreateRouteTable",
                "name/vpc:DeleteRoute",
                "name/vpc:DeleteRouteTable",
                "name/vpc:ModifyRouteTableAttribute"
            ],
            "resource": "*",
            "effect": "deny"
        }
    ]
}
```

## Permissão para um usuário gerenciar recursos do VPN
A seguinte política permite que um usuário visualize todos os recursos do VPC, mas permite apenas que o usuário crie, leia, atualize e exclua os recursos do VPN (CRUD).

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/vpc:Describe*",
                "name/vpc:Inquiry*",
                "name/vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "name/vpc:*Vpn*",
                "name/vpc:*UserGw*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
