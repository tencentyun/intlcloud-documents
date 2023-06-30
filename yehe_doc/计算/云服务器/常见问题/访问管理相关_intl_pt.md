### Como posso criar uma política personalizada?

Se as políticas predefinidas não atenderem aos seus requisitos, você poderá criar uma política personalizada.
A sintaxe de uma política personalizada é a seguinte:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "Action"
            ],
            "resource": "Resource",
            "effect": "Effect"
        }
    ]
}
```

- Action (Ação): substitua pela operação a ser permitida ou negada.
- Resource (Recurso): substitua-o pelos recursos que deseja autorizar.
- Effect (Efeito): substitua por “Allow (Permitir)” ou “Deny (Negar)”.

### Como devo configurar a política somente leitura para uma CVM?

Para permitir que um usuário consulte as instâncias da CVM, mas não crie, exclua, inicie ou desligue as instâncias, ative a política QcloudCVMInnerReadOnlyAccess.

Para isso, faça login no Console do CAM. Na página [Políticas](https://console.cloud.tencent.com/cam/policy), procure a **CVM** para localizar a política.

A sintaxe da política é a seguinte:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:Describe*",
                "name/cvm:Inquiry*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

A política acima **concede aos usuários permissões para realizar as seguintes operações**:

- Todas as operações iniciadas por “Describe (Descrever)” na CVM.
- Todas as operações iniciadas por “Inquiry (Consultar)” na CVM.

### Como posso configurar a política somente leitura para os recursos relacionados à CVM?

Para permitir que um usuário consulte instâncias da CVM e os recursos relevantes (instâncias do VPC e do CLB), mas não crie, exclua, inicie ou desligue as instâncias e os recursos relevantes, habilite a política QcloudCVMReadOnlyAccess.

Para isso, faça login no Console do CAM. Na página [Políticas](https://console.cloud.tencent.com/cam/policy), procure a **CVM** para localizar a política.

A sintaxe da política é a seguinte:

```
 {
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:Describe*",
                "name/cvm:Inquiry*"
            ],
            "resource": "*",
            "effect": "allow"
        },
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
                "name/clb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "name/monitor:*",
            "resource": "*"
        }
    ]
}
```

A política acima **concede aos usuários permissões para realizar as seguintes operações**:

- Todas as operações iniciadas por "Describe (Descrever)" e "Inquiry (Consultar)" na CVM.
- Todas as operações iniciadas por "Describe (Descrever)", "Inquiry (Consultar)" e "Get (Obter)" no VPC.
- Todas as operações iniciadas por "Describe (Descrever)" no CLB.
- Todas as operações no Monitor.

