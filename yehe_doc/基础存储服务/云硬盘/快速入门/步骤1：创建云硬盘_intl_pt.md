Este documento usa a criação de um disco em nuvem vazio `cbs-test` na região de Pequim como exemplo para ajudar você a iniciar o uso.

## Pré-requisitos
- Antes de criar um disco em nuvem, você precisa [se registrar no Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985) e concluir [a verificação de identidade](https://intl.cloud.tencent.com/document/product/378/3629).
- Você precisa ter um CVM disponível na região e na zona de disponibilidade (neste exemplo, Zona 1 de Pequim), na qual o disco em nuvem deverá ser criado. Para informações sobre a aquisição e a execução do CVM, consulte [Criação de instâncias](https://intl.cloud.tencent.com/document/product/213/4855).

## Orientações
>Neste exemplo, um disco em nuvem premium elástico é adquirido por meio do console. Para obter mais informações sobre como criar um disco em nuvem, consulte [Criação de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/5744).

1. Faça login no [Console do CBS](https://console.cloud.tencent.com/cvm/cbs).
2. Selecione **Beijing (Pequim)** e clique em **Create (Criar)**.
3. Configure os seguintes parâmetros:
 - Availability Zone (Zona de disponibilidade): selecione **Beijing Zone 1 (Zona 1 de Pequim)**
 - Cloud Disk Type (Tipo de disco em nuvem): selecione **Premium Cloud Storage (Armazenamento em nuvem premium)**.
 - Capacity (Capacidade): 20 GB.
 - Disk Name (Nome do disco): insira `cbs-test`.
 - Billing Mode (Modo de faturamento): selecione **Pay-as-you-go (Pagamento conforme o uso)**.
 - Period (Período): selecione **1 month (1 mês)**.
4. Clique em **OK**.
5. Após confirmar as configurações, clique em **Confirm (Confirmar)** e efetue o pagamento.
Volte à página de lista do Cloud Block Storage. Agora é exibido o disco em nuvem elástico adquirido `cbs-test`, cujo status é **To be mounted (A ser montado)**.

## Operações subsequentes
Após a criação do disco em nuvem, você precisa montá-lo em um CVM na mesma zona de disponibilidade para usá-lo como disco de dados. Para obter informações sobre essa operação, consulte [Montagem de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/31645).
