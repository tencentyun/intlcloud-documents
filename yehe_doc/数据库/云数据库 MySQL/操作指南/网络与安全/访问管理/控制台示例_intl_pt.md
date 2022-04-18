
Este documento fornece exemplos sobre como conceder permissões de usuário para visualizar e usar recursos específicos no console do TencentDB usando uma política de CAM.

## Política de acesso total para o TencentDB
Para conceder a um usuário permissões para criar e gerenciar instâncias do TencentDB, você pode implementar a política QcloudCDBFullAccess para o usuário.

Faça login no [console do CAM](https://console.cloud.tencent.com/cam/policy), selecione **Policies (Políticas)** na barra lateral esquerda e pesquise QcloudCDBFullAccess no canto superior direito.
![](https://main.qcloudimg.com/raw/5ec89e71595a5edd3e7f723a19c01a6a.png)
A sintaxe da política é a seguinte:
```
{
    "version": "2.0",
    “statement": [
        {
            "action": [
                "cdb:*"
            ],
            "resource": "*",
            “effect": "allow”
        },
        {
            "action": [
                "vpc:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "cvm:*"
            ],
            "resource": "qcs::cvm:::sg/*",
            "effect": "allow"
        },
        {
            "action": [
                "cos:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "monitor:*",
            "resource": "*"
        },
        {
            "action": [
                "kms:CreateKey",
                "kms:GenerateDataKey",
                "kms:Decrypt",
                "kms:ListKey"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
A política do CAM acima concede ao usuário permissões para usar todos os recursos do TencentDB, VPC, grupos de segurança, COS, KMS e Cloud Monitor.

## Política de permissão somente leitura para o TencentDB
Para conceder a um usuário a permissão para exibir as instâncias do TencentDB, mas não criar, excluir ou modificá-las, você pode implementar a política QcloudCDBInnerReadOnlyAccess para o usuário.

>?Recomenda-se configurar a política somente leitura para o TencentDB.

Faça login no [console do CAM](https://console.cloud.tencent.com/cam/policy), selecione **Policies (Políticas)** na barra lateral esquerda, clique em **Service Type (Tipo de serviço)** na lista de políticas, selecione **TencentDB for MySQL** na lista suspensa e então você verá essa política nos resultados.

A sintaxe da política é a seguinte:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

## Política de permissão somente leitura dos recursos relacionados ao TencentDB
Para conceder a um usuário permissões para visualizar instâncias do TencentDB e recursos relacionados (VPC, grupos de segurança, COS e Cloud Monitor), mas não criá-los, excluí-los ou modificá-los, você pode implementar a política QcloudCDBReadOnlyAccess para o usuário.

Faça login no [console do CAM](https://console.cloud.tencent.com/cam/policy), selecione **Policies (Políticas)** na barra lateral esquerda, clique em **Service Type (Tipo de serviço)** na lista de políticas e selecione **TencentDB for MySQL** na lista suspensa e então você verá essa política nos resultados.

A sintaxe da política é a seguinte:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "vpc:Describe*",
                "vpc:Inquiry*",
                "vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "cvm:DescribeSecurityGroup*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "cos:List*",
                "cos:Get*",
                "cos:Head*",
                "cos:OptionsObject"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "monitor:*",
            "resource": "*"
        }
    ]
}
```
A sintaxe de política de CAM acima concede ao usuário permissões das seguintes operações:
- Todas as operações no TencentDB que começam com "Describe".
- Todas as operações na VPC que começam com "Describe", "Inquiry" ou "Get".
- Todas as operações em grupos de segurança que começam com "DescribeSecurityGroup".
- Todas as operações no COS que começam com "List", "Get" e "Head", bem como a operação "OptionsObject".
- Todas as operações no Cloud Monitor.

## Política para conceder a um usuário permissões para usar APIs fora do nível de recurso
Para conceder a um usuário permissões para usar apenas APIs fora do nível de recurso, você pode implementar a política QcloudCDBProjectToUser para o usuário.
Faça login no [console do CAM](https://console.cloud.tencent.com/cam/policy), selecione **Policies (Políticas)** na barra lateral esquerda, clique em **Service Type (Tipo de serviço)** na lista de políticas, selecione **TencentDB for MySQL** na lista suspensa e então você verá essa política nos resultados.
A sintaxe da política é a seguinte:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:BalanceRoGroupLoad",
                "cdb:CancelBatchOperation",
                "cdb:CreateBatchJobFiles",
                "cdb:CreateDBInstance",
                "cdb:CreateDBInstanceHour",
                "cdb:CreateMonitorTemplate",
                "cdb:CreateParamTemplate",
                "cdb:DeleteBatchJobFiles",
                "cdb:DeleteMonitorTemplate",
                "cdb:DeleteParamTemplate",
                "cdb:DescribeBatchJobFileContent",
                "cdb:DescribeBatchJobFiles",
                "cdb:DescribeBatchJobInfo",
                "cdb:DescribeProjectSecurityGroups",
                "cdb:DescribeDefaultParams",
                "cdb:DescribeMonitorTemplate",
                "cdb:DescribeParamTemplateInfo",
                "cdb:DescribeParamTemplates",
                "cdb:DescribeRequestResult",
                "cdb:DescribeRoGroupInfo",
                "cdb:DescribeRoMinScale",
                "cdb:DescribeTasks",
                "cdb:DescribeUploadedFiles",
                "cdb:ModifyMonitorTemplate",
                "cdb:ModifyParamTemplate",
                "cdb:ModifyRoGroupInfo",
                "cdb:ModifyRoGroupVipVport",
                "cdb:StopDBImportJob",
                "cdb:UploadSqlFiles"
            ],
            "effect": "allow",
            "resource": "*"
        }
    ]
}
```

## Política para conceder a um usuário permissões para manipular uma instância específica do TencentDB
Para conceder a um usuário permissões para manipular um banco de dados específico, você pode associar a seguinte política ao usuário. Por exemplo, a política abaixo permite que o usuário manipule a instância do TencentDB "cdb-xxx" em Guangzhou.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cdb:*",
            "resource": "qcs::cdb:ap-guangzhou::instanceId/cdb-xxx",
            "effect": "allow"
        }
    ]
}
```

## Política para conceder permissões de usuário para manipular instâncias do TencentDB em lotes
Para conceder a um usuário permissões para manipular instâncias do TencentDB em lotes, você pode associar a seguinte política ao usuário. Por exemplo, a política abaixo permite que o usuário manipule as instâncias do TencentDB "cdb-xxx" e "cdb-yyy" em Guangzhou e "cdb-zzz" em Pequim.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cdb:*",
            "resource": ["qcs::cdb:ap-guangzhou::instanceId/cdb-xxx", "qcs::cdb:ap-guangzhou::instanceId/cdb-yyy", "qcs::cdb:ap-beijing::instanceId/cdb-zzz"],
            "effect": "allow"
        }
    ]
}
```

## Política para conceder permissões de usuário para manipular instâncias do TencentDB em uma região específica
Para conceder a um usuário permissões para manipular instâncias do TencentDB em uma região específica, você pode associar a seguinte política ao usuário. Por exemplo, a política abaixo permite que o usuário manipule as instâncias do TencentDB em Guangzhou.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cdb:*",
            "resource": "qcs::cdb:ap-guangzhou::*",
            "effect": "allow"
        }
    ]
}
```

## Políticas personalizadas
Se as políticas predefinidas não atenderem aos seus requisitos, é possível criar políticas personalizadas, conforme mostrado abaixo. Se as permissões forem concedidas por recursos para uma operação de API do TencentDB que não oferece suporte à autorização no nível do recurso, você ainda poderá autorizar um usuário a executá-la, mas deverá especificar `*` como o elemento de recurso na instrução de política.
     
A sintaxe das políticas personalizadas é a seguinte:
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
- Substitua "Action" pela operação a ser permitida ou negada.
- Substitua "Resource” pelos recursos que você deseja autorizar o usuário a manipular.
- Substitua "Effect" por "Allow" ou "Deny".
