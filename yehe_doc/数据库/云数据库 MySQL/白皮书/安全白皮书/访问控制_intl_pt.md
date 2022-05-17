O TencentDB for MySQL implementa o controle de acesso por meio do gerenciamento de contas de banco de dados, gerenciamento de acesso, grupo de segurança e outros meios para garantir a segurança dos dados do MySQL.

### Gerenciamento de contas de banco de dados
Você pode [criar contas de banco de dados](https://intl.cloud.tencent.com/document/product/236/31900) no console do TencentDB for MySQL ou por meio de APIs. Você também pode conceder permissões de gerenciamento em níveis diferentes para essas contas. Recomendamos autorizar as contas com base no princípio de privilégio mínimo para garantir a segurança dos dados.

### Cloud Access Management
O [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) ajuda você a gerenciar e controlar com segurança as permissões de acesso aos seus recursos da Tencent Cloud. Com o CAM, você pode criar, gerenciar e encerrar usuários (grupos) e controlar os recursos da Tencent Cloud que podem ser usados pelo usuário especificado por meio do gerenciamento de identidade e política, que implementa a separação de permissões.

### Grupo de segurança
O [grupo de segurança](https://intl.cloud.tencent.com/document/product/236/14470) ajuda principalmente a implementar o controle de acesso à rede das suas instâncias do TencentDB for MySQL. Um grupo de segurança é um firewall virtual com monitoração de estado que realiza filtragem. Como uma forma importante de isolamento de segurança de rede fornecida pela Tencent Cloud, ele pode ser usado para definir controles de acesso à rede de uma ou mais instâncias do TencentDB.

As instâncias com os mesmos requisitos de isolamento de segurança de rede na mesma região podem ser colocadas no mesmo grupo de segurança lógico. As instâncias em um grupo de segurança são correspondidas com base em regras. A modificação das regras do grupo de segurança não requer a reinicialização das instâncias do TencentDB for MySQL, e as alterações entrarão em vigor imediatamente.


