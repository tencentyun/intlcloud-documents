Um grupo de segurança é um firewall virtual que oferece filtragem de pacotes de dados com monitoração de estado. Ele é usado para configurar o controle de acesso à rede do CVM, do Cloud Load Balancer, do TencentDB e de outras instâncias, além de controlar o seu tráfego de saída e de entrada. É um meio importante de isolamento de segurança de rede.
É possível configurar regras de grupo de segurança para permitir ou rejeitar o tráfego de entrada e de saída de instâncias dentro do grupo de segurança.

## Funcionalidades do grupo de segurança
- Um grupo de segurança é um grupo lógico. É possível adicionar CVM, ENI, TencentDB e outras instâncias na mesma região com os mesmos requisitos de isolamento de segurança de rede ao mesmo grupo de segurança.
- Por padrão, as instâncias no mesmo grupo de segurança não são interconectadas, a menos que você permita especificando regras.
- Os grupos de segurança têm estado. O tráfego de entrada que você permitiu pode se tornar automaticamente de saída e vice-versa.
- É possível modificar as regras do grupo de segurança a qualquer momento e as novas regras entrarão em vigor imediatamente.

## Limites de uso

Para obter mais informações sobre os limites de uso e as cotas dos grupos de segurança, consulte os **limites do grupo de segurança** na [Visão geral dos limites de uso](https://intl.cloud.tencent.com/document/product/213/15379).

## Regras de grupos de segurança
### Componentes
Uma regra de grupo de segurança consiste em:
- Origem: endereço IP dos dados de origem (entrada) ou dados de destino (saída).
- Tipo de protocolo e porta de protocolo: o tipo de protocolo, como TCP, UDP, etc.
- Política: permitir ou rejeitar a solicitação de acesso.

### Prioridades das regras
- As regras em um grupo de segurança são priorizadas de cima para baixo. A regra no topo da lista tem a prioridade mais alta e entrará em vigor primeiro, enquanto a regra na parte inferior tem a prioridade mais baixa e entrará em vigor por último.
- Se houver um conflito de regras, a regra com a prioridade mais alta prevalecerá por padrão.
- Quando o tráfego entra ou sai de uma instância vinculada a um grupo de segurança, as regras do grupo de segurança serão correspondidas sequencialmente de cima para baixo. Se uma regra for correspondida com êxito e entrar em vigor, as regras subsequentes não serão correspondidas.

### Vários grupos de segurança
Uma instância pode ser vinculada a um ou vários grupos de segurança. Quando ela está vinculada a vários grupos de segurança, as regras do grupo de segurança serão correspondidas sequencialmente de cima para baixo. É possível ajustar as prioridades dos grupos de segurança a qualquer momento.

## Modelos de grupos de segurança
Ao criar um grupo de segurança, é possível selecionar um dos dois modelos de grupos de segurança fornecidos pelo Tencent Cloud:
- O modelo que abre todas as portas: todo o tráfego de entrada e de saída terá permissão para passar.
- O modelo que abre as portas principais: a porta TCP 22 (para login SSH do Linux), as portas 80 e 443 (para serviço web), a porta 3389 (para login remoto do Windows), o protocolo ICMP (para comandos ping) e a rede privada serão abertos para a internet.

>?
> - Se esses modelos não atenderem às suas necessidades reais, é possível criar grupos de segurança personalizados. Para obter mais informações, consulte [Criação de um grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34271) e [Casos de uso de grupos de segurança](https://intl.cloud.tencent.com/document/product/213/32369).
> - Se for necessário proteger a camada de aplicativos (HTTP/HTTPS), ative o [Tencent Cloud Web Application Firewall (WAF)](https://intl.cloud.tencent.com/product/waf), que fornece segurança na web na camada de aplicativos para se defender contra vulnerabilidades na web, rastreadores mal-intencionados e ataques CC, ajudando a proteger seus sites e aplicativos web.
>

## Como usar um grupo de segurança
A figura a seguir mostra como usar um grupo de segurança:
![](https://main.qcloudimg.com/raw/fbd5b2ec62e94f2cfee45d8b125f3e82.png)

## Práticas recomendadas de grupos de segurança

### Criação de um grupo de segurança
- Recomendamos que você especifique um grupo de segurança ao adquirir um CVM por API. Caso contrário, o grupo de segurança padrão será usado e não poderá ser excluído.
- Se você precisar alterar a política de proteção da instância, recomendamos modificar as regras existentes em vez de criar um grupo de segurança novo.

### Gerenciamento de regras
- Exporte e faça backup das regras de grupos de segurança antes de modificá-las, para que você possa importá-las e restaurá-las se ocorrer um erro.
- Para criar várias regras de grupos de segurança, use o [modelo de parâmetros](https://intl.cloud.tencent.com/document/product/215/31867).

### Associação de um grupo de segurança
- É possível adicionar instâncias com os mesmos requisitos de proteção ao mesmo grupo de segurança, em vez de configurar um grupo de segurança separado para cada instância.
- Não é recomendado vincular uma instância a muitos grupos de segurança, porque as regras em diferentes grupos podem entrar em conflito e resultar na desconexão da rede.

