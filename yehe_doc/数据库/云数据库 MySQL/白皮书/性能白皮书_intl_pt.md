## Ferramenta de teste
O Sysbench 0.5 é a ferramenta usada para testar o desempenho do benchmark do banco de dados.

Configuração da ferramenta:
O script OTLP que vem com o Sysbench foi modificado. Especificamente, a proporção de leitura/gravação foi alterada para 1:1 e controlada pelos parâmetros de comando de teste `oltp_point_selects` e `oltp_index_updates`. Neste documento, todos os casos de teste envolvem quatro operações SELECT e uma operação UPDATE com a proporção de leitura/gravação de 4:1.

#### Instalação da ferramenta
Execute o seguinte código para instalar o Sysbench 0.5:
```
git clone https://github.com/akopytov/sysbench.git
git checkout 0.5
yum -y install make automake libtool pkgconfig libaio-devel
yum -y install mariadb-devel
./autogen.sh
./configure
make -j
make install
```
>?As instruções de instalação acima se aplicam ao teste de estresse de desempenho em uma instância da CVM do CentOS. Para obter instruções sobre como instalar a ferramenta em outros sistemas operacionais, consulte a [documentação oficial do Sysbench](https://github.com/akopytov/sysbench?spm=a2c4g.11186623.2.12.36061072oZL2qS).

## Ambiente de teste

| Tipo | Descrição |
|--|--|
| Máquina física | Uma única máquina pode aceitar instâncias de banco de dados de dois nós com até 488 GB de memória e 6 TB de disco |
| Especificação da instância | Especificações normalmente disponíveis (consulte os [casos de teste](#cscs) abaixo) |
| Configuração do cliente | CPU de 4 núcleos e 8 GB de memória |
| Quantidade de clientes | 1 a 6 (mais clientes precisam ser adicionados à medida que é feito o upgrade da configuração) |
| Ambiente de rede | Data center com conexão de 10 Gigabits e latência de rede abaixo de 0,05 ms |
| Carga do ambiente | A carga na máquina onde o MySQL está instalado é acima de 70% (para instâncias não exclusivas) |

- Observação sobre a especificação do cliente: máquinas clientes de alta especificação são usadas para garantir que o desempenho da instância do banco de dados possa ser medido por meio de testes de estresse em um único cliente. Para clientes de baixa especificação, recomendamos usar vários clientes para testes de estresse simultâneos e agregar os resultados.
- Observação sobre a latência de rede: no ambiente de teste, é necessário garantir que os clientes e as instâncias de banco de dados estejam na mesma zona de disponibilidade para evitar que o resultado do teste seja afetado por fatores de rede.

## Método do teste
### 1. Estrutura de tabelas de banco de dados de teste
```
CREATE TABLE `sbtest1` ( 
`id` int(10) unsigned NOT NULL AUTO_INCREMENT, 
`k` int(10) unsigned NOT NULL DEFAULT '0', 
`c` char(120) NOT NULL DEFAULT '', 
`pad` char(60) NOT NULL DEFAULT '',
 PRIMARY KEY (`id`), KEY `k_1` (`k`) 
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

### 2. Formato das linhas de dados de teste
```
id: 1
k: 20106885
c: 08566691963-88624912351-16662227201-46648573979-64646226163-77505759394-75470094713-41097360717-15161106334-50535565977
pad: 63188288836-92351140030-06390587585-66802097351-4928296184
```

### 3. Preparações de dados
```
sysbench --mysql-host=xxxx --mysql-port=xxxx --mysql-user=xxx --mysql-password=xxx --mysql-db=test --mysql-table-engine=innodb --test=tests/db/oltp.lua --oltp_tables_count=20 --oltp-table-size=10000000  --rand-init=on prepare
```

Descrições dos parâmetros de preparação de dados:
- `--test=tests/db/oltp.lua` indica para implementar o teste OLTP chamando o script `tests/db/oltp.lua`.
- `--oltp_tables_count=20` indica que a quantidade de tabelas para teste é 20.
- `--oltp-table-size=10000000` indica que cada tabela de teste é preenchida com 10 milhões de linhas de dados.
- `--rand-init=on` indica que cada tabela de teste é preenchida com dados aleatórios.
  

### 4. Comando para teste de estresse
```
sysbench --mysql-host=xxxx --mysql-port=xxx --mysql-user=xxx --mysql-password=xxx --mysql-db=test --test=/root/sysbench_for_z3/sysbench/tests/db/oltp.lua --oltp_tables_count=xx --oltp-table-size=xxxx --num-threads=xxx --oltp-read-only=off --rand-type=special --max-time=600 --max-requests=0 --percentile=99 --oltp-point-selects=4 run
```

Descrições dos parâmetros de teste de estresse:
- `--test=/root/sysbench_for_z3/sysbench/tests/db/oltp.lua` indica para implementar o teste OLTP chamando o script `/root/sysbench_for_z3/sysbench/tests/db/oltp.lua`.
- `--oltp_tables_count=20` indica que a quantidade de tabelas para teste é 20.
- `--oltp-table-size=10000000` indica que cada tabela de teste é preenchida com 10 milhões de linhas de dados.
- `--num-threads=128` indica que as conexões simultâneas de clientes para teste são 128.
- `--oltp-read-only=off` indica que o modelo de teste somente leitura está desativado e o modelo híbrido de leitura/gravação é usado.
- `--rand-type=special` indica que o modelo aleatório é específico.
- `--max-time=1800` indica o tempo de execução deste teste.
- `--max-requests=0` indica que nenhum limite é imposto à quantidade total de solicitações e o teste é executado de acordo com `max-time`.
- `--percentile=99` indica a taxa de amostragem. Aqui, 99 significa descartar 1% de solicitações longas de todas as solicitações e considerar o valor máximo entre as solicitações restantes de 99%. O valor padrão é 95%.
- `--oltp-point-selects=4` indica que a quantidade de operações SELECT no comando de teste do SQL no script OLTP é 4. O valor padrão é 1.

### 5. Modelo de cenário
Todos os casos de teste neste documento adotam o script `lua` do Sysbench que foi modificado para executar quatro operações SELECT e uma operação UPDATE (coluna de índice) com a proporção de leitura/gravação em 4:1.
Para a configuração máxima, o modelo de ajuste de parâmetros é adicionado ao cenário de dados. Para obter os resultados do teste, consulte [Resultados do teste](#document_test_result) abaixo.


<span id="cscs"></span>
## Parâmetros do teste

| Especificação da instância | Capacidade de armazenamento | Quantidade de tabelas | Quantidade de linhas | Tamanho do conjunto de dados | Simultaneidade | Tempo de execução (minutos) |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1 núcleo, 1 GB|200 GB|4|20 milhões |19 GB|128|30|
|1 núcleo, 2 GB|200 GB|4|40 milhões |38 GB|128|30|
|2 núcleos, 4 GB|200 GB|8|40 milhões|76 GB|128|30|
|4 núcleos, 8 GB|200 GB|15|40 milhões |142 GB|128|30|
|4 núcleos, 16 GB|400 GB|25|40 milhões|238 GB|128|30|
|8 núcleos, 32 GB|700 GB|25|40 milhões|238 GB|128|30|
|16 núcleos, 64 GB|1 TB|40|40 milhões|378 GB|256|30|
|16 núcleos, 96 GB|1,5 TB|40|40 milhões|378 GB|128|30|
|16 núcleos, 128 GB|2 TB|40|40 milhões|378 GB|128|30|
|24 núcleos, 244 GB|3 TB|60|40 milhões|567 GB|128|30|
|48 núcleos, 488 GB|6 TB|60|40 milhões|567 GB|128|30|
|48 núcleos, 488 GB (ajustado)|6 TB|60|10 milhões|140 GB|128|30|

<span id="document_test_result"></span>
## Resultados dos testes

| Especificação da instância | Capacidade de armazenamento | Conjunto de dados | Quantidade de clientes | Simultaneidade de cliente único | QPS | TPS |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1 núcleo, 1 GB|200 GB|19 GB|1|128|1.757|97|
|1 núcleo, 2 GB|200 GB|38 GB|1|128|3.016|167|
|2 núcleos, 4 GB|200 GB|76 GB|1|128|4.082|816|
|4 núcleos, 8 GB|200 GB|142 GB|1|128|6.551|1.310|
|4 núcleos, 16 GB|400 GB|238 GB|1|128|11.098|2.219|
|8 núcleos, 32 GB|700 GB|238 GB|2|128|20.484|3.768|
|16 núcleos, 64 GB|1 TB|378 GB|2|128|36.395|7.279|
|16 núcleos, 96 GB|1,5 TB|378 GB|3|128|56.464|11.292|
|16 núcleos, 128 GB|2 TB|378 GB|3|128|81.752|16.350|
|24 núcleos, 244 GB|3 TB|567 GB|4|128|98.528|19.705|
|48 núcleos, 488 GB|6 TB|567 GB|6|128|142.246|28.449|
|48 núcleos, 488 GB (ajustado)|6 TB|140 GB|6|128|245.509|46.304|
