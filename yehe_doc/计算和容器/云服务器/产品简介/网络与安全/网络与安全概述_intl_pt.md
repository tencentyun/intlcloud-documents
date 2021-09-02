O Tencent Cloud oferece infraestrutura de rede e serviços de segurança para garantir que sua empresa permaneça segura, eficiente e flexível.

## Login criptografado
O Tencent Cloud fornece dois métodos de login criptografado usando [Senha de login](https://intl.cloud.tencent.com/document/product/213/6093) e [Chave SSH](https://intl.cloud.tencent.com/document/product/213/6092). Você pode usar qualquer um deles para se conectar à sua instância do CVM. O CVM do Windows não aceita login usando chaves SSH.

## Acesso à rede
Os produtos do Tencent Cloud podem se comunicar uns com os outros usando o [Acesso à internet](https://intl.cloud.tencent.com/document/product/213/5224) ou o [Acesso à rede privada](https://intl.cloud.tencent.com/document/product/213/5225).
 - Acesso à internet: As instâncias do CMV e outros produtos do Tencent Cloud usam o acesso à internet para fornecer serviços voltados ao público. Eles recebem endereços IP públicos para se comunicarem com outros computadores na internet.
 - Acesso à rede privada: O Tencent Cloud atribui endereços IP privados a recursos da mesma região, para que eles possam se comunicar uns com os outros na mesma LAN gratuitamente. 

## Ambiente de rede
O Tencent Cloud fornece dois tipos de [Ambientes de rede](https://intl.cloud.tencent.com/document/product/213/5227): rede básica e redes privadas (VPC).
 - A rede básica é um pool de recursos de rede compartilhado com todos os usuários. Recomendamos a rede básica para os iniciantes.
 - Os VPCs são espaços de rede personalizados que são isolados logicamente. Você pode iniciar as instâncias do CVM em um intervalo de IP predefinido e personalizado para isolar seus recursos daqueles de outros usuários. Recomendamos os VPCs para os usuários que estão familiarizados com a administração de redes.

## Grupos de segurança
Um [grupo de segurança](https://intl.cloud.tencent.com/document/product/213/12452) é um firewall virtual com monitoração de estado que realiza filtragem. Como uma forma importante de isolamento de segurança de rede fornecida pelo Tencent Cloud, ela pode ser usada para definir controles de acesso à rede para uma ou mais instâncias do TencentDB.
Veja a seguir uma lista de casos de uso de grupos de segurança comuns:
 - Crie vários grupos de segurança e defina regras diferentes para eles.
 - Associe um ou mais grupos de segurança a cada uma das suas instâncias do CVM. O sistema usa esses grupos de segurança para controlar o tráfego em direção às suas instâncias e os recursos que elas podem acessar.
 - Configure seus grupos de segurança para que apenas endereços IP ou grupos de segurança específicos possam acessar suas instâncias.

## IPs públicos elásticos
[IPs públicos elásticos](https://intl.cloud.tencent.com/document/product/213/5733), ou EIPs, são endereços IP estáticos criados especialmente para a computação em nuvem.
Recomendamos o uso de EIPs nos seguintes casos:
 - Uma instância pode ficar inativa por motivos imprevisíveis e a instância de failover precisa usar o mesmo endereço IP para fornecer serviço ininterrupto. 
 - Uma instância não tem um endereço IP público, mas ainda precisa de um endereço IP estático.

## ENIs
O [Elastic Network Interface (ENI)](https://intl.cloud.tencent.com/document/product/213/6514) é uma interface de rede elástica que pode ser vinculada a uma instância do CVM em um VPC para fornecer conexão de rede. É possível migrar livremente os ENIs entre as instâncias. Isso é essencial ao configurar e gerenciar redes e realizar implantações de alta disponibilidade.
