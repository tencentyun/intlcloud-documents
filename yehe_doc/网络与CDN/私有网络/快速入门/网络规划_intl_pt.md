Antes de iniciar a expansão da rede e a criação do seu VPC, é necessário planejar a quantidade e os intervalos de IP do VPC de acordo com suas necessidades de negócios.
- [Como planejar a quantidade de VPCs?](#planVPC)
- [Como planejar a quantidade de sub-redes?](#planSubnet)
- [Como planejar os intervalos de IP (blocos CIDR) de VPCs e sub-redes?](#planCIDR)
- [Como planejar a quantidade de tabelas de rotas?](#planRoute)
- [Como planejar uma rede de nuvem híbrida multicêntrica entre regiões?](#planExample)

<span id="planVPC"  ></span>
## Como planejar a quantidade de VPCs?

- **Planejamento de um VPC**
Se você tiver um negócio de pequeno porte implantado na mesma região sem a necessidade de isolamento de rede, recomendamos que você planeje um VPC.
É possível criar várias sub-redes e tabelas de rotas em um único VPC para gerenciamento de tráfego detalhado. Além disso, recomendamos que você implante sub-redes em zonas de disponibilidade diferentes para a recuperação de desastre delas.
![](https://main.qcloudimg.com/raw/22c3ea70430c6eaf50c994f5cb5923bc.png)
- **Planejamento de vários VPCs**
Recomendamos que você planeje vários VPCs em qualquer um dos seguintes cenários:
 - **Seu negócio está implantado em várias regiões**
Se seu negócio estiver implantado em várias regiões, será necessário planejar vários VPCs e implantar pelo menos um em cada região, porque um VPC não pode ser implantado em mais de uma região.
Por padrão, os VPCs não são interconectados. Para interconectar os VPCs, use o [Peering Connection](https://intl.cloud.tencent.com/document/product/553) ou o [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003).
![](https://main.qcloudimg.com/raw/8e08edafd53646887f337be56836e56c.png)
 - **Vários negócios estão implantados na mesma região e exigem isolamento**
Se você tiver vários negócios implantados na mesma região e eles precisarem ser isolados uns dos outros, será necessário planejar vários VPCs e implantar um VPC para cada negócio. Isso pode isolar os negócios, pois os VPCs não são interconectados por padrão.
![](https://main.qcloudimg.com/raw/ec02b9e821f2a723a3e2d90bfab553bb.png)

<span id="planSubnet" ></span>
## Como planejar a quantidade de sub-redes?
- Um VPC pode ter várias (100, por padrão) sub-redes. Sub-redes diferentes no mesmo VPC podem se comunicar entre si por meio de uma rede privada, por padrão.
- Para ter acesso a recuperação de desastre em zonas de disponibilidade, recomendamos que crie pelo menos duas sub-redes em zonas de disponibilidade diferentes para um VPC.

<span id="planCIDR"></span>
## Como planejar os intervalos de IP (blocos CIDR) de VPCs e sub-redes?

**Depois de definidas, as máscaras de intervalo de IP dos VPCs e das sub-redes não podem ser modificadas.** Portanto, planeje cuidadosamente os VPCs e as sub-redes com base em sua escala de negócios e cenários de comunicação. Isso facilitará um dimensionamento e operações perfeitos no futuro.
#### Planejamento de intervalos de IP do VPC
- **Você pode usar qualquer um dos seguintes intervalos de IP como seus intervalos de IP do VPC:**
 - **10.0**.0.0 - **10.255**.255.255 (**o intervalo das máscaras deve ser de 16 a 28**)
 - **172.16**.0.0 - **172.31**.255.255 (**o intervalo das máscaras deve ser de 16 a 28**)
 - **192.168**.0.0 - **192.168**.255.255 (**o intervalo das máscaras deve ser de 16 a 28**)
- **Ao planejar intervalos de IP do VPC, observe que:**
 - Se você precisar criar vários VPCs que se comunicam entre si ou com IDCs, certifique-se de que os intervalos de IP dos VPCs não se sobreponham.
 - Se seu VPC precisar se comunicar com a rede clássica, o intervalo de IP do VPC que você criar deve estar dentro de `10.[0-47].0.0/16` (incluindo os subconjuntos).
 - Depois de criados, os blocos CIDR dos VPCs e das sub-redes não podem ser modificados. Quando os blocos CIDR forem insuficientes, é possível [criar blocos CIDR auxiliares](https://intl.cloud.tencent.com/document/product/215/31805). No entanto, essa funcionalidade ainda está em beta e aumenta a complexidade operacional. Recomendamos que você planeje cuidadosamente os intervalos de IP ao criar os VPCs e as sub-redes.

#### Planejamento de intervalos de IP da sub-rede
- **Intervalo de IP da sub-rede**: é possível usar seu intervalo de IP do VPC ou parte dele como o intervalo de IP da sub-rede. Por exemplo, se o intervalo de IP do VPC for 10.0.0.0/16, o intervalo de IP da sub-rede pode estar entre 10.0.0.0/16-10.0.255.255/28.
- **Tamanho da sub-rede e capacidade de IP**: depois de criadas, as sub-redes não podem ser modificadas. Ao criar sub-redes, certifique-se de que os intervalos de IP da sub-rede conseguem atender às suas necessidades de negócios. No entanto, também é necessário controlar o tamanho da sub-rede, com a possibilidade de criar sub-redes posteriormente para a expansão.
- **Requisitos de negócios**: um único VPC pode ser dividido em sub-redes com base em segmentos de negócios. Por exemplo, você pode implantar a camada da web, a camada lógica e a camada de dados em sub-redes diferentes e usar [ACLs de rede](https://intl.cloud.tencent.com/document/product/215/31850) para implementar o controle de acesso.

>?
>- Se o VPC em que as sub-redes estiverem localizadas precisar se comunicar com outros VPCs ou IDCs, certifique-se de que o intervalo de IP da sub-rede não se sobreponha ao intervalo de IP de par. Caso contrário, a interconexão por meio de uma rede privada pode falhar.
>- Se os intervalos de IP da sub-rede se sobrepuserem, você pode [alterar a sub-rede da instância](https://intl.cloud.tencent.com/document/product/213/16565) e usar o CCN ou criar um VPC novo e adquirir CVMs.

<span id="planRoute" ></span>
## Como planejar a quantidade de tabelas de rotas?
Uma tabela de rotas é usada para controlar a direção do tráfego em uma sub-rede. Cada sub-rede só pode ser vinculada a uma tabela de rotas. Você pode usar a tabela de rotas padrão e tabelas de rotas personalizadas nos VPCs do Tencent Cloud.
- **Planejamento de uma tabela de rotas**
Se sub-redes diferentes em seu VPC tiverem requisitos iguais ou semelhantes para a direção do tráfego, recomendamos o planejamento de uma tabela de rotas. Em seguida, você pode criar políticas de roteamento diferentes para controlar a direção do tráfego.
![](https://main.qcloudimg.com/raw/0fdd4b7616e92011e3fd9d8141bc49a4.png)
- **Planejamento de várias tabelas de rotas**
Se as sub-redes em seu VPC tiverem requisitos diferentes para a direção do tráfego, recomendamos o planejamento de várias tabelas de rotas. Em seguida, você pode vinculá-las às sub-redes correspondentes e criar políticas de roteamento para controlar a direção do tráfego.
![](https://main.qcloudimg.com/raw/6f13922803b6531e77cdeb983e27b01e.png)

<span id="planExample" ></span>
## Como planejar uma rede de nuvem híbrida multicêntrica entre regiões?
- Se você precisar criar vários VPCs que se comunicam entre si ou com IDCs, certifique-se de que os intervalos de IP dos VPCs não se sobreponham ao intervalo de IP de par.
Suponha que você tenha um IDC local com intervalo de IP `10.1.0.0/16` em Chengdu e deseja criar dois IDCs em nuvem em Xangai e Pequim, que precisam se comunicar com seu IDC local. Nesse caso, recomendamos que você use `10.2.0.0/16` e `10.3.0.0/16` como os intervalos de IP do VPC dos dois IDCs de nuvem em Xangai e Pequim, respectivamente, para evitar falha de comunicação causada por intervalos de IP sobrepostos. Você pode habilitar a comunicação entre IDC local e IDCs de nuvem e entre os IDCs de nuvem usando os dois métodos abaixo.
- **Método 1:** adicione-os a um CCN para implementar a interconexão na rede pública e privada.
![](https://main.qcloudimg.com/raw/05d61e7d26768a3e539858ba51d90f31.png)
- **Método 2:** use o Direct Connect para conectar os IDCs de nuvem em Xangai e Pequim ao IDC local em Chengdu, permitindo assim a comunicação entre o IDC local e os IDCs de nuvem. Para permitir a comunicação entre os IDCs de nuvem em Xangai e Pequim, use o Peering Connection para conectar os VPCs correspondentes.
![](https://main.qcloudimg.com/raw/cba1d5751f6e7f6fce991b9ed3877bf9.png)

**Sugestões para casos de uso de vários VPCs:**
- Tente planejar intervalos de IP diferentes para cada VPC.
- Tente planejar intervalos de IP diferentes para sub-redes do VPC se cada VPC não puder ter um intervalo de IP distinto.
- Certifique-se de que os intervalos de IP das sub-redes que precisam se comunicar sejam diferentes se cada sub-rede não puder ter um intervalo de IP distinto.

## Documentação
- Para obter mais informações sobre como criar um Virtual Private Cloud (VPC) com bloco CIDR IPv4 de forma rápida, incluindo a criação de um VPC e uma sub-rede, a aquisição de um CVM e a vinculação de um EIP para permitir o acesso à rede pública, consulte [Criação de um VPC IPv4](https://intl.cloud.tencent.com/document/product/215/31891).
