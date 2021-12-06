Caso você use vários serviços do Tencent Cloud, como CLB, CVM e TencentDB, que são gerenciados por diferentes usuários compartilhando a chave da sua conta Tencent Cloud, pode ser que enfrente os seguintes problemas:
- Sua chave é compartilhada entre vários usuários, levando a um alto risco de exposição.
- Você não pode limitar as permissões de acesso de outros usuários, o que representa um risco de segurança devido a possíveis operações com falha.

O [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/17848) é usado para gerenciar as permissões de acesso aos seus recursos do Tencent Cloud. Com o CAM, você pode usar os recursos de gerenciamento de identidade e políticas para controlar quais recursos do Tencent Cloud podem ser acessados por quais subcontas.

Por exemplo, se você tiver em sua conta várias instâncias do CLB que são implementadas em projetos diferentes, para gerenciar permissões de acesso e autorizar recursos, você pode vincular o administrador do projeto A com uma política de autorização segundo a qual apenas este administrador pode usar os recursos do CLB do projeto A.

Se você não precisa gerenciar a permissão de acesso aos recursos do CLB para subcontas, pode pular este capítulo. Isso não afetará sua compreensão e uso de outras partes da documentação.

## Conceitos básicos em CAM
A conta raiz autoriza subcontas vinculando políticas. O grau de especificidade da configuração de política abrange **API, recurso, usuário/grupo de usuários, permitir/negar e condição**.

1. Conta
 - **Conta raiz**
 Como o proprietária fundamental dos recursos do Tencent Cloud, uma conta raiz atua como a base para o cálculo e faturamento da taxa de uso de recursos e pode ser usada para fazer login nos serviços do Tencent Cloud.
 - **Subconta**
 Uma subconta é criada pela conta raiz e tem um ID e credencial de identidade específicos que podem ser usados para fazer login no Console do Tencent Cloud. Uma conta raiz pode criar várias subcontas (usuários). **Uma subconta não possui nenhum recurso por padrão; em vez disso, esses recursos devem ser autorizados pela respectiva conta raiz.**
 - **Credencial de identidade**
Isso inclui credenciais de login e certificados de acesso. A **credencial de login** refere-se ao nome de usuário e senha. O **certificado de acesso** refere-se às chaves da API do TencentCloud (SecretId e SecretKey).
2. Recursos e permissões
 - **Recurso**
Um recurso é um objeto operado no serviço Tencent Cloud, como uma instância do CVM e uma instância do VPC.
 - **Permissão **
A permissão é uma autorização para permitir ou proibir certos usuários de realizarem certas operações. Por padrão, **uma conta raiz tem acesso total a todos os recursos que lhe cabem**, enquanto **uma subconta não tem acesso a nenhum recurso que cabe à conta raiz**.
 - **Política**
A política é a regra de sintaxe usada para definir e descrever uma ou várias permissões. **Uma conta raiz** realiza autorização **associando políticas** a usuários/grupos de usuários.

 Para obter mais informações, consulte [Visão geral do CAM](https://intl.cloud.tencent.com/document/product/598/10583).

## Documentos relacionados

| Descrição do documento | Link |
| ----------------------- | ------------------------------------------------------------ |
| Relação entre política e usuário | [Política](https://intl.cloud.tencent.com/document/product/598/10601) |
| Estrutura de política básica | [Referência de elemento](https://intl.cloud.tencent.com/document/product/598/10603) |
| Mais produtos compatíveis com o CAM | [Serviços em nuvem habilitados para CAM](https://intl.cloud.tencent.com/document/product/598/10588) |
