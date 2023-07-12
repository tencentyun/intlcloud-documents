## Casos de uso comuns
### Deslocalização
- **Armazenamento de dados com alto desempenho e alta confiabilidade**: o Cloud Block Storage (CBS) oferece suporte eficiente à migração dinâmica de CVMs, evitando a interrupção dos negócios causada por falhas físicas. O CBS usa o mecanismo de redundância de dados de três cópias para fazer backup de seus dados e snapshots e recuperar dados em segundos, tornando-o adequado para sistemas de alta carga e de missão crítica.
- **Expansão elástica**: discos em nuvem podem ser montados e desmontados livremente na mesma zona de disponibilidade sem desligar ou reiniciar o CVM. A capacidade do disco em nuvem pode ser configurada elasticamente e expandida sob demanda.
![](https://main.qcloudimg.com/raw/1cdbb7fadac1aa88d823eba12a106522.png)

### Análise de dados em massa
Em uma estrutura de análise de dados offline comum do Spark-HDFS, as leituras/gravações de RDD e as gravações aleatórias de discos são todas de E/S sequencial, exceto para a E/S de leitura aleatória. A E/S sequencial é responsável por 95%. O CBS apresenta um excelente desempenho de taxa de transferência simultânea multithread, permitindo o processamento de dados offline eficiente nos níveis de terabyte e petabyte para Hadoop-Mapreduce, HDFS e Spark.
Com a simultaneidade de vários discos, um único cluster HDFS pode atingir uma taxa de transferência de até 1 GB/s.
O CBS provê suporte a aplicações de big data, como análise de dados, mineração de dados e business intelligence para empresas como Xiaohongshu, Giant Interactive Group, Ele, Yoho!BUY e wepiao.com.
![](https://main.qcloudimg.com/raw/4be675dc660f05c9a7fcd35d9e83973d.png)
**Ambiente de implantação**: 5 servidores do CVM (com 12 núcleos e 40 GB de RAM), simulando a análise de dados offline de um volume de dados de 1,5 TB.
**Desempenho de teste**:

- Cada CVM montou um disco em nuvem HDD de 1 TB. Cinco discos em nuvem HDD fornecem uma velocidade de leitura de 500 MB/s, permitindo que os dados sejam lidos para a memória em 50 minutos.
- Cada CVM montou um SSD de 1 TB, permitindo que os dados sejam lidos para a memória em 25 minutos.

### Banco de dados principal
O SSD é ideal para cenários com altos requisitos de desempenho de E/S e confiabilidade de dados. É principalmente adequado para aplicativos de banco de dados relacionais de médio e grande porte, como PostgreSQL, MySQL, Oracle e SQL Server; para sistemas empresariais centrais com E/S intensiva com altos requisitos de confiabilidade de dados; e para ambientes de desenvolvimento e testes de médio e grande porte com altos requisitos de confiabilidade de dados.
O SSD oferece confiabilidade de dados e alto desempenho. Ele fornece suporte confiável e constante para empresas como Heroes Evolved, Wendao, Yoho!BUY, weipiao.com, Xiaohongshu, etc.
![](https://main.qcloudimg.com/raw/a826f514194aad6d398069b00ab817da.png)
**Ambiente de implantação**: 4 servidores do CVM (com 4 núcleos e 8 GB de RAM). Cada um tem um disco em nuvem SSD de 800 GB montado, com MySQL versão 5.5.42 implantado.
**Desempenho de teste*: simule o teste de desempenho de OLTP usando sysbench, com um conjunto de testes de 10 milhões de registros. Nesse teste, o TPS e o QPS atingem 1.616 e 29.000 respectivamente, o que significa que um único disco é suficiente para suportar 10 mil transações simultâneas por segundo.



## Cenários empresariais comuns para modelos de E/S
- **Persistência de dados por hora**
![](https://main.qcloudimg.com/raw/11e16a3ee744c3cdd313de199b461881.png)
- **Serviços OLTP de alta carga**
![](https://main.qcloudimg.com/raw/a835908f6a9bcaf8407a299607d33dee.png)
- **Cargas ultra-altas periódicas**
![](https://main.qcloudimg.com/raw/66b6e76d8cc2d477698a21e12cffff8d.png)
- **Leitura-gravação sequencial contínua**
![](https://main.qcloudimg.com/raw/f08c8eb9b38a1bf0a94cec35fea5538e.png)
