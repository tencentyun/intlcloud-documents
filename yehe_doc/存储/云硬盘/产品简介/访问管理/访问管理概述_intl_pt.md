Caso esteja usando vários serviços do Tencent Cloud, como CVM, CBS, VPC e TencentDB, que são gerenciados por usuários diferentes que compartilham a chave da sua conta do Tencent Cloud, os seguintes problemas podem acontecer:
- Sua chave é compartilhada entre vários usuários, levando a um alto risco de exposição.
- Você não pode controlar as permissões de acesso de outros usuários, o que representa um risco de segurança devido ao potencial de operações incorretas.

Nesse caso, você pode usar subcontas para permitir que diversos usuários gerenciem diversos serviços para evitar esses problemas. Por padrão, uma subconta não tem permissão para usar CVMs ou recursos relacionados a CVMs. Portanto, você precisará criar uma política para conceder as permissões ou os recursos necessários para a subconta.

O [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) é um conjunto de serviços do Tencent Cloud baseados em nuvem que ajuda você a gerenciar com segurança e controlar permissões de acesso aos seus recursos do Tencent Cloud. Ao usar o CAM, você pode criar, gerenciar e excluir usuários (grupos) e controlar quem pode usar os recursos do Tencent Cloud e quais recursos do Tencent Cloud eles podem usar por meio do gerenciamento de políticas e identidade.

Quando usar o CAM, você poderá associar políticas a um usuário ou grupo de usuários, o que concederá ou negará a eles permissão para usar determinados recursos para realizar as tarefas especificadas. Para obter mais informações sobre os princípios básicos da política do CAM, consulte [Sintaxe da política](https://intl.cloud.tencent.com/document/product/598/10603). Para obter mais informações sobre o uso de políticas do CAM, consulte [Políticas](https://intl.cloud.tencent.com/document/product/598/10601).

Se você não precisa gerenciar as permissões de acesso de subcontas aos recursos do CBS, pule esta seção. Isso não afetará sua compreensão e aplicação das outras seções deste documento.

### Introdução

Uma política do CAM deve conceder ou negar permissão a uma ou mais operações do CBS. Além disso, ela deve especificar os recursos que podem ser utilizados (que pode ser todos os recursos ou alguns recursos para determinadas operações). Uma política também pode conter as condições definidas para as operações dos recursos.

| Tarefa | Link |
|---------|---------|
| Saber mais sobre a estrutura básica da política | [Sintaxe da política](https://intl.cloud.tencent.com/document/product/362/34221) |
| Definir as operações da política | [Operações do CBS](https://intl.cloud.tencent.com/document/product/362/34221) |
| Definir os recursos da política | [Caminhos de recursos do CBS](https://intl.cloud.tencent.com/document/product/362/34221) |
| Limitar a política com condições | [Chaves de condição do CBS](https://intl.cloud.tencent.com/document/product/362/34221) |
| Saber mais sobre as permissões de nível de recursos que são compatíveis com o CBS| [Permissões de nível de recursos compatíveis com o CBS](https://intl.cloud.tencent.com/document/product/362/34220) |
| Ver exemplos do console | [Exemplos do console](https://intl.cloud.tencent.com/document/product/213/10312) |
