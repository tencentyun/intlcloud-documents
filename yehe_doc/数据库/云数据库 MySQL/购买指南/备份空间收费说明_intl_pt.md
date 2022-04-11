## Visão geral
O espaço de backup é usado para armazenar os backups de todas as instâncias do TencentDB for MySQL em uma região. Esses backups podem ser automáticos, manuais e de logs.

O TencentDB for MySQL fornece uma determinada quantidade de capacidade de backup gratuita com base na região. A capacidade é equivalente à soma da capacidade de armazenamento de todas as instâncias de dois e três nós (incluindo as instâncias de recuperação de desastres e de origem) na região. Para conferir exemplos de cálculo, consulte [Fórmula de cálculo](#jfgs).
>?
>- O espaço de backup gratuito será fornecido ao adquirir uma instância de recuperação de desastres e de origem, mas não estará disponível para a instância somente leitura.
>- A capacidade de backup pode ser exibida na página de backup do banco de dados no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/mysql/backup/index).

## Preços de backup
O uso da capacidade de backup que exceder o nível gratuito será cobrado em 0,000127 USD/GB/hora na China Continental. Para conferir os preços de regiões fora da China Continental, consulte [Calculadora de preços do TencentDB for MySQL](https://buy.intl.cloud.tencent.com/price/cdb/calculator).
Se a capacidade excessiva de backup for inferior a 1 GB, nenhuma taxa será cobrada. Se o período for inferior a 1 hora, ele será calculado como 1 hora. O TencentDB for MySQL adota uma política de distribuição flexível, para que, no geral, você não precise pagar pela capacidade de backup da maioria das instâncias.

## Agendamento de faturamento da capacidade de backup
- Oficialmente, o faturamento começou a partir das 0h de 2 de dezembro de 2019 para Hong Kong (China), Macau (China), Taiwan (China) e outras regiões fora da China Continental.
- Oficialmente, o faturamento começou a partir das 0h de 2 de dezembro de 2019 para o Sudoeste da China (regiões de Chengdu e Chongqing).
- Oficialmente, o faturamento começou a partir das 0h de 5 de dezembro de 2019 para o Sul da China (região de Guangzhou).
- Oficialmente, o faturamento começou a partir das 0h de 9 de dezembro de 2019 para o Norte da China (região de Pequim).
- Oficialmente, o faturamento começou a partir das 0h de 10 de dezembro de 2019 para o Leste da China (região de Xangai).
- Por padrão, o faturamento é iniciado para as regiões adicionadas após as 0h de 10 de dezembro de 2019.


## [Fórmula de cálculo](id:jfgs)
**Capacidade de backup gratuita em uma região = Soma da capacidade de armazenamento de todas as instâncias de dois e três nós do TencentDB for MySQL nessa região**

**Capacidade de backup paga em uma região = Volume de backup de dados + volume de backup de logs - capacidade de backup gratuita (todos os valores são para essa região)**

>?Os backups de instâncias do TencentDB for MySQL na lixeira também serão contabilizados na capacidade total de backup.

**Exemplo de cálculo**
Se você tiver uma instância de dois nós do TencentDB for MySQL em execução com capacidade de armazenamento de banco de dados adquirida de 500 GB/mês na Zona 3 de Guangzhou e outra instância desse tipo com capacidade de armazenamento de banco de dados adquirida de 200 GB/mês na Zona 4 de Guangzhou, você vai obter uma capacidade de backup gratuita de 700 GB/mês na região de Guangzhou.

O uso da capacidade de backup que exceder o nível gratuito será calculado por hora de acordo com a regra a seguir. Por exemplo, se os backups de dados atingirem 800 GB e os backups de logs atingirem 100 GB, o uso total da capacidade de backup em Guangzhou excederá 700 GB, e sua capacidade de backup faturável por hora será de 200 GB (800 + 100 - 700 = 200).


## Ciclo de vida de backup
### [Instância com pagamento conforme o uso](id:anliang_zhouqi)
- Os backups estão sujeitos a alterações ao longo do ciclo de vida da instância.
- Os backups podem funcionar normalmente dentro de 24 horas após o vencimento do pagamento da instância.
- Após 24 horas do vencimento do pagamento da instância, ela será isolada na lixeira. Nesse momento, o backup automático será interrompido e a reversão e o backup manual serão proibidos, mas os backups ainda poderão ser baixados na [Lista de backup](https://console.cloud.tencent.com/mysql/backup/list/data). A capacidade excessiva de backup continuará a ser faturada até que a instância seja eliminada. Você poderá renovar a instância na lixeira no console para recuperá-la.
- Após três dias do isolamento da instância na lixeira, a instância será eliminada (ou seja, excluída completamente) junto com todos os backups de dados. Salve os backups necessários em tempo hábil.

## Pagamento em atraso
### Instância com pagamento conforme o uso
Assim que a conta estiver em atraso, o backup será alterado com o ciclo de vida da instância. Para mais informações, consulte o ciclo de vida de backup de instâncias com pagamento conforme o uso, conforme descrito acima.

## Serviços com upgrade disponíveis após o início do faturamento de backup
>? Os valores indicados na tabela abaixo são os valores máximos permitidos na mesma região em uma única conta da Tencent Cloud.

| Melhoramento | Antes do upgrade | Depois do upgrade |
| ------------------ | -------------- | --------------- |
| Período de retenção de backup de dados | 30 dias | 1.830 dias |
| Período de retenção de backup de logs | 5 dias | 1.830 dias |
| Taxa de compactação de backup | Geral | Ultra-alta |
| Centralização de binlog | Armazenamento local | Armazenamento centralizado |

## Sugestões para reduzir os custos de backup
- Exclua os backups manuais que não são mais necessários. Você pode fazer login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), clicar em um ID de instância ou **Manage (Gerenciar)** na coluna **Operation (Operação)**, para acessar a página de gerenciamento de instâncias e excluir backups manuais na aba **Backup and Restoration (Backup e restauração)**. Os backups automáticos não podem ser excluídos manualmente no console. Em vez disso, eles serão excluídos automaticamente depois que expirarem.
- Reduza a frequência de backup automático de dados para negócios não essenciais (você pode ajustar o ciclo e o período de retenção de backup no console, e a frequência deve ser pelo menos duas vezes por semana).
>?A [funcionalidade de reversão](https://intl.cloud.tencent.com/document/product/236/7276) depende do ciclo de backup e dos dias de retenção de backups de dados e de logs (binlog). A reversão será afetada se você reduzir a frequência e o período de retenção de backup automático. Selecione os parâmetros conforme necessário.
>
- Reduza o período de retenção backups de dados e de logs para negócios não essenciais (um período de retenção de 7 dias pode atender aos requisitos da maioria dos cenários).

| Cenário de negócios             | Período de retenção de backup recomendado                                                 |
| -------------------- | ------------------------------------------------------------ |
| Negócios essenciais             | 7 a 1.830 dias                                              |
| Negócios não essenciais e não relacionados a dados | 7 dias                                                      |
| Negócios arquivados             | 7 dias. Recomendamos que você faça o backup manual dos dados com base em suas necessidades de negócios e exclua os backups imediatamente após o uso |
| Negócios de testes | 7 dias. Recomendamos que você faça o backup manual dos dados com base em suas necessidades reais de negócios e exclua os backups imediatamente após o uso |

