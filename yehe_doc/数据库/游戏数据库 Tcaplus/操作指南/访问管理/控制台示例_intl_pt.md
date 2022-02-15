## Cenários de operação
Você pode conceder a um usuário a permissão para exibir e usar recursos específicos no console do TcaplusDB usando uma política do CAM. Este documento descreve como conceder permissão para exibir e usar recursos especificados, mostrando como usar algumas políticas no console.


## Instruções
### Política de acesso total no TcaplusDB
Para conceder a um usuário a permissão para criar e gerenciar instâncias do TcaplusDB, associe a política `QcloudTcaplusDBFullAccess` ao usuário.
Essa política concede ao usuário a permissão para manipular todos os recursos no TcaplusDB. As etapas são as seguintes:
Autorize a política padrão `QcloudTcaplusDBFullAccess` ao usuário, conforme instruído em [Gerenciamento de autorização](https://intl.cloud.tencent.com/document/product/598/10602).

### Política somente leitura no TcaplusDB
Para conceder a um usuário a permissão para exibir as instâncias do TcaplusDB, mas não criar, excluir ou modificá-las, você pode associar a política `QcloudTcaplusDBReadOnlyAccess` ao usuário.
Essa política concede ao usuário as permissões de todas as operações no TcaplusDB que começam com a palavra "Describe (Descrever)" ou "Inquiry (Consultar)". As etapas são as seguintes:
Autorize a política padrão `TcaplusDB` ao usuário, conforme instruído em [Gerenciamento de autorização](https://intl.cloud.tencent.com/document/product/598/10602).

### Política para conceder permissão ao usuário para manipular um cluster específico
Para conceder a um usuário a permissão para manipular um cluster específico do TcaplusDB, você pode associar a política a seguir ao usuário. As etapas são as seguintes:

1. Crie uma política personalizada conforme instruído em [Política](https://intl.cloud.tencent.com/document/product/598/10601).
Essa política concede ao usuário a permissão para realizar todas as operações no cluster do TcaplusDB cujo ID é 19168929215. O conteúdo da política pode ser definido referindo-se à seguinte sintaxe de política:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "tcaplusdb:*",
            "resource": "qcs::tcaplusdb:ap-shanghai:uin/1231xxx166:cluster/19168929215",
            "effect": "allow"
        }
    ]
}
```
2. Encontre a política criada e clique em **Associate User/Group (Associar usuário/grupo)** na coluna "Operation (Operação)".
3. Na janela "Associate User/User Group (Associar usuário/grupo de usuários)" exibida, selecione o usuário/grupo que deseja autorizar e clique em **Confirm (Confirmar)**.


### Política para conceder permissão ao usuário para manipular todos os recursos do TcaplusDB
Para conceder a um usuário a permissão para manipular todos os recursos do TcaplusDB, associe a seguinte política ao usuário. As etapas são as seguintes:

1. Crie uma política personalizada conforme instruído em [Política](https://intl.cloud.tencent.com/document/product/598/10601).
Essa política concede ao usuário a permissão para manipular todos os recursos do TcaplusDB. O conteúdo da política pode ser definido referindo-se à seguinte sintaxe de política:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "tcaplusdb:*",
            "resource": "qcs::tcaplusdb:::*",
            "effect": "allow"
        }
    ]
}
```
2. Encontre a política criada e clique em **Associate User/Group (Associar usuário/grupo)** na coluna "Operation (Operação)".
3. Na janela "Associate User/User Group (Associar usuário/grupo de usuários)" exibida, selecione o usuário/grupo que deseja autorizar e clique em **Confirm (Confirmar)**.


### Política para negar ao usuário todas as permissões de algumas tabelas do TcaplusDB
Para negar a um usuário a permissão para manipular algumas tabelas do TcaplusDB, associe a seguinte política ao usuário. As etapas são as seguintes:

1. Crie uma política personalizada conforme instruído em [Política](https://intl.cloud.tencent.com/document/product/598/10601).
Essa política nega ao usuário a permissão para manipular tabelas (ID: tcaplus-c8d1caa4 e tcaplus-d8d1cbb4). O conteúdo da política pode ser definido referindo-se à seguinte sintaxe de política:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "tcaplusdb:*",
            "resource": [
						"qcs::tcaplusdb::uin/16xxx472:table/tcaplus-c8d1caa4",
						"qcs::tcaplusdb::uin/16xxx472:table/tcaplus-d8d1cbb4",
						],
            "effect": "deny"
        }
    ]
}
```
2. Encontre a política criada e clique em **Associate User/Group (Associar usuário/grupo)** na coluna "Operation (Operação)".
3. Na janela "Associate User/User Group (Associar usuário/grupo de usuários)" exibida, selecione o usuário/grupo que deseja autorizar e clique em **Confirm (Confirmar)**.

<span id="CAMCustomPolicy"></span>
### Política personalizada
Se as políticas predefinidas não atenderem aos seus requisitos, é possível criar políticas personalizadas, conforme necessário.
Para obter instruções detalhadas, consulte [Política](https://intl.cloud.tencent.com/document/product/598/10601).
Para obter mais sintaxe da política do TcaplusDB, consulte [Sintaxe da política de autorização](https://intl.cloud.tencent.com/document/product/1016/35751).

