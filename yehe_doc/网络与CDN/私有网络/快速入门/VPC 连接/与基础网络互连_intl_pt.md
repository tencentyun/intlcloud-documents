Tanto a rede clássica quanto a VPC são espaços de rede na nuvem. A VPC é mais seguro e controlável. Embora a maioria das CVMs esteja implantada em VPCs da Tencent Cloud, algumas aplicações ainda estão sendo executadas na rede clássica que precisa de interconexão com a VPC. Para resolver esse problema, a Tencent Cloud fornece a seguinte solução.

## Interconexão entre a rede clássica e uma VPC
   ![](https://qcloudimg.tencent-cloud.cn/raw/736af560727e55c1f907d873f357473b.png)
+  **Classiclink**
Ele associa as CVMs baseadas na rede clássica a uma VPC especificada para permitir que essas CVMs se comuniquem com os recursos da VPC, como as instâncias da CVM e do TencentDB. No entanto, isso fornece acesso apenas entre as CVMs baseadas na VPC e as CVMs baseadas na rede clássica, em vez de outros recursos de nuvem, como o TencentDB e o CLB dentro da rede clássica.
+  **Conexão de terminal**
 Ela ajuda as instâncias em uma VPC a se comunicarem com os recursos na rede clássica (exceto as CVMs) por meio de uma rede privada. Uma conexão de terminal estabelece o mapeamento entre endereços IP de instâncias da rede clássica e endereços IP da VPC, para que as instâncias da rede clássica possam ser acessadas pelos endereços IP da VPC. Os produtos da rede clássica que aceitam as conexões de terminal incluem as instâncias do CLB, do MySQL, do Memcached, do Redis, do MariaDB, do SQL Server, do PostgreSQL, do MongoDB e do TDSQL.
>?Uma conexão de terminal não permite a comunicação entre regiões ou contas diferentes. Se você desejar estabelecer uma conexão de terminal, [envie um tíquete](https://console.cloud.tencent.com/workorder/category).


## Migração da rede clássica para uma VPC
 A VPC da Tencent Cloud é recomendada por sua segurança, flexibilidade e controlabilidade. Atualmente, a Tencent Cloud permite a migração de recursos da rede clássica para uma VPC. Para mais informações, consulte [Migração da rede clássica para a VPC](https://intl.cloud.tencent.com/document/product/215/41414).
## Referências
+ Para mais informações sobre a rede clássica e suas diferenças com relação a uma VPC, consulte [Rede clássica](https://cloud.tencent.com/document/product/215/58039).
+ Para mais informações sobre as configurações do Classiclink, consulte [Classiclink](https://intl.cloud.tencent.com/document/product/215/41418).
