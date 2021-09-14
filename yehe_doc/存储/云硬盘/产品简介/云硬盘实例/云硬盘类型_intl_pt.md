O Cloud Block Storage (CBS) fornece um dispositivo de bloco de rede com alta disponibilidade, altamente confiável, de baixo custo e personalizável que pode ser usado como um disco autônomo e expansível para os CVMs. O CBS armazena dados no nível dos blocos de dados em um mecanismo distribuído de três cópias, de modo a garantir a confiabilidade dos dados. O CBS é classificado em três tipos: **Premium**, **SSD** e **Enhanced SSD**. Cada tipo oferece desempenho e funcionalidades exclusivos a preços diferentes, tornando o CBS adequado para diferentes casos de uso.

>!
>- Atualmente, o Enhanced SSD está disponível apenas na Zona 3 de Guangzhou, Zona 4 de Guangzhou, Zona 2 de Xangai, Zona 3 de Xangai, Zona 5 de Xangai, Zona 3 de Pequim, Zona 4 de Pequim, Zona 1 de Chengdu, Zona 1 de Chongqing, Zona 1 de Nanquim e na Zona 2 de Nanquim. Haverá suporte em mais zonas de disponibilidade.
>- O desempenho do Enhanced SSD só é garantido quando ele é montado nos modelos S5, M5, SA2, IT3 e D3 criados após 1º de agosto de 2020 e todos os modelos de geração posterior.
>- Não é possível usar o Enhanced SSD como disco do sistema.
>- Não é possível criptografar o Enhanced SSD.
>- Não é possível fazer o upgrade do Enhanced SSD a partir de outros tipos de discos.

- **Premium Cloud Storage**: o Tencent Cloud Premium Cloud Storage é um tipo de armazenamento híbrido. Ele adota o mecanismo de cache para fornecer um armazenamento semelhante ao SSD de alto desempenho e emprega um mecanismo distribuído de três cópias para garantir a confiabilidade dos dados. O Premium Cloud Storage é adequado para aplicações de pequeno e médio porte com altos requisitos de confiabilidade de dados e requisitos gerais de desempenho, como servidores Web/de aplicativos, processamento empresarial lógico, assim como sites de pequeno e médio porte.
- **SSD**: o SSD usa SSD NVMe como mídia de armazenamento e emprega um mecanismo distribuído de três cópias. Ele oferece serviço de armazenamento com baixa latência, IOPS aleatório alto, E/S de alta taxa de transferência e segurança de dados de até 99,9999999%, tornando-o adequado para aplicativos com altos requisitos de desempenho de E/S.
- **Enhanced SSD**: o Enhanced SSD conta com o mecanismo de armazenamento mais recente do Tencent Cloud, a mídia de armazenamento SSD NVMe e a infraestrutura de rede mais recente. Ele emprega um mecanismo distribuído de três cópias para fornecer armazenamento de alto desempenho com baixa latência, IOPS aleatório alto, E/S de alta taxa de transferência e segurança de dados de até 99,9999999%, tornando-o adequado para aplicações de E/S intensiva com altos requisitos para latência, como bancos de dados e NoSQL de grande porte.


A tabela a seguir compara o desempenho dos três serviços do CBS.

|        Métrica de desempenho       |               Enhanced SSD Cloud Storage             | SSD Cloud Storage                                                    | Premium Cloud Storage                                                 |
| -------------- | ------------------------------|------------------------------ | ------------------------------------------------------------ |
| Tamanho máximo (GB)     | 32.000 | 32.000 | 32.000 |
| IOPS máximo    | 50.000 | 26.000 | 6.000 |
| Desempenho do IOPS aleatório      | IOPS aleatório máximo = 1.800 + capacidade de armazenamento (GB) × 50<br/>O IOPS aleatório máximo não ultrapassa 50.000 | IOPS aleatório máximo = 1.800 + capacidade de armazenamento (GB) × 30<br/>O IOPS aleatório máximo não ultrapassa 26.000 | IOPS aleatório máximo = 1.800 + capacidade de armazenamento (GB) × 8<br>O IOPS aleatório máximo não ultrapassa 6.000. |
| Taxa de transferência máxima (MB/s)    | 350 MB/s | 260 MB/s | 150 MB/s |
| Desempenho da taxa de transferência (MB/s) | Taxa de transferência máxima = 120 + capacidade de armazenamento (GB) × 0,5<br/>A taxa de transferência máxima não ultrapassa 350 MB/s | Taxa de transferência máxima = 120 + capacidade de armazenamento (GB) × 0,2<br/>A taxa de transferência máxima não ultrapassa 260 MB/s | Taxa de transferência máxima = 100 + capacidade de armazenamento (GB) × 0,15<br>A taxa de transferência máxima não ultrapassa 150 MB/s |
| Latência de leitura/gravação aleatória de 1 rodada           | 0,3-1 ms                                                    | 0,5-3 ms                                                    | 0,8-4 ms                                                    |


A principal diferença entre o **Enhanced SSD**, o **SSD** e o **Premium Cloud Storage** é o desempenho de E/S.

**O Enhanced SSD é mais adequado para cenários sensíveis à latência ou de E/S intensiva**, incluindo:
- Alto desempenho e alta confiabilidade de dados: adequado para sistemas empresariais de missão crítica e de alta carga. O SSD fornece redundância de dados de três cópias e é equipado com recursos abrangentes para backup de dados, snapshots e restauração de dados em segundos.
- Bancos de dados de médio e grande porte: é compatível com aplicativos de banco de dados relacionais de médio e grande porte que contêm tabelas com milhões de linhas, como MySQL, Oracle, SQL Server e MongoDB.
- NoSQL de grande porte: é compatível com empresas com NoSQL, como HBase e Cassandra.
- ElasticSearch: é compatível com o armazenamento de E/S de baixa latência.
- Serviço de vídeo: adequado para aplicações com altos requisitos de largura de banda de armazenamento, como codificação e decodificação de áudio/vídeo, transmissão ao vivo e reprodução de gravações.
- Sistemas empresariais centrais: adequado para aplicações com uso de E/S intensiva e outros sistemas empresariais centrais com altos requisitos de confiabilidade de dados.
- Análise de big data: adequado para análise de dados, mineração de dados, business intelligence e outras áreas. Fornece capacidades de processamento distribuídas para dados em níveis de TB e PB.

**O SSD é adequado para aplicações com cargas altas e médias**, incluindo:
- Bancos de dados de médio e grande porte: aplicações de banco de dados relacionais de médio e grande porte, como MySQL.
- Processamento de imagens: é compatível com a análise de dados e negócios de armazenamento, como processamento de imagens.

**O Premium Cloud Storage é adequado principalmente para os seguintes cenários de dados**:
- Bancos de dados de pequeno e médio porte e servidores Web/de aplicativos. Fornece desempenho de E/S estável e de longo prazo.
- Cenários que requerem capacidade de armazenamento e desempenho equilibrados, como serviços de escritório corporativo.
- Teste empresariais centrais e depuração de front-end e back-end
  

Para obter detalhes de preços dos discos em nuvem, consulte a [Visão geral de preços](https://intl.cloud.tencent.com/document/product/362/2413).
