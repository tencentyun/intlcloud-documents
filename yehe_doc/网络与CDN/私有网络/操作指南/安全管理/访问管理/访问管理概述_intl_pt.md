Se você estiver usando vários serviços do Tencent Cloud, como VPC, CVM e TencentDB, que são gerenciados por diferentes usuários que compartilham sua chave de conta do Tencent Cloud, você pode encontrar os seguintes problemas:
- Sua chave é compartilhada por vários usuários, o que representa um alto risco de vazamento.
- Você não pode limitar as permissões de acesso de outros usuários, o que representa um risco de segurança devido a uma possível operação incorreta.

Para evitar esses problemas, é possível usar subcontas para permitir que usuários diferentes gerenciem serviços diferentes. Por padrão, uma subconta não tem permissão para usar um CVM ou recursos relacionados ao CVM. Portanto, é necessário criar uma política para conceder os recursos ou permissões necessários às subcontas.

## Visão geral
O Cloud Access Management (CAM) é um serviço da web fornecido pelo Tencent Cloud para ajudar os clientes a gerenciar as permissões de acesso aos recursos em suas contas do Tencent Cloud de forma segura. É possível usar o CAM para criar, gerenciar e encerrar usuários (ou grupos de usuários), e usar o gerenciamento de identidade e de políticas para controlar os recursos do Tencent Cloud que podem ser usados por cada usuário.

Ao usar o CAM, você pode associar uma política a um usuário ou grupo de usuários. A política pode autorizar ou negar as solicitações dos usuários de usar recursos especificados para concluir tarefas especificadas.
- Para obter mais informações básicas sobre as políticas do CAM, consulte [Lógica da sintaxe](https://intl.cloud.tencent.com/document/product/598/10603).
- Para obter mais informações sobre o uso das políticas do CAM, consulte [Políticas](https://intl.cloud.tencent.com/document/product/598/10601).

Se não for necessário gerenciar as permissões de acesso de subcontas para recursos do VPC, pule esta seção. Isso não afetará sua compreensão e uso de outras partes do documento.



## Introdução
Uma política do CAM deve autorizar ou negar o uso de uma ou mais operações do VPC. Ao mesmo tempo, ela deve especificar os recursos (que podem ser todos os recursos ou recursos parciais para determinadas operações) que podem ser usados para as operações. A política também pode incluir as condições definidas para os recursos de operação.

Algumas operações de API do VPC aceitam permissões no nível de recursos. Ou seja, ao chamar essas APIs, você não pode especificar alguns recursos para as operações. Em vez disso, você deve especificar todos os recursos para as operações.


| Tarefa | Link |
| -------------------- | -------------------- |
| Estrutura básica de uma política | Sintaxe da política |
| Definir as operações da política | Operações do VPC|
| Definir os recursos da política | Caminhos dos recursos do VPC |
| Permissões de nível de recursos compatíveis com o VPC | [Permissões de nível de recursos compatíveis com o VPC](https://intl.cloud.tencent.com/document/product/215/31862) |
| Exemplo do console | [Exemplo do console](https://intl.cloud.tencent.com/document/product/215/31861) |
