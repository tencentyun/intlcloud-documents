## Pré-requisitos
Primeiro, é necessário verificar a sua identidade. Para mais informações, consulte [Guia de verificação de identidade](https://intl.cloud.tencent.com/document/product/378/3629).

## Aquisição de instâncias no console
1. Faça login na [página de aquisição do TencentDB for MySQL](https://buy.Intl.cloud.tencent.com/cdb), configure as seguintes informações da instância e clique em **Buy Now (Comprar agora)**.
 - **Billing Mode (Modo de faturamento)**: pagamento conforme o uso
    - Se o volume de solicitações do seu negócio flutuar muito e de forma instantânea, recomendamos que você escolha o faturamento com pagamento conforme o uso.
 - **Region (Região)**: selecione a região na qual você deseja que sua instância do TencentDB for MySQL seja implantada. Recomendamos que você use a mesma região que a instância da CVM à qual ela será conectada. Os produtos da Tencent Cloud em regiões diferentes não podem se comunicar entre si pela rede privada. Não é possível modificar a região após a aquisição.
 - **Database Version (Versão do banco de dados)**: atualmente, o TencentDB for MySQL aceita o MySQL 8.0, 5.7, 5.6 e 5.5. Para mais informações sobre as funcionalidades de cada versão, consulte a [documentação oficial](https://dev.mysql.com/doc/refman/5.7/en/).
  - **Architecture (Arquitetura)**: nó único, dois nós ou três nós. Para mais informações, consulte [Arquitetura de bancos de dados](https://intl.cloud.tencent.com/document/product/236/38328).
  - **Data Replication Mode (Modo de replicação de dados)**: são fornecidos os modos de replicação assíncrona, semissincronizada e de sincronização forte. Para mais informações, consulte [Replicação de instância de banco de dados](https://intl.cloud.tencent.com/document/product/236/7913).
 - **Source AZ (AZ de origem)** e **Replica AZ (AZ de réplica)**: selecione AZs de origem e réplica diferentes (ou seja, [implantação Multi-AZ](https://intl.cloud.tencent.com/document/product/236/8459)) para proteger seu banco de dados contra falhas e interrupções de AZ.
>?
>- Se os nós de origem e de réplica estiverem em AZs diferentes, pode haver um atraso de sincronização de rede adicional de 2 a 3 ms.
>- Ao adquirir os serviços da Tencent Cloud, recomendamos que selecione a região mais próxima de você para minimizar a latência de acesso e melhorar a velocidade de download.
 - **Instance Type (Tipo de instância)**: geral ou dedicada. Para mais informações, consulte [Política de isolamento de recursos](https://intl.cloud.tencent.com/document/product/236/39794).
 - **Instance Specification (Especificação da instância)**: selecione as especificações conforme necessário.
 - **Hard Disk (Disco rígido)**: o espaço em disco é usado para armazenar os arquivos necessários para a execução do MySQL.
 - **Network (Rede)**: selecione a rede onde a instância do TencentDB for MySQL está localizada, que é “Default-VPC (default) (VPC padrão (padrão))” por padrão. Recomendamos que você selecione a mesma VPC na mesma região da instância da CVM a ser conectada. Caso contrário, a instância do MySQL não poderá ser conectada à instância da CVM pela rede privada.
 - **Security Group (Grupo de segurança)**: para mais informações sobre a criação e o gerenciamento de grupos de segurança, consulte [Gerenciamento de grupos de segurança do TencentDB](https://intl.cloud.tencent.com/document/product/236/14470).
>?A porta 3306 deve ser aberta para a instância do MySQL por meio da regra de entrada do grupo de segurança. A instância do MySQL usa a porta de rede privada 3306 por padrão e aceita uma porta personalizada. Se a porta padrão for alterada, a nova porta deverá ser aberta no grupo de segurança.
 - **Parameter Template (Modelo de parâmetros)**: além do modelo de parâmetros do sistema fornecido pelo TencentDB, você pode criar um modelo de parâmetros personalizado. Para mais informações, consulte [Gerenciamento de modelos de parâmetros](https://intl.cloud.tencent.com/document/product/236/31906).
 - **Alarm Policy (Política de alarme)**: você pode criar uma política de alarme para acionar alarmes e enviar mensagens quando o estado do recurso da Tencent Cloud mudar. Para mais informações, consulte [Políticas de alarme (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457).
 - **Project (Projeto)**: selecione um projeto ao qual a instância do TencentDB pertence. O projeto padrão é usado.
 - **Tag**: categorize e gerencie os recursos com tags. Para mais informações, consulte [Tag > Visão geral](https://intl.cloud.tencent.com/document/product/236/31917).
 - **Instance Name (Nome da instância)**: nomeie a instância agora ou posteriormente.
 - **Quantity (Quantidade)**: você pode adquirir até 10 instâncias com pagamento conforme o uso em cada AZ.
 - **Terms of Service (Termos de serviço)**: para mais informações, consulte [Termos de serviço](https://intl.cloud.tencent.com/document/product/236/35543).
2. Você retornará à lista de instâncias após adquirir a instância. A instância estará com o status **Delivering (Em entrega)**. Será possível inicializar a instância após cerca de 3 a 5 minutos quando seu status mudar para **Uninitialized (Não inicializada)**.

## Aquisição de instâncias por meio de uma API
Para mais informações sobre como adquirir uma instância do TencentDB por meio de uma API, consulte [CreateDBInstanceHour](https://intl.cloud.tencent.com/document/product/236/15865).

## Operações subsequentes
- [Inicialização de instância do MySQL](https://intl.cloud.tencent.com/document/product/236/3128)
- [Conexão à instância do MySQL](https://intl.cloud.tencent.com/document/product/236/37788)

