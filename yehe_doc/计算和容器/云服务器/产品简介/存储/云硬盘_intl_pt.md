O Tencent Cloud Block Storage (CBS) fornece um serviço de armazenamento permanente em bloco para instâncias do CVM.

- O CBS armazena os dados automaticamente em várias cópias redundantes em uma zona de disponibilidade, a fim de eliminar o risco de pontos únicos de falha de dados, fornecendo até 99,9999999% de confiabilidade de dados.
- O CBS oferece discos em nuvem de vários tipos e especificações para garantir um desempenho de armazenamento estável e de baixa latência.
- O CBS provê suporte à montagem e desmontagem de instâncias na mesma zona de disponibilidade. Você pode usá-lo para ajustar a capacidade de armazenamento em minutos, para satisfazer as demandas elásticas e pagar apenas pelo que usar.


## Casos de uso comuns
- Quando o espaço em disco se torna insuficiente durante o uso, você pode adquirir um ou mais discos em nuvem para atender aos requisitos de capacidade de armazenamento.
- Adquira discos em nuvem para atender às demandas de armazenamento não planejadas ao comprar a instância do CVM.
- Armazene dados em um disco em nuvem, desmonte-o e monte-o em outra instância do CVM para transferir os dados.
- Use vários discos em nuvem para formar um Gerenciamento de volume lógico (LVM, na sigla em inglês), a fim de ultrapassar o limite físico de um único disco em nuvem.
- Use vários discos em nuvem para formar uma configuração RAID e melhorar o desempenho de E/S de um disco em nuvem único.


## Ciclo de vida
O ciclo de vida de um disco em nuvem elástico é independente das instâncias do CVM. Você pode montar vários discos em nuvem em uma instância do CVM e desmontá-los para poder montá-los em outra instância do CVM.

### Aquisição e uso
- Para obter informações sobre os tipos de disco em nuvem, consulte os [Tipos de disco em nuvem](https://intl.cloud.tencent.com/document/product/362/31636).
- Para obter informações sobre como adquirir discos em nuvem, consulte a [Visão geral de preços do CBS](https://intl.cloud.tencent.com/document/product/362/2413)
- Para obter informações sobre a instância do CVM e as especificações de disco em nuvem, consulte a [Criação de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/5744) e a [Documentação do CBS](https://intl.cloud.tencent.com/document/product/362/5745).
- Para obter informações sobre as práticas recomendadas de disco em nuvem para expansão de capacidade, desmontagem, encerramento e outras operações, consulte a [Documentação do CBS](https://intl.cloud.tencent.com/document/product/362).
