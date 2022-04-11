O TencentDB for MySQL fornece três tipos de arquiteturas: nó único (single-node), dois nós (two-node) e três nós (three-node). Este documento descreve a arquitetura de três nós.

- As instâncias de três nós adotam uma arquitetura de uma source e duas réplicas, e permitem a replicação de sincronização forte. Elas garantem uma forte consistência de dados por meio de backup dinâmico em tempo real, e fornecem confiabilidade de nível financeiro e alta disponibilidade.
- As instâncias de três nós apresentam duas políticas de isolamento de recursos: geral e dedicada. Para mais informações, consulte [Política de isolamento de recursos](https://intl.cloud.tencent.com/document/product/236/39794).

## Casos de uso
As instâncias de três nós são ideais para setores como jogos, internet, IoT, varejo, comércio eletrônico, logística, seguros e títulos.

## Funcionalidades
- A arquitetura de três nós fornece modos de replicação de source/réplica como assíncrona (padrão), sincronização forte e semissincronizada.
- A arquitetura de três nós fornece um conjunto completo de funcionalidades, incluindo instâncias somente leitura, grupos de segurança, migração de dados e implantação Multi-AZ. Para mais informações, consulte [Vantagens](https://intl.cloud.tencent.com/document/product/236/5148).
- A arquitetura de três nós alcança uma alta disponibilidade de até 99,99%. Para mais informações, consulte [Acordo de nível de serviço do TencentDB (nova versão)](https://intl.cloud.tencent.com/document/product/301/30977).
- A instância de três nós fornece várias réplicas para garantir a persistência dos dados. Os dados do nó de source podem ser sincronizados com os nós de réplica; os dados da instância de source podem ser sincronizados com as instâncias somente leitura (se houver). Essa arquitetura garante a segurança dos dados e alcança uma persistência de dados de até 99,99999%.
- A arquitetura de três nós implanta nós de dados em dispositivos de hardware poderosos e usa discos SSD NVMe locais como armazenamento subjacente com um IOPS de até 240 mil (este valor é o resultado do teste com o tamanho de página padrão do MySQL de 16 KB e serve apenas para referência. O valor real depende da configuração específica, do tamanho da página e da carga de negócios).
- Você pode implantar os dois nós de réplica de uma instância de três nós na mesma zona de disponibilidade (por exemplo, Zona 5 de Pequim), mas a estratégia de distribuição de nós padrão do TencentDB garante que eles sejam implantados em servidores físicos diferentes. Você também pode implantar os dois nós de réplica em zonas de disponibilidade diferentes (por exemplo, um nó de réplica na Zona 5 de Pequim e outro na Zona 7 de Pequim).


## Upgrade
- É possível fazer o upgrade das versões do mecanismo do TencentDB for MySQL. Para mais informações, consulte [Upgrade de mecanismos de banco de dados](https://intl.cloud.tencent.com/document/product/236/8126).
- É possível fazer o upgrade das versões secundárias do kernel do TencentDB for MySQL de forma automática ou manual. Para mais informações, consulte [Upgrade das versões secundárias do kernel](https://intl.cloud.tencent.com/document/product/236/36816).

