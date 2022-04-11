O mecanismo de armazenamento de um banco de dados se refere ao tipo de tabelas e determina como as tabelas são armazenadas nos computadores. Embora o MySQL forneça diferentes tipos de mecanismos de armazenamento, nem todos foram otimizados para a restauração e persistência de dados. As funcionalidades do TencentDB for MySQL, como a restauração pontual e a restauração de snapshot, requerem um mecanismo de armazenamento habilitado para restauração e estão disponíveis apenas no mecanismo de armazenamento InnoDB.

Por padrão, o TencentDB for MySQL aceita o InnoDB. Ele não aceita mais os mecanismos MyISAM e Memory no MySQL 5.6 e versões posteriores, principalmente pelos seguintes motivos:
- O TencentDB for MySQL otimiza muito os kernels do InnoDB e atinge um desempenho superior.
- O MyISAM adota um mecanismo de bloqueio em nível de tabela, já o InnoDB usa um mecanismo em nível de linha. Normalmente, o InnoDB tem maior eficiência de gravação.
>?
>- Com o escopo de bloqueio mais amplo, o bloqueio em nível de tabela é para bloquear toda a tabela que está sendo manipulada no MySQL.
>- Com o escopo de bloqueio mais estreito, o bloqueio em nível de linha é para bloquear apenas a linha que está sendo manipulada no MySQL.
- O MyISAM tem defeitos na proteção da integridade dos dados, o que pode levar à corrupção ou até mesmo à perda dos dados. Além disso, muitos desses defeitos são problemas de design e não podem ser corrigidos sem quebrar a compatibilidade.
- A migração de MyISAM e Memory para InnoDB pode ser obtida a baixo custo apenas alterando o código para criar as tabelas para a maioria das aplicações.
- O MyISAM está dando lugar ao InnoDB. No MySQL 8.0 mais recente, todas as tabelas do sistema vêm com o tipo InnoDB.
- O Memory não consegue garantir a integridade dos dados. Se a instância for reiniciada ou passar pela alternância de source/réplica, todos os dados da tabela serão perdidos. É recomendado migrar para o InnoDB o mais rápido possível.

Para mais informações, consulte [Visão geral do InnoDB](https://dev.mysql.com/doc/refman/5.7/en/innodb-introduction.html) e [Visão geral do MyISAM](https://dev.mysql.com/doc/refman/5.7/en/myisam-storage-engine.html).

