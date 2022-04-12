O TencentDB for MySQL fornece três tipos de arquiteturas: nó único, dois nós e três nós. Este documento descreve a arquitetura de dois nós.

- As instâncias de dois nós adotam uma arquitetura de uma source e uma réplica altamente disponível, e permitem o backup dinâmico em tempo real, a detecção automática de falhas e o failover automático.
- As instâncias de dois nós fornecem duas políticas de isolamento de recursos: geral e dedicada. Para mais informações, consulte [Política de isolamento de recursos](https://intl.cloud.tencent.com/document/product/236/39794).

## Casos de uso
As instâncias de dois nós são ideais para setores como jogos, internet, IoT, varejo, comércio eletrônico, logística, seguros e títulos.

## Funcionalidades
- A arquitetura de dois nós fornece dois modos de replicação de source/réplica: assíncrona (padrão) e semissincronizada. Você pode modificar o modo de replicação ou [fazer upgrade para a arquitetura de três nós](https://intl.cloud.tencent.com/document/product/236/35986) (com o modo de sincronização forte de uma source e duas réplicas) na página de detalhes da instância no [Console](https://console.cloud.tencent.com/cdb).
- A arquitetura de dois nós fornece um conjunto completo de funcionalidades, incluindo instâncias somente leitura, grupos de segurança, migração de dados e implantação Multi-AZ. Para mais informações, consulte [Vantagens](https://intl.cloud.tencent.com/document/product/236/5148).
- A arquitetura de dois nós alcança uma alta disponibilidade de até 99,95%. Para mais informações, consulte [Acordo de nível de serviço do TencentDB (nova versão)](https://intl.cloud.tencent.com/document/product/301/30977).
- A instância de dois nós fornece várias réplicas para garantir a persistência dos dados. Os dados do nó de source podem ser sincronizados com o nó de réplica; os dados da instância de source podem ser sincronizados com as instâncias somente leitura (se houver). Essa arquitetura garante a segurança dos dados e alcança uma persistência de dados de até 99,99999%.
- A arquitetura de dois nós implanta nós de dados em dispositivos de hardware poderosos e usa discos SSD NVMe locais como armazenamento subjacente com um IOPS de até 240 mil (este valor é o resultado do teste com o tamanho de página padrão do MySQL de 16 KB e serve apenas para referência. O valor real depende da configuração específica, do tamanho da página e da carga de negócios).

## Diagrama de estrutura básica
![Alt text](https://main.qcloudimg.com/raw/19d5619f983d3dc550b3218c0520b447.png)

## Upgrade
- É possível fazer o upgrade das versões do mecanismo do TencentDB for MySQL. Para mais informações, consulte [Upgrade de mecanismos de banco de dados](https://intl.cloud.tencent.com/document/product/236/8126).
- É possível fazer o upgrade do TencentDB for MySQL da arquitetura de dois nós para a arquitetura de três nós. Para mais informações, consulte [Upgrade de instâncias de dois nós para três nós](https://intl.cloud.tencent.com/document/product/236/35986).
- É possível fazer o upgrade das versões secundárias do kernel do TencentDB for MySQL de forma automática ou manual. Para mais informações, consulte [Upgrade das versões secundárias do kernel](https://intl.cloud.tencent.com/document/product/236/36816).
