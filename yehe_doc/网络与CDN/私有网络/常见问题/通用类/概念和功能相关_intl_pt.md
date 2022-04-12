### Como estabelecer a comunicação entre sub-redes diferentes de um VPC?
- Cada VPC tem interconexões de rede privada por padrão, e você pode observar uma rota padrão na tabela de rotas correspondente. Essa rota indica que todos os recursos nesse VPC podem se conectar entre si pela rede privada.
- As sub-redes em VPCs diferentes não podem se interconectar pela rede privada e podem se comunicar entre si apenas usando [Peering Connections](https://intl.cloud.tencent.com/document/product/553) ou o [CCN](https://intl.cloud.tencent.com/document/product/1003).

### É possível implantar CVMs diferentes em zonas de disponibilidade diferentes no mesmo VPC?
Sim. Um VPC tem um atributo de região (como Guangzhou, Pequim ou Seul), e as sub-redes no VPC têm um atributo de zona de disponibilidade (como Zona 1 de Guangzhou ou Zona 2 de Guangzhou); portanto, as sub-redes no mesmo VPC podem ser implantadas em zonas de disponibilidade diferentes na mesma região. O atributo de zona de disponibilidade de uma CVM herda o atributo da sub-rede à qual pertence, e as CVMs são adquiridas em sub-redes em zonas de disponibilidade. Portanto, é possível que CVMs diferentes sejam implantados em zonas de disponibilidade diferentes.

### Como estabelecer a comunicação entre CVMs e bancos de dados em zonas de disponibilidade diferentes?
- Mesmo VPC: há interconexão por padrão. Se eles não se conectarem, você pode dar prioridade à solução de problemas das políticas de firewall do [grupo de segurança](https://intl.cloud.tencent.com/document/product/215/38750) e da [ACL de rede](https://intl.cloud.tencent.com/document/product/215/31850).
- VPCs diferentes: você pode usar [Peering Connections](https://intl.cloud.tencent.com/document/product/553) ou o [CCN](https://intl.cloud.tencent.com/document/product/1003) para implementar a interconexão pela rede privada entre dois VPCs.

### Quantos endereços IP privados cada VPC pode fornecer para instâncias de serviço da Tencent Cloud?
Cada VPC pode fornecer até 65.533 endereços IP privados para instâncias de serviço da Tencent Cloud.

### O que é o CIDR?
O roteamento entre domínios sem classe (CIDR, na sigla em inglês) implementa a divisão geral da rede usando o bloco de endereços de espaço de rede independente designado por você junto com o IP e a máscara. Ele elimina os conceitos tradicionais de intervalos de endereços e sub-redes de classe A, classe B e classe C, e aloca o espaço de endereço IP com mais eficiência. Ao criar um VPC e uma sub-rede, você precisa criar o intervalo de IP correspondente na forma de bloco CIDR. Por exemplo, para criar um intervalo de IP de `10.0.16.0 - 10.0.17.255`:
converta `10.0.16.0 - 10.0.17.255` para o formato binário `00001010.00000000.00010000.00000000 - 00001010.00000000.00010001.11111111`, com os primeiros 23 bits sendo os mesmos. O formato do bloco CIDR após a conversão é `10.0.16.0/23`.


### Por que não consigo excluir o VPC e a sub-rede depois de encerrar manualmente uma instância do TencentDB for Redis?
Se houver apenas uma instância do TencentDB for Redis no VPC, depois que a instância for encerrada manualmente, ela será movida para a lixeira do TencentDB. No momento, os recursos do Redis ainda não foram liberados, portanto, o VPC não pode ser excluído imediatamente. Você pode resolver esse problema das seguintes maneiras:
+ Na lixeira do TencentDB, **eliminate (elimine)** a instância do TencentDB for Redis e, depois, exclua o VPC e a sub-rede.
+ Aguarde a instância do TencentDB for Redis expirar automaticamente na lixeira do TencentDB e, depois, exclua o VPC e a sub-rede.
Para mais informações, consulte [Encerramento de instâncias](https://intl.cloud.tencent.com/document/product/239/31937).


### Por que uma solicitação de EIP falha?
Quando a cota de EIP for excedida, a solicitação de EIP falhará. Para mais informações sobre como exibir os detalhes da cota, consulte [Limites de cota de EIP](https://intl.cloud.tencent.com/document/product/213/5733).
