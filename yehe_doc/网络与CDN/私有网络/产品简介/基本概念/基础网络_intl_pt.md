A rede clássica é um pool de recursos de rede pública para todos os usuários da Tencent Cloud. Os IPs privados de todos os CVMs são atribuídos pela Tencent Cloud. Não é possível personalizar os intervalos de IP ou os endereços de IP. Os VPC com acesso independente, controlável e mais seguro são evoluídos da rede clássica para atender aos requisitos de uma quantidade crescente de usuários por serviços mais complexos.
>?À medida que os recursos da rede clássica se tornam cada vez mais escassos e não podem ser expandidos, as contas da Tencent Cloud criadas após 13 de junho de 2017, 00:00:00, só podem criar instâncias (incluindo CVM e CLB) em um VPC em vez da rede clássica. Se você precisar usar o serviço da rede clássica, envie uma solicitação.


## Limites de uso
+ Os CVMs baseados na rede clássica não aceitam ENIs.
+ A migração da rede clássica para o VPC é irreversível.

## Rede clássica vs. VPC
Tanto a rede clássica quanto o VPC são espaços de rede na nuvem.  
+ A rede clássica é um pool de recursos de rede pública para todos os usuários da Tencent Cloud (como mostrado no lado direito da figura abaixo). Os IPs privados de todos os CVMs são atribuídos pela Tencent Cloud. Não é possível personalizar os intervalos de IP ou os endereços IP.
+ Por outro lado, o VPC é um espaço de rede logicamente isolado na Tencent Cloud (como mostrado no lado esquerdo da figura abaixo). Em um VPC, é possível personalizar os intervalos de IP, os endereços IP e as políticas de roteamento. O VPC é mais adequado para os casos de uso que exigem configurações personalizadas.
![](https://main.qcloudimg.com/raw/5fe7730ac2f302d960cf20443f976b6f.png)

>?Você pode usar a API [`DescribeAccountAttributes`](https://intl.cloud.tencent.com/document/product/215/17875) para consultar os atributos de rede de uma conta. Se o valor de `supportedPlatforms` for `only-vpc`, a conta é um usuário de VPC padrão, que possui todos os recursos de nuvem em VPCs. Se o valor de `supportedPlatforms` for `classic`, a conta é um usuário da rede clássica padrão, que possui todos os recursos de nuvem na rede clássica.

## Referência
+ Para mais informações sobre o plano de comunicação entre um VPC e a rede clássica, consulte [Comunicação com a rede clássica](https://intl.cloud.tencent.com/document/product/215/35505).
+ Para mais informações sobre as configurações do Classiclink, consulte [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807).
+ Você pode migrar as instâncias da rede clássica para um VPC. Para maiores instruções detalhadas, consulte [Migração da rede clássica para o VPC](https://intl.cloud.tencent.com/document/product/215/41414).

