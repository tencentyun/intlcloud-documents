## Visão geral da funcionalidade
- Réplica de dados online em tempo real
Os snapshots são cópias totalmente utilizáveis de discos em nuvem. Quando ocorre um problema em um disco em nuvem para o qual um snapshot foi criado, o status antes da ocorrência do problema pode ser restaurado rapidamente usando o snapshot. Antes de realizar alterações importantes em sua empresa, recomendamos que você crie um snapshot do disco em nuvem relacionado, para que os dados possam ser restaurados rapidamente em caso de falhas.
- Backup persistente de marcos críticos
Os snapshots podem ser usados como backups persistentes dos dados da empresa para manter o status de marco dos dados dela.
- Rápida implantação de negócios
É possível usar o snapshot da sua empresa para clonar vários discos em nuvem rapidamente, obtendo uma implantação rápida de servidores.

## Cenários
Sendo um serviço de proteção de dados prático e eficiente, recomendamos os snapshots para estes cenários empresariais:
- Backup diário de dados
Você pode usar os snapshots para fazer backups frequentes de dados importantes da empresa, a fim de evitar a perda de dados causada por operações incorretas, ataques, vírus, etc.
- Restauração rápida de dados
Antes de realizar operações importantes, como alternar sistemas operacionais, atualizar aplicativos ou migrar dados da empresa, é possível criar um ou mais snapshots. Se ocorrer algum problema ao fazer essas alterações, é possível restaurar os dados da empresa usando o snapshot que você criou.
- Aplicações de várias réplicas de dados de produção
É possível fornecer dados de produção reais quase em tempo real para aplicações como mineração de dados, consulta de relatórios e testes de desenvolvimento criando snapshots de dados de produção.
- Rápida implantação de ambientes
É possível criar um snapshot de um CVM e usar esse snapshot para criar uma imagem personalizada. Você pode usar essa imagem para criar uma ou mais instâncias do CVM rapidamente, implantando vários CVMs com o mesmo ambiente em um lote para diminuir o tempo gasto em configurações duplicadas.

## Faturamento
Para obter informações detalhadas acerca do faturamento do serviço de snapshots, consulte a [Visão geral de faturamento do snapshot](https://intl.cloud.tencent.com/document/product/362/32415) e a [Visão geral do faturamento](https://intl.cloud.tencent.com/document/product/362/2413).

## Limites de cota
Para obter detalhes acerca dos limites de cotas dos snapshots, consulte os [Limites dos serviços](https://intl.cloud.tencent.com/document/product/362/5145).

## Tipos de snapshots
- Snapshot manual
É possível criar um snapshot manualmente para dados do disco em nuvem a qualquer momento. Esse snapshot pode ser utilizado para criar mais discos em nuvem com dados idênticos ou para restaurar o disco em nuvem para o status atual posteriormente. Para obter mais informações, consulte a [Criação de snapshots](https://intl.cloud.tencent.com/document/product/362/5755).
- Snapshot programado
Para empresas atualizadas continuamente, é possível usar snapshots programados para criar backups contínuos de dados. Para obter backups contínuos de dados do disco em nuvem durante um período determinado, basta configurar uma política de backup e associá-la aos discos, melhorando significativamente a segurança dos dados. Para obter mais informações, consulte [Snapshots programados](https://intl.cloud.tencent.com/document/product/362/31622).

> Durante a criação do snapshot, os dados do aplicativo salvos na memória podem não ser armazenados de forma persistente, fazendo com que os snapshots não consigam capturar os dados do disco em nuvem mais recentes e completos. Consulte as [Observações] para garantir a consistência dos dados do snapshot.


## Análise de caso
#### Caso 1: falha ao criar snapshots manualmente antes de uma operação de alto risco, causando perda de dados
**Detalhes**: o cliente A nunca criou um snapshot para o disco em nuvem. Em maio de 2019, um operador realizou um teste de fio no disco em nuvem. O sistema de arquivos foi corrompido e não foi possível recuperar os dados.
**Análise**: se o cliente A tivesse criado um snapshot para o disco em nuvem antes do teste, ele poderia ativar a reversão do snapshot após a ocorrência de danos aos dados para restaurar os negócios imediatamente.

#### Caso 2: falha ao criar snapshots programados para disco de dados importantes, causando perda de dados
**Detalhes**: o cliente B criou snapshots para vários discos em nuvem, mas não para os discos em nuvem recém-adquiridos após janeiro de 2019 devido a questões de custo. Em junho de 2019, um disco em nuvem não protegido por snapshots teve uma perda de dados irrecuperável devido a uma exclusão acidental de dados de arquivos da camada do sistema.
**Análise**: se o cliente B tivesse criado snapshots programados para esse disco em nuvem, ele poderia restaurar os dados para o status no momento anterior do snapshot, minimizando assim a perda após a exclusão acidental de dados. Após o incidente, o cliente B criou um snapshot para esse disco com o objetivo de melhorar a proteção de dados.

#### Caso 3: reversão com snapshot agendado para restaurar os negócios após uma operação incorreta
**Detalhes:** o cliente C criou snapshots para todos os discos em nuvem. Em maio de 2019, ocorreu uma exceção de inicialização devido a uma operação incorreta.
**Análise**: o cliente C restaurou prontamente os dados usando os snapshots programados tirados dois dias atrás, e a empresa não foi afetada.


Nesses casos acima, os erros operacionais levam à perda de dados. Por comparação, podemos constatar que:
- Nas situações em que **um snapshot não foi criado**, a recuperação de dados foi difícil quando ocorreu uma exceção de servidor ou disco em nuvem, resultando em grande perda.
- Na situação em que **um snapshot foi criado**, os dados puderam ser recuperados quando ocorreu uma exceção de servidor ou disco em nuvem, minimizando a perda.

Recomendamos que as empresas criem periodicamente os snapshots tomando como base o tipo de negócio, melhorando assim a segurança dos dados e conseguindo uma recuperação de desastres de baixo custo e de alta eficiência.

## Outros
Se tiver outras dúvidas, consulte as [Perguntas frequentes sobre snapshot](https://intl.cloud.tencent.com/document/product/362/17820).







