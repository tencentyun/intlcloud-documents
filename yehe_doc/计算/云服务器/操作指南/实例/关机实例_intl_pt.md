## Cenário
A instância pode ser desligada quando você precisar interromper o serviço ou modificar as configurações que podem ser feitas apenas no estado desligado. Desligar uma instância é como desligar um computador local.

## Observações

- Você pode desligar uma instância usando comandos do sistema (como o comando desligar no sistema Windows e no sistema Linux) ou pelo console do Tencent Cloud. Recomendamos que você visualize o processo de desligamento no console para verificar se ocorre algum problema.
- A instância não fornecerá mais serviços após o desligamento. Antes do desligamento, certifique-se de que o CVM parou de receber solicitações de serviço.
- Durante o desligamento, o status da instância mudará de "shutting down (desligando)" para "shutdown (desligada)". Se o processo de desligamento demorar muito, pode haver uma exceção. Para obter mais informações, consulte [Fechar um CVM](https://intl.cloud.tencent.com/document/product/213/2917) para evitar o desligamento forçado.
- Depois que uma instância é desligada, todo o armazenamento que ainda estiver conectado à instância e todos os dados do disco são retidos. Os dados na memória serão perdidos.
- O desligamento de uma instância não altera seus atributos físicos. Os IPs públicos e privados da instância permanecem inalterados. O [IP público elástico](https://intl.cloud.tencent.com/document/product/213/5733) permanece vinculado à instância. No entanto, devido à interrupção do serviço, você receberá uma resposta de erro ao acessar esses IPs. A relação [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807) permanece inalterada.
- Se a instância pertencer ao [cluster do servidor real](https://intl.cloud.tencent.com/document/product/214/32388) da instância do CLB, ela não poderá mais fornecer serviços após o desligamento.
Se a política de verificação de integridade tiver sido configurada, a instância que foi desligada será automaticamente bloqueada e as solicitações não serão mais encaminhadas para ela. Caso contrário, o cliente pode receber um código de erro 502. Para obter mais informações, consulte [Verificação de integridade](https://intl.cloud.tencent.com/document/product/214/38451).
- Se a instância que foi desligada estiver em um [grupo do Auto Scaling](https://intl.cloud.tencent.com/document/product/377/3590), o serviço do Auto Scaling marcará a instância como tendo baixo desempenho e pode substituí-la e removê-la do grupo do Auto Scaling. Para obter mais informações, consulte [Auto Scaling](https://intl.cloud.tencent.com/document/product/377).

## Direções
### Desligar uma instância pelo console
 1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
 2. Escolha métodos diferentes com base nas necessidades reais.
  - Desligar uma instância: selecione a instância a ser desligada e clique em **More (Mais)** > **Instance Status (Status da instância)** > **Shutdown (Desligar)** na coluna de operação no lado direito.
  - Desligar várias instâncias: selecione todas as instâncias a serem desligadas e clique em **Shutdown (Desligar)** no topo da lista para desligar as instâncias em lotes.
  Os motivos são fornecidos para as instâncias que não podem ser desligadas.

### Desligar uma instância por API
Para obter mais informações, consulte a API [StopInstances](https://intl.cloud.tencent.com/document/product/213/33235).

## Operações subsequentes
Você pode modificar os seguintes atributos apenas se a instância estiver sido desligada.
- **Configuração da instância (CPU, memória):** para alterar o tipo de instância, consulte [Alterar configuração da instância](https://intl.cloud.tencent.com/document/product/213/2178).
- **Alterar senha:** consulte [Senha de login](https://intl.cloud.tencent.com/document/product/213/6093).
- **Carregar chave SSH:** consulte [Chave SSH](https://intl.cloud.tencent.com/document/product/213/6092).
