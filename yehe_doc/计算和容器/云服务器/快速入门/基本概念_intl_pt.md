
### Instância
Uma instância é um Cloud Virtual Machine (CVM), que é um recurso de computação virtual que contém CPU, memória, sistema operacional, rede, discos e outros componentes básicos de computação.
As instâncias do CVM fornecem serviços de computação seguros, confiáveis e elásticos na nuvem para atender aos requisitos de computação. Conforme as demandas da empresa mudam, os recursos de computação podem ser dimensionados em tempo real, a fim de reduzir os custos de software e de hardware e simplificar o trabalho das operações de TI.

### Tipo de instâncias
O Tencent Cloud oferece várias configurações de capacidade de CPU, memória, armazenamento e rede para as instâncias do CVM. Para obter mais informações, consulte os [Tipos de instâncias](https://intl.cloud.tencent.com/document/product/213/11518).

### Imagem
Uma imagem é um modelo pré-configurado que contém um sistema operacional e os aplicativos nos quais as instâncias do CVM são executadas. O Tencent Cloud CVM fornece imagens pré-configuradas para Windows, Linux etc.

### Cloud Block Storage
O Cloud Block Storage (CBS) é um dispositivo de armazenamento em blocos altamente disponível, confiável, de baixo custo e personalizável. Ele pode ser usado como um disco autônomo e expansível para o CVM, fornecendo dispositivos de [armazenamento](https://intl.cloud.tencent.com/document/product/213/4952) eficientes e confiáveis.

### VPC
Um VPC é um espaço de rede virtual isolado logicamente no Tencent Cloud.

### Endereços IP
O Tencent Cloud fornece [endereço IP privado](https://intl.cloud.tencent.com/document/product/213/5225) e [endereço IP público](https://intl.cloud.tencent.com/document/product/213/5224). O endereço IP privado é destinado à interconexão de instâncias do CVM dentro da mesma LAN, já o endereço IP público serve para serviços voltados para o público.

### IP elástico
O IP elástico (EIP) é endereços IP estáticos de rede pública criados especialmente para redes dinâmicas, para atender às demandas de solução rápida de problemas.
Um EIP é um endereço IP público que pode ser solicitado de forma independente. Ele é compatível com a vinculação e desvinculação dinâmicas. Você pode vinculá-lo ou desvinculá-lo do CVM (ou instâncias do NAT Gateway) em sua conta. Seus principais usos são:
- Para manter um IP. O arquivamento do nome de domínio ICP é necessário para IP e DNS da China Continental.
- Para mascarar uma falha de instância. Por exemplo, um nome DNS é mapeado para um endereço IP por meio do mapeamento DNS dinâmico. Pode levar até 24 horas para propagar esse mapeamento para toda a internet, já um IP elástico permite o remapeamento rápido de um IP de um CVM para outro. Quando um CVM falha, basta você iniciar e remapear outra instância para responder rapidamente às falhas da instância.

### Grupo de segurança
Um grupo de segurança é um firewall virtual que oferece filtragem de pacotes de dados com monitoração de estado. É usado para configurar o controle de acesso à rede dos CVMs. É possível adicionar instâncias do CVM com os mesmos requisitos de isolamento de segurança de rede na mesma região ao mesmo grupo de segurança, para filtrar o tráfego de entrada e de saída do CVM por meio das políticas de rede do grupo de segurança.

### Método de login
A senha é uma credencial de login exclusiva para a instância do CVM. Para garantir a segurança da instância, o Tencent Cloud fornece dois métodos de login criptografado conforme abaixo:
- Os [Pares de chaves SSH](https://intl.cloud.tencent.com/document/product/213/6092) são mais fáceis de usar. Você pode fazer login em instâncias remotamente com algumas etapas simples de configuração no console e no cliente local, e não precisa inserir uma senha ao fazer login novamente.
- A [Senha de login](https://intl.cloud.tencent.com/document/product/213/6093) permite que qualquer pessoa com a senha faça login na instância do CVM remotamente por meio de um endereço de rede pública permitido pelo grupo de segurança.

### Regiões e zonas de disponibilidade
Locais físicos onde as instâncias do CVM e outros recursos residem e são iniciados.
- Uma região se refere a uma localização geográfica onde estão localizados os data centers hospedados pelo Tencent Cloud. Cada região possui várias zonas de disponibilidade.
- Uma zona de disponibilidade é um IDC do Tencent Cloud com uma fonte de alimentação independente e rede na mesma região. Pode garantir a estabilidade da empresa, já que falhas de energia em uma AZ são isoladas sem afetar outras AZs na mesma região.



