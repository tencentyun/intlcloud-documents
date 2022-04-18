Os parâmetros no TencentDB for MySQL foram otimizados com base nos valores padrão oficiais no MySQL. Recomendamos que você configure os seguintes parâmetros para a instância do TencentDB for MySQL após a aquisição com base em seus cenários de negócios.

### character_set_server
- Valor padrão: UTF8
- Reinicialização necessária: sim
- Descrição: configuração do conjunto de caracteres padrão para o servidor MySQL. O TencentDB for MySQL oferece quatro conjuntos de caracteres: LATIN1, UTF8, GBK e UTF8MB4. Entre eles, o LATIN1 é compatível com caracteres em inglês, sendo que um caractere possui um byte; O UTF8 geralmente é usado para codificação internacional, que contém todos os caracteres usados ​​por todos os países, cada caractere contendo três bytes; no GBK, cada caractere possui dois bytes; e o UTF8MB4 (um superconjunto de UTF8) é totalmente compatível com versões anteriores e aceita emojis, cada caractere contendo quatro bytes.
- Recomendação: após adquirir uma instância, você precisa selecionar o conjunto de caracteres apropriado com base no formato de dados exigido em seu negócio para garantir que o cliente e o servidor usem o mesmo conjunto de caracteres, evitando texto ilegível e reinicializações desnecessárias.

### lower_case_table_names
- Valor padrão: 0
- Reinicialização necessária: sim
- Descrição: ao criar um banco de dados ou tabela, você pode definir se as operações de armazenamento e consulta diferenciam maiúsculas de minúsculas. Esse parâmetro pode ser definido como 0 (diferencia maiúsculas de minúsculas) ou 1 (não diferencia maiúsculas de minúsculas). O valor padrão é 0.
- Recomendação: O TencentDB for MySQL diferencia maiúsculas de minúsculas por padrão. Recomendamos que você configure esse parâmetro com base em suas necessidades de negócios e hábitos de uso.

### sql_mode
- Valores padrão:
```
NO_ENGINE_SUBSTITUTION (v5.6); ONLY_FULL_GROUP_BY, STRICT_TRANS_TABLES, NO_ZERO_IN_DATE, NO_ZERO_DATE, ERROR_FOR_DIVISION_BY_ZERO, NO_AUTO_CREATE_USER, NO_ENGINE_SUBSTITUTION (v5.7)
```
- Reinicialização necessária: não
- Descrição: O TencentDB for MySQL pode operar em diferentes modos de SQL, que definem a sintaxe da SQL e a verificação de dados que deve suportar.
O valor padrão deste parâmetro na v5.6 é `NO_ENGINE_SUBSTITUTION`, o que significa que se o mecanismo de armazenamento usado estiver desabilitado ou não compilado, um erro será lançado; na v5.7, os valores padrão são `ONLY_FULL_GROUP_BY, STRICT_TRANS_TABLES, NO_ZERO_IN_DATE, NO_ZERO_DATE, ERROR_FOR_DIVISION_BY_ZERO, NO_AUTO_CREATE_USER, NO_ENGINE_SUBSTITUTION`.
Observações:
 - Se `ONLY_FULL_GROUP_BY` estiver habilitado, o MySQL rejeita consultas para as quais a lista de seleção, condição `HAVING` ou lista `ORDER BY` referem-se a colunas não agregadas que não são nomeadas na cláusula `GROUP BY` nem são funcionalmente dependentes de colunas `GROUP BY`.
 - `STRICT_TRANS_TABLES` habilita o modo SQL estrito. `NO_ZERO_IN_DATE` controla se o servidor permite datas nas quais a parte do ano é diferente de zero, mas a parte do mês ou do dia é zero. O efeito de `NO_ZERO_IN_DATE` depende se o modo SQL estrito está ativado.
 - `NO_ZERO_DATE` controla se o servidor permite uma data zero como válida. Seu efeito depende da ativação do modo SQL estrito.
 - `ERROR_FOR_DIVISION_BY_ZERO` significa que no modo SQL estrito, se os dados forem divididos por zero durante o processo INSERT ou UPDATE, um erro, em vez de um aviso, será gerado, enquanto no modo SQL não estrito, NULL será retornado.
 - `NO_AUTO_CREATE_USER` proíbe a instrução GRANT de criar um usuário cuja senha esteja vazia.
 - `NO_ENGINE_SUBSTITUTION` significa que se o mecanismo de armazenamento estiver desabilitado ou não compilado, um erro será lançado.
- Recomendação: como diferentes modos SQL suportam diferentes sintaxes SQL, recomendamos que você os configure com base em suas necessidades de negócios e hábitos de desenvolvimento.

### long_query_time
- Valor padrão: 10
- Reinicialização necessária: não
- Descrição: usado para definir o limite de tempo para consultas lentas, com o valor padrão de 10 segundos. Se a execução de uma consulta demorar 10 segundos ou mais, os detalhes da execução serão registrados no log lento para análise futura.
- Recomendação: como os cenários de negócios e a sensibilidade do desempenho podem variar, recomendamos que você defina o valor considerando a análise de desempenho futura.

