O Cloud Block Storage (CBS) é um dispositivo de bloco de rede com alta disponibilidade, altamente confiável, de baixo custo e personalizável que pode ser usado como um disco autônomo e expansível para os CVMs. O CBS usa um mecanismo distribuído de três cópias para armazenar dados no nível do bloco de dados e garantir a confiabilidade dos dados. O CBS é classificado em dois tipos: **SSD** e **Premium Cloud Storage**. Cada tipo tem desempenho e características exclusivos, e o preço varia, tornando o CBS adequado para diferentes casos de uso.

- **SSD**: o SSD usa SSD NVMe como mídia de armazenamento e emprega um mecanismo distribuído de três cópias. Ele oferece armazenamento de alto desempenho com baixa latência, alto IOPS aleatório, E/S de alta taxa de transferência e segurança de dados de até 99,9999999%, tornando-o adequado para aplicativos com altos requisitos de desempenho de E/S.
- **Premium Cloud Storage**: o Tencent Cloud Premium Cloud Storage é um tipo de armazenamento híbrido. Ele adota o mecanismo de cache para fornecer um armazenamento semelhante ao SSD de alto desempenho e emprega um mecanismo distribuído de três cópias para garantir a confiabilidade dos dados. O Premium Cloud Storage é adequado para aplicativos de pequeno e médio porte com altos requisitos de confiabilidade de dados e requisitos padrão de desempenho, bem como para aplicativos de banco de dados relacionais de pequeno e médio porte, como MySQL, SQL Server e PostgreSQL.


A tabela abaixo compara os desempenhos do SSD e do Premium Cloud Storage.

|        Métrica de desempenho       | SSD                                                    | Premium Cloud Storage                                                | 
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | 
| IOPS aleatório       | IOPS aleatório máximo = 1.800 + capacidade de armazenamento (GB) × 30<br/>O IOPS aleatório máximo não ultrapassa 26.000 | IOPS aleatório máximo = 1.800 + capacidade de armazenamento (GB) × 8<br>O IOPS aleatório máximo não ultrapassa 6.000 |  
| Taxa de transferência (MB/s) | Taxa de transferência máxima = 120 + capacidade de armazenamento (GB) × 0,2<br/>A taxa de transferência máxima não ultrapassa 260 MB/s | Taxa de transferência máxima = 100 + capacidade de armazenamento (GB) × 0,15<br>A taxa de transferência máxima não ultrapassa 150 MB/s |  
| Latência           | < 3 ms                                                 | < 4 ms                                                 | 

A principal diferença entre o **SSD** e o **Premium Cloud Storage** é o requisito de E/S.

O SSD é mais adequado para aplicativos com uso intensivo de E/S, incluindo:
- Alto desempenho e alta confiabilidade de dados: adequado para sistemas empresariais de missão crítica e de alta carga. O SSD fornece redundância de dados de três cópias e é equipado com recursos abrangentes para backup de dados, snapshots e restauração de dados em segundos.
- Bancos de dados de médio e grande porte: é compatível com aplicativos de banco de dados relacionais de médio e grande porte que contêm tabelas com milhões de linhas, como MySQL, Oracle, SQL Server e MongoDB.
- NoSQL de grande porte: é compatível com empresas com NoSQL, como HBase e Cassandra.
- Sistemas empresariais centrais: adequado para aplicativos com uso intensivo de E/S e outros sistemas empresariais centrais com altos requisitos de confiabilidade de dados.
- Análise de big data: adequado para análise de dados, mineração de dados, business intelligence e outras áreas. Fornece capacidades de processamento distribuídas para dados em níveis de TB e PB.

**O Premium Cloud Storage é adequado para os seguintes cenários de dados**:
- Adequado para bancos de dados de pequeno e médio porte e servidores web. Fornece desempenho de E/S estável e de longo prazo.
- Adequado para cenários com requisitos equilibrados de capacidade e desempenho de armazenamento, como serviços de escritório corporativo e serviços de log.
- Atende aos requisitos de E/S para os testes empresariais principais e para o desenvolvimento de ambientes de teste conjuntos.
  

Os preços dos dois tipos de discos em nuvem variam de acordo com a região. O SSD de alto desempenho geralmente tem o preço mais alto. Para obter detalhes de preços, consulte a [Visão geral de preços](https://intl.cloud.tencent.com/document/product/362/2413).
