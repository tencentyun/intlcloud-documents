A implantação Multi-AZ protege o seu banco de dados de ser afetado por falhas de instância de banco de dados e interrupções de AZ. Para mais informações, consulte [Regiões e AZs](https://intl.cloud.tencent.com/document/product/236/8458).
O esquema de implantação Multi-AZ do TencentDB for MySQL garante a alta disponibilidade e capacidade de failover de instâncias de banco de dados, combinando várias AZs em uma única “Multi-AZ”.

>?
>- Independentemente se as instâncias do TencentDB for MySQL em um cluster de banco de dados estão sendo executadas em várias AZs ou não, cada instância tem uma subordinada para backup dinâmico em tempo real, a fim de garantir a alta disponibilidade do banco de dados.
>- Com a implantação Multi-AZ, o TencentDB for MySQL predefine e mantém automaticamente uma réplica da subordinada de sincronização em uma AZ diferente.
>- A instância do banco de dados mestre é replicada de forma síncrona para a réplica subordinada entre AZs diferentes, a fim de fornecer redundância de dados, eliminar congelamentos de E/S e minimizar a latência durante os backups do sistema.

### Regiões com suporte
Atualmente, o esquema de implantação Multi-AZ do TencentDB for MySQL está disponível nas regiões de Guangzhou, Xangai, Pequim, Chengdu e Virgínia.

### Implantação Multi-AZ
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb/) e clique em **Create (Criar)** na Lista de instâncias para acessar a página de aquisição.
2. Na página de aquisição do TencentDB for MySQL, selecione uma região com suporte, e selecione a AZ subordinada desejada na opção **Slave AZ (AZ subordinada)**.
>?Apenas algumas AZs podem ser selecionadas como uma AZ subordinada. Para mais informações, consulte a página de aquisição.
>
![](https://main.qcloudimg.com/raw/aec9d1b540ceff3426968c213cfe9435.png)
3. Após confirmar que tudo está correto, clique em **Buy Now (Comprar agora)**. Após a realização do pagamento, você pode retornar à lista de instâncias para exibir a instância Multi-AZ recém-adquirida.

### Failover
O TencentDB for MySQL processa o failover automaticamente, para que as operações do banco de dados possam ser retomadas o mais rápido possível, sem necessidade de intervenção administrativa. A instância do banco de dados mestre será alternada automaticamente para a réplica subordinada na AZ subordinada nas seguintes condições:
- Interrupção de AZ.
- Falha na instância do banco de dados mestre.
