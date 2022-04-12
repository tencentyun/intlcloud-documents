### Como os CVMs ou os bancos de dados se interconectam pela rede privada?
A comunicação de rede privada de CVMs ou bancos de dados em um VPC é, na verdade, a comunicação de endereços IP privados no nível da rede e, portanto, não há diferença entre eles. Os métodos de comunicação em diferentes cenários de endereço IP privado são os seguintes:

| Cenário de comunicação | Método de comunicação |
|---------------|------------|
| Regiões diferentes | Os CVMs ou bancos de dados em regiões diferentes pertencem a instâncias do VPC diferentes e se comunicam por meio de [Peering Connections](https://intl.cloud.tencent.com/document/product/553/18836) ou do [CCN](https://intl.cloud.tencent.com/document/product/1003/31985). (Tanto a comunicação da mesma conta quanto a comunicação entre contas diferentes são aceitas.) |
| Zonas de disponibilidade diferentes | Mesmo VPC: permite a interconexão por padrão.<br>Instâncias do VPC diferentes: comunicam-se por meio de [Peering Connections](https://intl.cloud.tencent.com/document/product/553/18836) ou do [CCN](https://intl.cloud.tencent.com/document/product/1003/31985). (Tanto a comunicação da mesma conta quanto a comunicação entre contas diferentes são aceitas.) |
| Instâncias do VPC diferentes | Comunicam-se por meio de [Peering Connections](https://intl.cloud.tencent.com/document/product/553/18836) ou do [CCN](https://intl.cloud.tencent.com/document/product/1003/31985). (Tanto a comunicação da mesma conta quanto a comunicação entre contas diferentes são aceitas.) |
| Sub-redes diferentes | Mesmo VPC: permite a interconexão por padrão.<br>VPCs diferentes: comunicam-se por meio de [Peering Connections](https://intl.cloud.tencent.com/document/product/553/18836) ou do [CCN](https://intl.cloud.tencent.com/document/product/1003/31985). (Tanto a comunicação da mesma conta quanto a comunicação entre contas diferentes são aceitas.) |
| Entre contas diferentes | A comunicação entre contas diferentes é feita por meio de [Peering Connections](https://intl.cloud.tencent.com/document/product/553/18836) ou do [CCN](https://intl.cloud.tencent.com/document/product/1003/31985). (Tanto a comunicação da mesma região quanto a comunicação entre regiões diferentes são aceitas.) |
 
>!
>- Para a interconexão de VPC entre contas diferentes por meio de Peering Connection ou do CCN, atenção ao seguinte: 
    - A conta raiz possui os recursos. Se você quiser se comunicar com outra conta por meio de Peering Connection ou do CCN, insira a conta raiz. 
    - A subconta só tem permissão de operação por padrão. Solicite a permissão da conta raiz para estabelecer o Peering Connection ou CCN, se necessário.
>- A **interconexão padrão de rede privada** está presente entre sub-redes diferentes do mesmo VPC (estejam ou não na mesma zona de disponibilidade). Se elas não puderem se conectar umas com as outras, primeiro você pode solucionar os problemas das políticas de firewall do [grupo de segurança](https://intl.cloud.tencent.com/document/product/213/12452) e da [ACL de rede](https://intl.cloud.tencent.com/document/product/215/5132).


### O que devo fazer quando um Peering Connection não é estabelecido devido a um conflito de intervalo de IP do VPC?
Quando você tenta estabelecer um Peering Connection, os blocos CIDR das duas instâncias do VPC não podem se sobrepor, caso contrário, o Peering Connection não pode ser estabelecido.

- Se os intervalos de IP de ambas as instâncias do VPC que precisam se intercomunicar se sobrepuserem, mas os intervalos de IP da sub-rede não se sobrepuserem, você poderá tentar estabelecer a comunicação por meio do [CCN](https://intl.cloud.tencent.com/product/ccn). O CCN pode reduzir os limites do intervalo de endereços IP para o nível da sub-rede quando as instâncias do VPC se comunicam.
Por exemplo, os intervalos de IP das duas instâncias do VPC que precisam se comunicar entre si são `10.0.0.0/16`, mas os das sub-redes são `10.0.1.0/24` e `10.0.2.0/24`, respectivamente. Nesse caso, você pode estabelecer a comunicação por meio do CCN. Para mais informações, consulte [CCN](https://intl.cloud.tencent.com/document/product/1003).
- Se suas necessidades não forem atendidas usando o CCN, você precisará migrar os recursos dentro das sub-redes sobrepostas.
    - Para mais detalhes sobre como alterar as sub-redes de CVMs, consulte [Alterar sub-rede da instância](https://intl.cloud.tencent.com/document/product/213/16565).
    - Para mais detalhes sobre a migração entre VPCs, consulte [Alteração para VPC](https://intl.cloud.tencent.com/document/product/213/20278).

### Se o VPC1 estabelece Peering Connections separadamente com o VPC2 e o VPC3, o VPC2 e o VPC3 podem se comunicar entre si?
Não. Duas instâncias do VPC podem estabelecer interconexão por meio de um Peering Connection, mas essa relação de interconexão não é transitiva. Isso significa que quando um Peering Connection é estabelecido entre o VPC1 e o VPC2 enquanto outro Peering Connection é estabelecido entre o VPC1 e o VPC3, a interconexão de tráfego fica indisponível entre o VPC2 e o VPC3 porque o Peering Connection não é transitivo.

