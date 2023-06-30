
### O que é a instância Big Data D1?

A instância Big Data D1 foi criada especificamente para computação distribuída do Hadoop, processamento de log em massa, sistema de arquivos distribuído, grande data warehouse e outros cenários de atividades. Esse tipo de instância da CVM é usado principalmente para solucionar problemas de computação em nuvem e armazenamento de dados corporativos em massa.

### A quais clientes/setores e cenários de atividades as instâncias Big Data D1 se aplicam?

A instância Big Data D1 é aplicável a clientes nos setores de Internet, jogos, finanças e outros que exigem computação de big data e análise de armazenamento, assim como cenários de atividades que exigem armazenamento de dados em massa e computação offline. Ela pode atender aos requisitos de armazenamento, capacidade e largura de banda de rede privada das atividades de computação distribuída representados pelo Hadoop.
Além disso, com a estrutura arquitetônica altamente disponível de atividades de computação distribuída representadas pelo Hadoop, a instância Big Data D1 possui um design de armazenamento local para nivelar o custo total com o cluster Hadoop físico em um IDC offline, garantindo capacidade de armazenamento em massa e alto desempenho.

### Funcionalidades da instância Big Data D1

* Uma única instância tem capacidade de taxa de transferência de até 2,3 GB/s. O disco local HDD é a melhor escolha para armazenamento com alta taxa de transferência. Com taxa de transferência de leitura/gravação sequencial estável e de alto desempenho, a instância Big Data D1 foi criada especificamente para computação distribuída do Hadoop, processamento de log em massa, grande data warehouse e outros cenários de atividades.
* O armazenamento local tem um preço unitário baixo em torno de 1/10. A instância Big Data D1 apresenta grande capacidade de armazenamento e alto desempenho, ao mesmo tempo em que garante ótima relação custo-benefício para cenários de big data. Ela tem um custo total próximo ao do cluster Hadoop físico em um IDC offline.
* A latência de leitura/gravação é minimizada para 2 ms a 5 ms. A instância Big Data D1, com seu modelo de alto desempenho e nível empresarial, é adequada para desenvolvedores corporativos.
*O método de faturamento de pagamento conforme o uso é permitido.

### Especificações da instância Big Data D1

| Modelo | vCPU (núcleo) | Memória (GB) | Disco de dados local | Largura de banda da rede privada | Observação |
|-------|----|------|------|------|------|
| D1.2XLARGE32 | 8 | 32 | 2 × 3720 GB | 1,5 Gbps | - |
| D1.4XLARGE64 | 16 | 64 | 4 × 3720 GB | 3 Gbps | - |
| D1.6XLARGE96 | 24 | 96 | 6 × 3720 GB | 4,5 Gbps | - |
| D1.8XLARGE128 | 32 | 128 | 8 × 3720 GB | 6 Gbps | - |
| D1.14XLARGE224 | 56 | 224 | 12× 3720 GB | 10 Gbps | Exclusiva para host |

### Observações sobre o armazenamento de dados local da instância Big Data D1

A instância Big Data D1 usa o disco local como o disco de dados, o que pode levar à **perda de dados** (por exemplo, quando o host trava). Se sua aplicação não puder garantir a confiabilidade dos dados, recomendamos que você escolha uma instância que possa usar o disco em nuvem como o disco de dados.

A relação entre operar em uma instância com disco local e a retenção de dados é a seguinte:

| Operação | Status do disco de dados local | Descrição |
|------|-----|-----|
| Reinicialização do sistema operacional/Reinicialização do console/Reinicialização forçada | Retido | O armazenamento no disco local é retido. Os dados são retidos. |
| Desligamento do sistema operacional/Desligamento do console/Desligamento forçado | Retido | O armazenamento no disco local é retido. Os dados são retidos. |
| Encerramento (da instância) no console | Apagado | O armazenamento no disco local é apagado. Nenhum dado é retido. |

> Não armazene dados de atividades que precisem ser retidos por muito tempo no disco local. Faça backup dos dados com antecedência e use uma arquitetura de alta disponibilidade. Para retenção de longo prazo, recomendamos que você armazene os dados no disco do CBS.

### Como posso adquirir o disco local da Big Data D1?

O disco local não pode ser adquirido separadamente. Você só pode adquirir o disco local ao criar a instância D1. A quantidade e a capacidade dos discos locais dependem das especificações da instância.

### O armazenamento local da instância Big Data D1 aceita snapshots?
Não.

### A instância Big Data D1 permite o ajuste de configuração e o failover?

O ajuste de configuração não é permitido.
A instância Big Data D1 apresenta armazenamento de dados em massa e usa o HDD local como o disco de dados. Esse tipo de instância não permite o failover de disco de dados (por exemplo, quando o host trava ou o disco local é danificado). Para evitar a perda de dados, recomendamos que você use uma política de redundância, por exemplo, um sistema de arquivos que permita a redundância e a tolerância a falhas (como o HDFS e o Mapr-FS). Além disso, recomendamos que você faça backup frequente dos dados em um sistema de armazenamento permanente, como o COS da Tencent. Para mais informações, consulte o [Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436).
Depois que um disco local é danificado, você precisa desligar a instância da CVM para que possamos alterar o disco local. Se a instância da CVM tiver falhado, vamos notificar e corrigir o problema.

### Em quais regiões posso adquirir a instância Big Data D1?

As seguintes zonas de disponibilidade são compatíveis:
* Zona 2 de Xangai
* Zona 2 de Pequim
* Zona 3 de Guangzhou


### Por que não consigo encontrar o disco de dados após adquirir uma instância Big Data D1?

O disco local de uma instância Big Data D1 não é montado automaticamente. Você pode montá-lo conforme a demanda.

### Qual é a diferença entre a instância Big Data D1 e a instância Alta E/S I2?

A instância Alta E/S I2 é uma instância da CVM criada especificamente para cenários de atividades com baixa latência e alta E/S aleatória. Possui desempenho de IOPS ultra-alto e é usada principalmente para banco de dados de alto desempenho (banco de dados relacional, NoSQL etc.). A instância Big Data D1 é uma instância da CVM criada especificamente para cenários de atividades que exigem muita leitura/gravação sequencial e armazenamento de dados em massa e de baixo custo. Possui armazenamento de alto desempenho aliado a baixo custo e largura de banda de rede privada devidamente configurada.

### Como é a taxa de transferência do disco da instância Big Data D1?

Considere D1.14XLARGE224 como exemplo, a taxa de transferência de leitura/gravação sequencial do disco local de instâncias Big Data D1 é a seguinte:
* Para um único disco, a velocidade de leitura/gravação sequencial é de mais de 190 MB/s (128 KB de tamanho de bloco e profundidade de 32).
* Para 12 discos, a velocidade de leitura/gravação sequencial simultânea é de mais de 2,3 GB/s (128 KB de tamanho de bloco e profundidade de 32).

### Qual é a diferença entre o disco local da instância Big Data D1 e o CBS?

O [Cloud Block Storage](https://intl.cloud.tencent.com/document/product/362) fornece um dispositivo de armazenamento altamente eficiente e confiável para a instância da CVM. É um dispositivo de armazenamento em bloco personalizável com alta disponibilidade, alta confiabilidade e baixo custo, podendo ser usado como um disco expansível independente para a CVM. Ele fornece armazenamento de dados a nível de blocos de dados e emprega um mecanismo distribuído de cópias triplas para garantir a confiabilidade dos dados da instância da CVM, atendendo aos requisitos de diferentes cenários de aplicação. O disco local da instância Big Data D1 foi criado especificamente para cenários de atividades que exigem muita leitura/gravação sequencial para grandes conjuntos de dados locais, como computação distribuída do Hadoop, computação paralela em grande escala e data warehouse.

