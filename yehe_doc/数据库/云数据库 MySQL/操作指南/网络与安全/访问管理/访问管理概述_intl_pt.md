## Problemas conhecidos
Se você tiver vários usuários gerenciando diferentes serviços da Tencent Cloud, como CVM, VPC e TencentDB, e todos eles compartilharem sua chave de acesso à conta da Tencent Cloud, você poderá enfrentar os seguintes problemas:
- O risco de sua chave ser comprometida é alto, pois vários usuários a compartilham.
- Seus usuários podem comprometer a segurança através de falhas operacionais causadas pela falta de controle de acesso de usuário.

## Soluções
Você pode evitar os problemas acima permitindo que diferentes usuários gerenciem diferentes serviços por meio de subcontas. Por padrão, uma subconta não tem permissões para usar os serviços ou recursos da Tencent Cloud. Portanto, você precisa criar uma política para conceder permissões diferentes às subcontas.

O [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) é um serviço da Tencent Cloud baseado na web que ajuda a gerenciar e controlar com segurança as permissões de acesso aos seus recursos da Tencent Cloud. Usando o CAM, você pode criar, gerenciar e encerrar usuários individuais e grupos. É possível gerenciar identidades e políticas para permitir que usurários específicos acessem seus recursos da Tencent Cloud.

Ao usar o CAM, você pode associar uma política a um usuário ou grupo de usuários para permitir ou proibir que usem recursos especificados para concluir tarefas especificadas. Para obter mais informações sobre as políticas do CAM, consulte [Lógica da sintaxe](https://intl.cloud.tencent.com/document/product/598/10603).

Você pode pular esta seção se não precisar gerenciar permissões para recursos do TencentDB para subcontas. Isso não afetará sua compreensão e uso das outras seções do documento.

### Introdução
Uma política CAM é usada para permitir ou negar uma ou mais operações do TencentDB. Ao configurar uma política, você deve especificar os recursos de destino das operações, que podem ser todos os recursos ou recursos especificados. Uma política também pode incluir condições em que os recursos podem ser usados.

>?
>- Recomendamos que você gerencie os recursos e autorize as operações do TencentDB por meio de políticas CAM. Embora a experiência do usuário não seja alterada para usuários existentes que recebem permissões por projeto, não recomendamos que você continue gerenciando recursos e autorizando operações com base em projetos.
>- As condições não podem ser definidas no TencentDB por enquanto.

| Tarefa | Link | 
|---------|---------|
| Saber mais sobre a estrutura básica da política | [Sintaxe da política](https://intl.cloud.tencent.com/document/product/236/14466) |
| Definir as operações em uma política | [Operações do TencentDB](https://intl.cloud.tencent.com/document/product/236/14466) | 
| Definir os recursos na política | [Caminho do recurso do TencentDB](https://intl.cloud.tencent.com/document/product/236/14466) |
| Permissão de nível de recurso aceita pelo TencentDB | [Tipos de recursos autorizáveis](https://intl.cloud.tencent.com/document/product/236/14467)|
| Exemplo do console | [Exemplo do console](https://intl.cloud.tencent.com/document/product/236/14468) |
