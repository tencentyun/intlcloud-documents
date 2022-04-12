### Quais são os limites nos intervalos de IP de VPCs e sub-redes?
O bloco CIDR do VPC da Tencent Cloud aceita o uso de qualquer um dos seguintes intervalos de IP privado:
- `10.0.0.0` - `10.255.255.255` (intervalo de máscara entre 16 e 28)
- `172.16.0.0` - `172.31.255.255` (intervalo de máscara entre 16 e 28)
- `192.168.0.0` - `192.168.255.255` (intervalo de máscara entre 16 e 28)

O bloco CIDR da sub-rede deve estar dentro ou ser igual ao bloco CIDR do VPC.

### É possível modificar os intervalos de IP de VPCs e sub-redes?
- Ao criar o VPC e a sub-rede, é necessário designar blocos CIDR a eles, e não é possível alterá-los depois de criados.
- Se não for possível estabelecer um Peering Connection devido à sobreposição de intervalos de IP do VPC, você pode tentar o [Cloud Connect Network](https://intl.cloud.tencent.com/product/ccn), que tem granularidade de limite menor (somente os intervalos de IP da sub-rede não podem se sobrepor) ou migrar as instâncias para outro VPC. Para mais detalhes, consulte [Alteração para VPC](https://intl.cloud.tencent.com/document/product/213/20278).

### O que deve ser feito quando um Peering Connection não é estabelecido devido a um conflito de intervalo de IP do VPC?
Ao estabelecer um Peering Connection, os blocos CIDR dos dois VPCs não podem se sobrepor, caso contrário, o Peering Connection não será estabelecido.
- Se os intervalos de IP das sub-redes de dois VPCs que precisam se comunicar não se sobrepuserem, você poderá usar o [CCN](https://intl.cloud.tencent.com/product/ccn) para estabelecer a comunicação. O CCN reduz os limites de intervalo de IP para o nível da sub-rede quando os VPCs se comunicam.
Por exemplo, se os intervalos de IP dos dois VPCs que precisam se comunicar entre si forem `10.0.0.0/16`, mas os das sub-redes forem respectivamente `10.0.1.0/24` e `10.0.2.0/24`, você pode estabelecer a comunicação usando o CCN. Consulte a [Documentação do produto CCN](https://intl.cloud.tencent.com/document/product/1003).
- Se suas necessidades não forem atendidas usando o CCN, você precisará migrar os recursos dentro das sub-redes sobrepostas.
    - Para mais detalhes sobre como alterar a sub-rede da CVM, consulte [Alterar sub-rede da instância](http://intl.cloud.tencent.com/document/product/213/16565).
    - Migre as instâncias no VPC conforme instruído em [Alteração para VPC](https://intl.cloud.tencent.com/document/product/213/20278).

### Posso modificar os IPs privados de recursos em VPCs (CVMs e bancos de dados)?
- É possível modificar o IP privado principal de um ENI principal de uma CVM, mas não o IP privado principal de um ENI secundário. Para mais detalhes, consulte [Modificação de endereços IP privados](https://intl.cloud.tencent.com/document/product/213/16561).
- Você pode modificar o IP privado de instâncias do TencentDB (como instâncias do MySQL). Consulte [Personalização de IP e porta](https://intl.cloud.tencent.com/document/product/236/31915).
- Não é possível modificar o IP privado do CLB.

### Posso migrar CVMs ou bancos de dados de um VPC para outro?
- Por enquanto, você pode migrar instâncias da CVM e do TencentDB for MySQL para outro VPC na mesma conta. Outras instâncias do TencentDB não são aceitas.
- Para migrar instâncias da CVM, consulte [Alteração para VPC](https://intl.cloud.tencent.com/document/product/213/20278).
- Para migrar instâncias do TencentDB for MySQL, consulte [Opção de rede](https://intl.cloud.tencent.com/document/product/236/31915).

### O que os EIPs fazem?
Os ElPs são aplicáveis aos seguintes cenários:
1. **Recuperação de desastres**
É altamente recomendável que você use EIPs para recuperação de desastres. Quando um dos CVMs falhar em fornecer serviços normalmente, você poderá desvincular o EIP dessa CVM e vinculá-lo a uma CVM íntegra para retomar o serviço rapidamente.
2. **Retenção de um IP público específico**
Se você precisar reter um IP público específico em sua conta, poderá convertê-lo em um EIP, que poderá ser usado para acessar redes públicas depois de ser vinculado ao dispositivo. Esse EIP será retido em sua conta até que seja “liberado” por você.
3. **Outros cenários especiais**
Quando você precisar alterar um IP em outros casos especiais, poderá converter o IP público comum em um EIP e, em seguida, vincular/desvincular o EIP. No entanto, com a disponibilidade limitada de recursos EIP, uma cota é imposta à quantidade de EIPs para cada região em uma única conta. Portanto, o planejamento e o uso razoáveis de EIPs são muito importantes.

### Como mantenho um IP público inalterado?
Se você precisar reter um IP público específico em sua conta, poderá convertê-lo em um EIP, que poderá ser usado para acessar redes públicas depois de ser vinculado ao dispositivo. Esse EIP será retido em sua conta até que seja “liberado” por você.
Para maiores instruções, consulte [Conversão de IPs públicos comuns em EIPs](https://intl.cloud.tencent.com/document/product/213/16586#convert-a-public-ip-to-an-eip).

### É possível converter um EIP novamente em um IP público?
Não é possível converter um EIP novamente em um IP público.



