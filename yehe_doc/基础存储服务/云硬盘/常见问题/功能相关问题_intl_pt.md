### O que é o Tencent Cloud Block Storage?
O Tencent Cloud Block Storage (CBS) é um dispositivo de armazenamento em blocos altamente disponível e confiável para instâncias do CVM. Ele fornece vários tipos de discos para atender a diversos requisitos de leitura/gravação. Para obter mais informações sobre o CBS, consulte [Visão geral](https://intl.cloud.tencent.com/document/product/362/2345).
Nós recomendamos o CBS quando os dados mudam frequentemente e você quer armazená-los de forma persistente a uma velocidade de leitura/gravação maior. O CBS pode ser montado em qualquer instância em execução na mesma zona de disponibilidade, permitindo que você use um sistema de arquivos e armazenamento de banco de dados da instância sem seguir o ciclo de vida útil dela. Para obter mais informações sobre as operações do CBS, consulte [Visão geral das operações](https://intl.cloud.tencent.com/document/product/362/33140).

### Quais são as funcionalidades do Tencent Cloud CBS?
O Tencent Cloud CBS vem com quatro tipos de discos: Premium Cloud Storage, SSD, Enhanced SSD e Tremendous SSD. Os quatro tipos apresentam as seguintes funcionalidades:
- Montagem e desmontagem elásticas: os discos em nuvem elásticos podem ser montados e desmontados. É possível montar até 20 discos em nuvem elásticos em um CVM como discos de dados. 
- Expansão elástica: um único disco permite uma capacidade máxima de 32 TB. Você pode expandir o disco a qualquer momento.
- Backup por snapshots: você pode criar um snapshot para fazer backup dos dados. Isso melhora a confiabilidade dos dados e permite uma restauração rápida dos dados quando necessário. Você também pode criar um disco em nuvem a partir do snapshot para agilizar a implantação dos seus negócios.

### Qual é a diferença entre o COS e o CBS?
- O [Cloud Object Storage (COS)](https://intl.cloud.tencent.com/document/product/436) está disponível via APIs da Web e não se restringe a sistemas de arquivos, estrutura do diretório, quantidade de arquivos ou capacidade de armazenamento. O serviço oferece vários SDKs e ferramentas para integração de negócios, o que também pode ser usado de forma independente do CVM. O COS é ideal quando você precisa acessar uma grande quantidade de dados, mas não é adequado para resposta no nível de milissegundos ou em cenários de leitura/gravação aleatória.
- O [CBS](https://intl.cloud.tencent.com/document/product/362) precisa ser usado em conjunto com o CVM e só pode ser montado e usado após o sistema de arquivos ter sido particionado ou formatado. O COS e o CBS têm métricas de desempenho distintas para casos de uso diferentes.

### Quais são os limites dos discos em nuvem?
- Um único disco em nuvem elástico pode ser expandido até 32 TB e não pode ser reduzido.
- Os discos em nuvem elásticos só podem ser montados em CVMs que estejam na mesma zona de disponibilidade.
- É possível montar até 20 discos em nuvem elásticos em um único CVM como discos de dados. Você pode montar discos em nuvem elásticos diretamente em um CVM que você esteja adquirindo ou [fazer isso depois](https://intl.cloud.tencent.com/document/product/362/32401).
- Você pode adquirir até 50 discos em nuvem elásticos de uma vez no [console do CBS](https://console.cloud.tencent.com/cvm/cbs).


### Quais são as vantagens de discos em nuvem?
Os discos em nuvem apresentam alta confiabilidade, elasticidade e desempenho. Eles são fáceis de usar e permitem o backup por snapshots. Para obter mais informações, consulte [Vantagens do produto](https://intl.cloud.tencent.com/document/product/362/3039).

### Os discos em nuvem elásticos podem ser usados como discos do sistema?
Não. Apenas os discos em nuvem não elásticos podem ser usados como discos do sistema.

[](id:Q1)
### Os discos em nuvem podem ser usados como disco de dados?
Sim. Todos os tipos de discos locais e discos em nuvem podem ser usados como discos de dados.

### Os discos em nuvem podem ser montados e desmontados?
- Os discos em nuvem podem ser montados e desmontados quando estão sendo usados como discos de dados.
- Entretanto, eles não podem ser montados ou desmontados quando estão sendo usados como discos do sistema.

### Os discos em nuvem elásticos podem ser montados e desmontados em lotes?
- Os discos em nuvem elásticos podem ser montados e desmontados em lotes.
- Os discos em nuvem não elásticos não podem ser montados e desmontados em lotes.
