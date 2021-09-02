## Visão geral
- **Réplica de dados online em tempo real**
Os snapshots são cópias totalmente utilizáveis de discos em nuvem. Quando ocorrer um problema no disco em nuvem onde foi criado um snapshot, você pode usar o snapshot para restaurar rapidamente o estado normal do disco. Antes de realizar alterações importantes em sua empresa, recomendamos que você crie um snapshot para o disco em nuvem, para que os dados possam ser rapidamente restaurados em caso de falhas.
- **Backup persistente em marcos críticos**
Os snapshots podem ser usados como backups persistentes dos dados da empresa, a fim de mantê-los nos marcos.
- **Implantação rápida na empresa**
Os snapshots permitem clonar rapidamente vários discos em nuvem para uma implementação ágil do servidor.

## Casos de uso
Os snapshots fornecem um serviço de proteção de dados prático e eficiente, que pode ser usado nas seguintes situações:
- **Backup diário de dados**
Você pode usar os snapshots para realizar backups frequentes de dados importantes da empresa, a fim de evitar a perda causada por operações incorretas, ataques e vírus.
- **Recuperação rápida de dados**
Você pode criar snapshots antes de executar operações importantes, como mudança de sistemas operacionais, atualização de aplicativos ou migração de dados da empresa. Caso aconteça algum problema, os snapshots poderão ser usados para restaurar os dados da empresa.
- **Aplicações de várias réplicas de dados de produção**
Você pode criar snapshots dos dados de produção para fornecer informações quase em tempo real para aplicações como mineração de dados, consulta de relatórios e testes de desenvolvimento.
- **Implantação rápida de ambiente**
Você pode criar snapshots de uma instância do CVM para criar uma imagem personalizada, e usar esta para criar instâncias de implantação em lote com o mesmo ambiente e menor tempo de configuração.

## Cobrança
Para obter mais informações acerca dos custos dos snapshots, consulte a [Visão geral de cobrança](https://intl.cloud.tencent.com/document/product/362/32415) e a [Visão geral de preços](https://intl.cloud.tencent.com/document/product/362/2413).

## Limites de cota
Para obter mais informações com relação aos limites de cotas dos snapshots, consulte os [Limites de uso](https://intl.cloud.tencent.com/document/product/362/32406).

## Tipos de snapshots
- **Snapshot manual**
É possível criar um snapshot manualmente de um disco em nuvem a qualquer momento. Esse snapshot pode ser utilizado para criar mais discos em nuvem com dados idênticos ou para restaurá-los no ponto exato em que o snapshot foi criado. Para obter mais informações, consulte a [Criação de snapshots](https://intl.cloud.tencent.com/document/product/362/5755).
- **Snapshot programado**
Para as empresas que se atualizam continuamente, você pode usar snapshots programados para fornecer backups contínuos de dados. Para obter backups contínuos de dados do disco em nuvem durante um período determinado, você só precisa configurar uma política de backup e associá-la aos discos, o que melhora significativamente a segurança dos dados. Para obter mais informações, consulte [Snapshots programados](https://intl.cloud.tencent.com/document/product/362/35238).

>?Durante a criação do snapshot, é possível que os dados do aplicativo salvos na memória não sejam armazenados de forma persistente. Sendo assim, os snapshots talvez não capturem os dados em nuvem mais recentes e completos. Para obter mais informações, consulte as [Observações](https://intl.cloud.tencent.com/document/product/362/5755#.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A1.B9) para garantir a consistência dos dados dos snapshots.


## Análise de caso
#### Caso 1: não foram criados snapshots manuais antes de realizar operações de alto risco, o que resultou em perda de dados
O cliente A nunca criou um snapshot para o disco em nuvem. Em maio de 2019, um operador realizou um teste de fio no disco em nuvem. O sistema de arquivos foi corrompido. Os dados foram danificados e não puderam ser recuperados.
**Análise**: se o cliente A criou um snapshot do disco antes do teste, o snapshot pode ser usado para reverter os dados e retomar o serviço imediatamente após os danos aos dados.

#### Caso 2: não foram criados snapshots programados para os discos de dados importantes, resultando em perda de dados
O cliente B criou snapshots de vários discos em nuvem, exceto os adquiridos após janeiro de 2019 por motivos de custo. Em junho de 2019, um disco sem proteção por snapshot teve uma perda de dados irrecuperável devido à uma exclusão acidental de dados de arquivos próprios do sistema.
**Análise**: se o cliente B criou snapshots programados para esse disco em nuvem, os dados podem ser recuperados a partir do exato momento que o snapshot foi criado, minimizando assim a perda. Após o incidente, o cliente B criou um snapshot para esse disco com o objetivo de melhorar a proteção de dados.

#### Caso 3: uso do snapshot programado para reverter os dados e restaurar os serviços após uma operação incorreta
O cliente C criou snapshots para todos os discos em nuvem. Em maio de 2019, ocorreu uma exceção de inicialização devido a uma operação incorreta.
**Análise**: o cliente C restaurou prontamente os dados usando o snapshot programado, que foi criado há dois dias, e a empresa permanece estável.


Todos esses casos envolvem perda de dados devido a operações incorretas, mas os resultados são diferentes. Por comparação, podemos constatar que:
- Em situações em que **um snapshot não foi criado**, os dados raramente são recuperáveis quando ocorre uma exceção de servidor ou disco na nuvem, resultando em grande perda.
- Em situações em que **um snapshot foi criado**, os dados podem ser recuperados quando ocorre uma exceção de servidor ou disco na nuvem, minimizando a perda.

Recomendamos que as empresas criem periodicamente os snapshots tomando como base o tipo de negócio, melhorando assim a segurança dos dados e conseguindo uma recuperação de desastres de baixo custo e de alta eficiência.

## Outros
Se tiver outras dúvidas, consulte as [Perguntas frequentes sobre snapshot](https://intl.cloud.tencent.com/document/product/362/17820).





