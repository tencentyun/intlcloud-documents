O CLB permite a criação de instâncias do CLB anycast. O CLB anycast é um serviço de balanceamento de carga que aceita a aceleração dinâmica entre regiões. O VIP do CLB é publicado em várias regiões. O cliente se conecta ao POP mais próximo e encaminha o tráfego para uma instância do CVM, por meio da Internet de alta velocidade do IDC do Tencent Cloud.
O CLB anycast pode alcançar a otimização da transferência de rede e o acesso próximo de várias entradas e reduzir a tremulação da rede e a perda de pacotes, o que pode melhorar a qualidade do serviço de aplicativos na nuvem, expandir o escopo do serviço e otimizar a implantação de back-end.
>?Atualmente, essa funcionalidade está em teste beta. Para solicitar um teste, envie um tíquete de qualificação para o teste beta.

## O que é anycast?
Anycast significa que quando o mesmo IP é publicado em vários locais simultaneamente, o algoritmo de roteamento entregará o tráfego do usuário ao roteador mais próximo.
Vantagens do CLB anycast:
- **Baixa latência**
O CLB anycast publica o VIP em várias regiões simultaneamente por meio do anycast. De acordo com o protocolo de transferência, um pacote de solicitação chegará à região de publicação do VIP ideal para obter acesso privilegiado ao Tencent Cloud e, em seguida, chegará à instância do CVM por meio da rede privada do Tencent Cloud, evitando o congestionamento da rede pública e reduzindo a latência.
- **Tremulação reduzida e perda de pacotes**
A instabilidade de transmissão de redes públicas entre bordas ou entre operadoras pode resultar em instabilidade da rede e perda de pacotes, prejudicando a experiência do serviço. Já o CLB anycast possui alta estabilidade de transmissão. Ele fornece às solicitações do cliente acesso próximo ao Tencent Cloud e permite a transmissão entre regiões por meio da conexão de rede privada dedicada do Tencent Cloud, ajudando a eliminar a tremulação e a perda de pacotes.
- **Alta confiabilidade**
A transmissão em redes públicas pode não ser confiável. Quando problemas de linha específicos do ISP tornam os serviços inacessíveis, os usuários geralmente precisam esperar até que os serviços sejam retomados. Com a ajuda do CLB anycast, a rede privada do Tencent Cloud, as redes de ISPs e os POPs do Tencent Cloud podem alcançar vários caminhos e entradas de rede, para eliminar falhas causadas por uma única região ou linha e melhorar a estabilidade da rede.
- **Implantação simplificada**
Quando seus clientes estão distribuídos entre regiões e precisam de acesso próximo, você deve implantar servidores em todas essas regiões e configurar o DNS para obter balanceamento de carga, e os IPs variam por região, tornando a implantação ainda mais complicada. Por meio do CLB anycast, o atributo região é convergido no nível do IP, eliminando a necessidade de configurar IPs para cada região. Além disso, você só precisa manter um conjunto de lógica de negócios no back-end, e as solicitações de regiões diferentes são encaminhadas diretamente para servidores de back-end por meio da aceleração da rede privada.

## Arquitetura do CLB anycast
A arquitetura do CLB anycast é conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/22e2999156768fa7866b70001280fce5.png)
O VIP do CLB anycast é publicado em várias regiões do mundo. O cliente se conecta ao POP mais próximo e encaminha o tráfego de acesso de maneira ultrarrápida para uma instância do CVM, pela rede privada do Tencent Cloud.

### Região de publicação anycast
Uma região de publicação anycast é onde um endereço IP acelerado é publicado, ou seja, o POP onde o VIP do CLB anycast é publicado. O cliente acessa o POP mais próximo. Atualmente, o CLB anycast aceita publicação simultânea nas seguintes regiões: Pequim, Xangai, Guangzhou, Hong Kong (China), Toronto, Vale do Silício, Frankfurt, Virgínia, Moscou, Singapura, Seul, Mumbai, Bangkok e Tóquio.

### Região do CLB anycast
Assim como uma região de instâncias genéricas do CLB, uma região do CLB anycast é aquela que você selecionou ao adquirir uma instância do CLB anycast ou a região onde está localizado seu servidor de back-end. Atualmente, o CLB anycast está disponível na maioria das regiões.
- China: Pequim, Xangai, Guangzhou e Região administrativa especial de Hong Kong.
- Europa e América do Norte: Toronto, Vale do Silício, Frankfurt, Virgínia e Moscou.
- Sudeste da Ásia: Singapura, Seul, Mumbai, Bangkok e Tóquio.

>?
>- A capacidade anycast do CLB anycast é implementada vinculando um EIP anycast a uma instância do CLB de rede privada.
>- O EIP anycast pode ser vinculado a instâncias do CLB de rede privada, mas não a instâncias do CLB de rede privada clássica ou da rede clássica.
>

## Casos de uso do CLB anycast
### Servidor unificado para acesso entre regiões
Se você fizer parte do setor de jogos, pode desejar que jogadores de lugares diferentes estejam na mesma região do servidor ou que suas filiais ao redor do mundo possam compartilhar o mesmo IDC. Você pode usar o CLB anycast para implantar servidores de back-end em uma região (como Guangzhou), adquirir uma instância do CLB anycast nessa região e selecionar as regiões de publicação conforme necessário. Dessa forma, os jogadores ou funcionários podem obter o acesso próximo aos mesmos servidores de back-end.
![](https://main.qcloudimg.com/raw/548f5853d5d56af85a248d5ee64d2c39.png)

### Aceleração de jogos
O CLB anycast tem sido amplamente utilizado na aceleração de jogos. Por meio do CLB anycast, as solicitações de jogos podem ter acesso próximo ao Tencent Cloud e chegar aos servidores de jogos por meio da rede privada do Tencent Cloud, encurtando muito o caminho da rede pública e reduzindo problemas como atraso, tremulação e perda de pacotes. Em comparação com a aceleração tradicional, o CLB anycast não requer implantação extra de receptores de tráfego na entrada e elimina a necessidade de zoneamento, simplificando a implantação de DNS.
![](https://main.qcloudimg.com/raw/c1db004b30c41a6c0968e95a2197332b.png)


## Guia de operação
### Pré-requisitos
Atualmente, essa funcionalidade está em beta. Certifique-se de que sua solicitação para a qualificação para o teste beta foi aprovada antes de usá-la.

### Instruções
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na barra lateral esquerda, clique em **[EIP](https://console.cloud.tencent.com/cvm/eip2)** para entrar na página de gerenciamento de EIPs.
3. Clique em **Apply (Aplicar)**. Na janela pop-up, selecione **Accelerated IP (IP acelerado)** como o tipo de endereço IP e clique em **OK**.
![](https://main.qcloudimg.com/raw/838f629b9d40c4db3be1e98dbd95c7f3.png)
4. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb), selecione uma instância do CLB de rede privada (instâncias do CLB da rede clássica não são aceitas) e clique em **More (Mais)** > **Bind Accelerated IP (Vincular IP acelerado)** na coluna "Operation (Operação)".
![](https://main.qcloudimg.com/raw/e4877ad575321d2599b3258cf741a8a3.png)
5. Depois que a instância do CLB da rede privada for vinculada a um IP acelerado, ela poderá fornecer o serviço do CLB anycast. Para obter mais informações sobre a configuração do CLB, consulte a [Visão geral do listener do CLB](https://intl.cloud.tencent.com/document/product/214/6151).
![](https://main.qcloudimg.com/raw/f8e1334deb5679de7b5330208782a5e4.png)
