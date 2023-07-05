Se você utiliza vários serviços do Tencent Cloud, como o Cloud Virtual Machine (CVM), o VPC e o TencentDB, é provável que eles sejam gerenciados por diferentes usuários que têm acesso à sua chave de conta. Isso traz os seguintes desafios:
- Sua chave é compartilhada entre vários usuários, levando a um alto risco de exposição.
- Você não consegue restringir o acesso dos usuários aos diferentes recursos, o que representa risco de segurança devido a possíveis erros de operação.

Uma solução para esses problemas é o uso de subcontas. As subcontas lhe permitem atribuir uma conta diferente a cada usuário, para que esse possa desempenhar suas funções sem o risco de interferir nas de outras pessoas. Entretanto, as subcontas, por padrão, não têm permissão para acessar instâncias do CVM e recursos relacionados. É necessário criar políticas adequadas para cada subconta para lhes conceder acesso.

O Tencent Cloud fornece um serviço Web chamado Cloud Access Management (CAM) para ajudar os clientes a gerenciar com segurança o acesso a seus recursos em suas contas do Tencent Cloud. O CAM permite-lhe criar, administrar ou encerrar usuários e grupos de usuários, e fornece gerenciamento de identidades e de políticas para controlar quem tem permissão para acessar e utilizar os recursos do Tencent Cloud.

Você pode associar políticas do CAM a um usuário ou grupo de usuários, as quais concedem ou negam permissões para usar recursos exclusivos que executam tarefas específicas. Para obter mais informações sobre a política do CAM, consulte [Sintaxe da política](https://intl.cloud.tencent.com/document/product/598/10603). Para obter mais informações acerca de como utilizar as políticas do CAM, consulte [Políticas](https://intl.cloud.tencent.com/document/product/598/10601).

Você pode ignorar essa seção se o gerenciamento de acesso a recursos por vários usuários não for aplicável. Isso não afetará a sua compreensão do restante do artigo.

#### Introdução

Uma política do CAM deve permitir ou negar uma ou mais operações do CVM, bem como os recursos a que essas ações se destinam. Uma política também pode incluir as condições que regem a utilização de recursos.

Algumas das APIs do CVM não aceitam permissões de nível de recursos, o que significa que você deve especificar todos esses, em vez de recursos específicos, ao executar tais operações de API.

| Tarefa | Link | 
|---------|---------|
| Saber mais sobre a estrutura básica da política | [Sintaxe da política](https://intl.cloud.tencent.com/document/product/213/10313) |
| Definir as operações da política | [Operações do CVM](https://intl.cloud.tencent.com/document/product/213/10313) | 
| Definir os recursos da política | [Caminho do recurso do CVM](https://intl.cloud.tencent.com/document/product/213/10313) |
| Limitar a política com condições | [Chaves de condição do CVM](https://intl.cloud.tencent.com/document/product/213/10313) |
| Permissões de nível de recursos compatíveis com o CVM | [Permissões de nível de recursos compatíveis com o CVM](https://intl.cloud.tencent.com/document/product/213/10314) |
| Amostras do console | [Amostras do console](https://intl.cloud.tencent.com/document/product/213/10312) |
