
A replicação de instâncias de banco de dados significa sincronizar os dados ao configurar um ou mais bancos de dados de backup para o servidor, para distribuir os dados no MySQL em vários sistemas. O TencentDB for MySQL tem três modos de replicação de dados:

>?
>- “Source (Origem)” refere-se ao nó de origem em uma instância, e “replica (réplica)”, o nó de réplica na instância.
>- Atualmente, o MySQL v5.6, v5.7 e v8.0 aceitam três modos de replicação: assíncrona, semissincronizada e sincronização forte. Apenas o modo de replicação assíncrona está disponível no MySQL v5.5.


### Replicação assíncrona
Uma aplicação inicia uma solicitação de atualização de dados (incluindo as operações INSERT, UPDATE e DELETE). Após concluir a operação de atualização, o source envia uma resposta à aplicação imediatamente, e replica os dados para a réplica.

Durante a atualização dos dados, o source não precisa esperar por uma resposta da réplica, portanto, a instância do banco de dados replicada de forma assíncrona costuma ter um desempenho superior, e a indisponibilidade da réplica não afetará o fornecimento de serviços pelo source. No entanto, como os dados não são sincronizados com a réplica em tempo real, se o source falhar quando ocorrer um atraso na réplica, há uma pequena chance de inconsistência de dados.
A replicação assíncrona é implementada no TencentDB for MySQL de um source e uma réplica.

### Replicação semissincronizada
Uma aplicação inicia uma solicitação de atualização de dados (incluindo as operações INSERT, UPDATE e DELETE). Após concluir a operação de atualização, o source replica os dados para uma réplica imediatamente. Após **receber e gravar os dados no log de retransmissão (ignorado)**, a réplica gera uma mensagem de sucesso para o source. Somente após receber a mensagem da réplica, o source pode gerar  uma resposta à aplicação.

Somente quando ocorrer um erro com a replicação de dados (um nó de réplica fica indisponível ou ocorre um erro com a rede usada para a replicação de dados), o source suspenderá a resposta à aplicação (por cerca de 10 segundos por padrão no MySQL), e será feito o downgrade da replicação para assíncrona. Quando a replicação de dados retornar ao estado normal, a replicação semissincronizada será restaurada.
A replicação semissincronizada é implementada no TencentDB for MySQL de um source e uma réplica.

### Replicação de sincronização forte
Uma aplicação inicia uma solicitação de atualização de dados (incluindo as operações INSERT, UPDATE e DELETE). Após concluir a operação de atualização, o source replica os dados para uma réplica imediatamente. Após **receber e gravar os dados no log de retransmissão (ignorado)**, a réplica gera uma mensagem de sucesso para o source. Somente após receber a mensagem da réplica, o source pode gerar uma resposta à aplicação.

Quando ocorrer um erro com a replicação de dados (um nó de réplica fica indisponível ou ocorre um erro com a rede usada para a replicação de dados), **não será feito o downgrade da replicação** e o source suspenderá a resposta à aplicação até que o erro seja corrigido, de modo a garantir a consistência dos dados.

A replicação de sincronização forte é implementada no TencentDB for MySQL de um source e duas réplicas. O source pode receber a mensagem de sucesso desde que uma das duas réplicas atualize os dados com êxito, evitando que a indisponibilidade de uma única réplica afete as operações no source e melhorando a disponibilidade do cluster de replicação de sincronização forte.


