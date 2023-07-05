## Introdução

Você pode usar políticas do Cloud Access Management (CAM) para gerenciar o acesso do usuário aos recursos, usando o console do Cloud Virtual Machine (CVM). Este documento fornece exemplos para ajudar você a entender como usar as políticas do CAM predefinidas usando o console do CVM.

## Exemplos
### Leitura e gravação (CVM)
Se você deseja permitir que um usuário crie e gerencie instâncias do CVM, associe o usuário à política chamada QcloudCVMFullAccess. Essa política foi projetada para conceder aos usuários as permissões para acessar todos os recursos no CVM, no Virtual Private Cloud (VPC), no Cloud Load Balancer (CLB) e no Cloud Monitor.
As etapas detalhadas são as seguintes:
Consulte [Gerenciamento de autorizações](https://intl.cloud.tencent.com/document/product/598/10602) para obter instruções sobre como conceder a política predefinida QcloudCVMFullAccess a um usuário.

### Somente leitura (CVM)
Se você deseja permitir que um usuário apenas consulte, mas não crie, exclua ou inicie/desligue instâncias do CVM, associe o usuário à política chamada QcloudCVMInnerReadOnlyAccess. Essa política foi projetada para conceder aos usuários as permissões para realizar todas as operações iniciadas por "Describe (Descrever)" e "Inquiry (Consultar)" no CVM. As etapas detalhadas são as seguintes:
Consulte [Gerenciamento de autorizações](https://intl.cloud.tencent.com/document/product/598/10602) para obter instruções sobre como conceder a política predefinida QcloudCVMInnerReadOnlyAccess a um usuário.

### Somente leitura (CVM e recursos associados)
Se você deseja permitir que um usuário apenas consulte, mas não crie, exclua ou inicie/desligue instâncias do CVM e recursos associados (VPC e CLB), associe o usuário à política chamada QcloudCVMReadOnlyAccess. Essa política foi projetada para conceder aos usuários as permissões para realizar as seguintes operações:
- Todas as operações iniciadas por "Describe (Descrever)" e "Inquiry (Consultar)" no CVM.
- Todas as operações iniciadas por "Describe (Descrever)", "Inquiry (Consultar)" e "Get (Obter)" no VPC.
- Todas as operações iniciadas por "Describe (Descrever)" no CLB.
- Todas as operações no Monitor.

As etapas detalhadas são as seguintes:
Consulte [Gerenciamento de autorizações](https://intl.cloud.tencent.com/document/product/598/10602) para obter instruções sobre como conceder a política predefinida QcloudCVMReadOnlyAccess a um usuário.

### Políticas do CBS

Se você deseja permitir que um usuário visualize, crie e use discos em nuvem no console do CVM, adicione as seguintes operações à sua política e associe a política ao usuário.
- **CreateCbsStorages:** criar um disco em nuvem.
- **AttachCbsStorages:** montar o disco em nuvem especificado para o CVM especificado.
- **DetachCbsStorages:** desmontar o disco em nuvem especificado.
- **ModifyCbsStorageAttributes:** modificar o nome ou o ID do projeto do disco em nuvem especificado.
- **DescribeCbsStorages:** consultar os detalhes de um disco em nuvem.
- **DescribeInstancesCbsNum:** consultar a quantidade de discos em nuvem montados de um CVM e a quantidade máxima de discos em nuvem que podem ser montados no CVM.
- **RenewCbsStorage:** renovar o disco em nuvem especificado.
- **ResizeCbsStorage:** redimensionar o disco em nuvem especificado.

As etapas detalhadas são as seguintes:
1. Consulte [Políticas](https://intl.cloud.tencent.com/document/product/598/10601) para obter informações e criar uma política personalizada que conceda as permissões para visualizar as informações do disco em nuvem no console do CVM e para criar e usar discos em nuvem.
Use o seguinte como referência de sintaxe:
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/cvm:CreateCbsStorages",
                "name/cvm:AttachCbsStorages",
                "name/cvm:DetachCbsStorages",
                "name/cvm:ModifyCbsStorageAttributes",
                "name/cvm:DescribeCbsStorages"
            ],
            "resource": [
                "qcs::cvm::uin/1410643447:*"
            ]
        }
    ]
}
```
2. Encontre a política criada e, na coluna “Action (Ação)” da linha, clique em **Associate User/Group (Associar usuário/grupo)**.
3. Na janela “Associate User/Group (Associar usuário/grupo)”, selecione o usuário/grupo que deseja associar e clique em **OK**.


### Políticas de grupos de segurança

Para permitir que um usuário visualize e use os grupos de segurança no console do CVM, adicione as seguintes operações à sua política e associe a política ao usuário.
- **DeleteSecurityGroup:** excluir um grupo de segurança.
- **ModifySecurityGroupPolicys:** substituir todas as políticas de um grupo de segurança.
- **ModifySingleSecurityGroupPolicy:** modificar uma única política de um grupo de segurança.
- **CreateSecurityGroupPolicy:** criar uma política de grupo de segurança.
- **DeleteSecurityGroupPolicy:** excluir uma política de grupo de segurança.
- **ModifySecurityGroupAttributes:** modificar os atributos de um grupo de segurança.

As etapas detalhadas são as seguintes:
1. Consulte [Políticas](https://intl.cloud.tencent.com/document/product/598/10601) para obter informações e criar uma política personalizada que conceda as permissões para criar, excluir e modificar grupos de segurança no console do CVM.
Use o seguinte como referência de sintaxe:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:ModifySecurityGroupPolicys",
                "name/cvm:ModifySingleSecurityGroupPolicy",
                "name/cvm:CreateSecurityGroupPolicy",
                "name/cvm:DeleteSecurityGroupPolicy"
            ],
            "resource": "*",
            “effect": "allow"
        }
    ]
}
```
2. Encontre a política criada e, na coluna “Action (Ação)” da linha, clique em **Associate User/Group (Associar usuário/grupo)**.
3. Na janela “Associate User/Group (Associar usuário/grupo)”, selecione o usuário/grupo que deseja autorizar e clique em **OK**.


### Política para EIPs

Se você deseja permitir que um usuário visualize e use EIPs no console do CVM, adicione as seguintes operações à sua política e associe a política ao usuário.
- **AllocateAddresses:** atribuir um EIP a uma instância do VPC ou do CVM.
- **AssociateAddress:** associar um EIP a uma instância ou uma interface de rede.
- **DescribeAddresses:** visualizar EIPs no console do CVM.
- **DisassociateAddress:** desassociar um EIP de uma instância ou de uma interface de rede.
- **ModifyAddressAttribute:** modificar os atributos de um EIP.
- **ReleaseAddresses:** liberar um EIP.

As etapas detalhadas são as seguintes:
1. Consulte [Políticas](https://intl.cloud.tencent.com/document/product/598/10601) para obter informações e criar uma política personalizada.
Essa política permite aos usuários visualizar um EIP e atribuí-lo e associá-lo a uma instância no console do CVM. Os usuários não podem modificar os atributos do EIP, desassociá-lo de uma instância ou liberar o EIP. Use o seguinte como referência de sintaxe:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:DescribeAddresses",
                "name/cvm:AllocateAddresses",
                "name/cvm:AssociateAddress"
            ],
            "resource": "*",
            “effect": "allow"
        }
    ]
}
```
2. Encontre a política criada e, na coluna “Action (Ação)” da linha, clique em **Associate User/Group (Associar usuário/grupo)**.
3. Na janela “Associate User/Group (Associar usuário/grupo)”, selecione o usuário/grupo que deseja autorizar e clique em **OK**.

### Política para autorizar usuários a realizar operações em CVMs específicos
Se você deseja autorizar um usuário a realizar operações em um CVM específico, associe a política a seguir ao usuário. As etapas detalhadas são as seguintes:
1. Consulte [Políticas](https://intl.cloud.tencent.com/document/product/598/10601) para obter informações e criar uma política personalizada.
Essa política autoriza o usuário a operar uma instância do CVM com o ID ins-1 na região de Guangzhou. Use o seguinte como referência de sintaxe:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cvm:*",
            "resource": "qcs::cvm:ap-guangzhou::instance/ins-1",
            “effect": "allow"
        }
    ]
}
```
2. Encontre a política criada e, na coluna “Action (Ação)” da linha, clique em **Associate User/Group (Associar usuário/grupo)**.
3. Na janela “Associate User/Group (Associar usuário/grupo)”, selecione o usuário/grupo que deseja autorizar e clique em **OK**.


### Política para autorizar usuários a realizar operações nos CVMs em uma região específica
Se você deseja autorizar um usuário a realizar operações nos CVMs em uma região específica, associe a política a seguir ao usuário. As etapas detalhadas são as seguintes:
1. Consulte [Políticas](https://intl.cloud.tencent.com/document/product/598/10601) para obter informações e criar uma política personalizada.
Essa política autoriza o usuário a operar instâncias do CVM na região de Guangzhou. Use o seguinte como referência de sintaxe:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cvm:*",
            "resource": "qcs::cvm:ap-guangzhou::*",
            “effect": "allow"
        }
    ]
}
```
2. Encontre a política criada e, na coluna “Action (Ação)” da linha, clique em **Associate User/Group (Associar usuário/grupo)**.
3. Na janela “Associate User/Group (Associar usuário/grupo)”, selecione o usuário/grupo que deseja autorizar e clique em **OK**.


### Conceder a uma subconta todas as permissões para instâncias do CVM, exceto pagamento

Suponha que a conta CompanyExample, cujo ownerUin é 12345678, tenha uma subconta chamada Developer. A Developer requer permissões totais de gerenciamento (incluindo todas as operações, como criação e gerenciamento) para a instância do CVM, exceto o pagamento, o que significa que a subconta pode fazer pedidos, mas não pode pagar por eles.
É possível fazer isso usando uma das seguintes soluções:
- **Solução A**
O proprietário da conta CompanyExample associa a política predefinida QcloudCVMFullAccess à subconta Developer. Para obter mais informações, consulte [Gerenciamento de autorizações](https://intl.cloud.tencent.com/document/product/598/10602).
- **Solução B**
 1. Use o seguinte como uma referência de sintaxe e crie uma [política personalizada](#CAMCustomPolicy).
```
 {
    "version": "2.0",
    "statement":[
         {
             "effect": "allow",
             "action": "cvm:*",
             "resource": "*"
         }
    ]
}
```
 2. Associe a política à subconta. Para obter mais informações, consulte [Gerenciamento de autorizações](https://intl.cloud.tencent.com/document/product/598/10602).


### Conceder a uma subconta a permissão para gerenciar projetos
Suponha que a conta corporativa, CompanyExample, com ownerUin de 12345678, tenha uma subconta chamada Developer. O proprietário da CompanyExample deseja permitir que a Developer gerencie projetos, incluindo a atribuição e a remoção de recursos, no console.
As etapas detalhadas são as seguintes:
1. Crie uma política personalizada para o gerenciamento de projetos.
Para obter mais informações, consulte [Políticas](https://intl.cloud.tencent.com/document/product/598/10601).
2. Consulte [Gerenciamento de autorizações](https://intl.cloud.tencent.com/document/product/598/10602) para obter informações sobre como associar a política personalizada à subconta.
Se você tiver problemas de permissão ao tentar visualizar snapshots, imagens e EIPs, associe as políticas predefinidas QcloudCVMAccessForNullProject, QcloudCVMOrderAccess e QcloudCVMLaunchToVPC à subconta. Para obter mais informações sobre autorizações, consulte [Gerenciamento de autorizações](https://intl.cloud.tencent.com/document/product/598/10602).

<span id="CAMCustomPolicy"></span>
### Política personalizada

Se as políticas predefinidas não atenderem aos seus requisitos, é possível criar políticas personalizadas.
Para obter instruções detalhadas, consulte [Políticas](https://intl.cloud.tencent.com/document/product/598/10601).
Para obter mais informações sobre a sintaxe da política do CVM, consulte [Sintaxe da política de autorização](https://intl.cloud.tencent.com/document/product/213/10313).

