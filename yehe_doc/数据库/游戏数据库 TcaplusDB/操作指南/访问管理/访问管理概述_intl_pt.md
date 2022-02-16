## Problemas conhecidos
Caso você use vários serviços do Tencent Cloud, como TcaplusDB, VPC, CVM e TencentDB, que são gerenciados por diferentes usuários compartilhando a chave da sua conta do Tencent Cloud, pode ser que enfrente os seguintes problemas:
- Sua chave é compartilhada entre vários usuários, levando a um alto risco de exposição.
- Você não pode limitar as permissões de acesso de outros usuários, o que representa um risco de segurança devido a possíveis operações com falha.

## Solução
Você pode permitir que usuários diferentes gerenciem serviços diferentes por meio de subcontas para evitar os problemas acima. Por padrão, uma subconta não tem permissão para usar o serviço ou os recursos do TcaplusDB. Portanto, você precisa criar uma política para conceder a permissão necessária à subconta.

O [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) é um serviço do Tencent Cloud baseado na web que ajuda a gerenciar e controlar com segurança as permissões de acesso aos seus recursos do Tencent Cloud. Usando o CAM, você pode criar, gerenciar e encerrar usuários (grupos) e controlar os recursos do Tencent Cloud que podem ser usados pelo usuário especificado por meio do gerenciamento de identidade e política.

Ao usar o CAM, você pode associar uma política a um usuário ou grupo de usuários para permitir ou proibi-los de usar recursos especificados para concluir tarefas especificadas. Para obter mais informações sobre as políticas do CAM, consulte [Sintaxe da política](https://intl.cloud.tencent.com/document/product/598/10603).

Se você não precisa gerenciar as permissões de acesso aos recursos do TcaplusDB para subcontas, pode pular essa parte. Isso não afetará seu entendimento e utilização de outras partes da documentação.

### Introdução
Uma política do CAM deve autorizar ou negar o uso de uma ou mais operações do TcaplusDB. Ao mesmo tempo, deve especificar os recursos que podem ser usados para as operações (que podem ser todos os recursos ou recursos parciais para algumas operações). Uma política também pode incluir as condições definidas para os recursos manipulados.

Algumas APIs do TencentCloud para o TcaplusDB não aceitam permissões a nível de recurso, o que significa que, para esse tipo de operações de API, você não pode especificar um determinado recurso para uso quando são realizadas; em vez disso, você deve especificar todos os recursos para uso.


| Tarefa | Link |
| -------------------------- | ------------------------------------------------------------ |
| Estrutura básica da política | [Sintaxe da política](https://intl.cloud.tencent.com/document/product/1016/35751) |
| Definição de operação em uma política | [Operações do TcaplusDB](https://intl.cloud.tencent.com/document/product/1016/35751) |
| Definição de recursos em uma política | [Caminho dos recursos do TcaplusDB](https://intl.cloud.tencent.com/document/product/1016/35751) |
| Permissões a nível de recurso aceitas no TcaplusDB | [Permissões a nível de recurso aceitas no TcaplusDB](https://intl.cloud.tencent.com/document/product/1016/35750) |
| Exemplos do console | [Exemplos do console](https://intl.cloud.tencent.com/document/product/1016/35752) |

