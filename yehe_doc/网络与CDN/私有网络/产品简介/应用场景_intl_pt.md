## Acesso à Internet
### CVM única
Quando o tráfego para o seu negócio estiver baixo e apenas uma CVM estiver disponível, você poderá solicitar um endereço IP público e vinculá-lo à CVM para obter acesso à Internet.
![](https://main.qcloudimg.com/raw/623ba575db31584481e7b660f8b1dec0.png)

### Vários CVMs
Quando você tem vários CVMs que precisam acessar a Internet simultaneamente e não quer que os endereços de rede privada dos CVMs sejam expostos, você pode usar o [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015). O NAT Gateway fornece a funcionalidade SNAT e permite que vários CVMs acessem a Internet com endereços IP públicos no NAT Gateway. Além disso, sem a configuração da funcionalidade DNAT, os usuários externos não conseguem acessar diretamente o NAT Gateway, garantindo a segurança. Quando existem vários endereços IP públicos no NAT Gateway, ele executa automaticamente o balanceamento de carga.
![](https://main.qcloudimg.com/raw/79cf9f746c93cdce4a2e01bb6ece0297.png)

## Fornecimento de serviços à Internet
### CVM única
Você pode hospedar serviços (como serviços de site) em uma CVM baseada em VPC e usar um endereço IP público para fornecer serviços a usuários externos.
![](https://main.qcloudimg.com/raw/1e0f8b71f125b857f6d421629e90e94f.png)

### Vários CVMs
Quando você tem muitos CVMs para implantar serviços complexos e o tráfego da Internet é alto, você pode usar o [Cloud Load Balancer (CLB)](https://intl.cloud.tencent.com/document/product/214). O CLB pode distribuir automaticamente o tráfego de acesso a aplicativos entre instâncias da CVM na nuvem, aprimorando a tolerância a falhas para aplicativos.
![](https://main.qcloudimg.com/raw/d943efd83cc5d6df07e3e78954e681af.png)

## Recuperação de desastres para aplicativos
### Recuperação de desastres entre zonas de disponibilidade diferentes
Uma sub-rede é associada a uma zona de disponibilidade. Você pode criar sub-redes em zonas de disponibilidade diferentes de um VPC em uma região. Por padrão, as sub-redes diferentes do mesmo VPC se interconectam por meio da rede privada. Você pode implantar recursos em sub-redes de zonas de disponibilidade diferentes para obter recuperação de desastres entre zonas de disponibilidade.
![](https://main.qcloudimg.com/raw/32d62386d6369d631163749a0007396e.png)

### Recuperação de desastre entre regiões diferentes
Você pode implantar negócios entre regiões diferentes (por exemplo, a solução 2-regiões-3-DC) para obter recuperação de desastres entre regiões.
![](https://main.qcloudimg.com/raw/89fa56523b51e4ad09d1ae238c74b1cb.png)

## Implantação de nuvem híbrida
### Conexão a IDCs locais
O VPC fornece vários modos de conexão, como o Direct Connect e o VPN Connection, que podem conectar os IDCs locais a instâncias do VPC na nuvem para criar facilmente uma arquitetura de nuvem híbrida. O uso de IDCs locais garante a segurança de seus dados principais. Você pode expandir os recursos (como CVMs e TencentDB) na nuvem com base em seu volume de negócios para reduzir os custos de operações de TI.
![](https://main.qcloudimg.com/raw/40bd0f4a3920409a0e08c15568551a5c.png)

### Interconexão global multiponto
Quando você tem negócios implantados em várias regiões ao redor do mundo e precisa de interconexão entre regiões diferentes, você pode usar produtos como o [CCN](https://intl.cloud.tencent.com/document/product/1003) e o [Direct Connect](https://intl.cloud.tencent.com/document/product/216) para habilitar a interconexão global multiponto por meio de acesso de ponto único.
![](https://main.qcloudimg.com/raw/cdcded11e541ee50f4b050d48c251b43.png)
