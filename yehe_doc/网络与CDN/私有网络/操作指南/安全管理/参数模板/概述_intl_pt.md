Um modelo de parâmetros é um conjunto de parâmetros de endereço IP ou porta de protocolo. Você pode salvar endereços IP ou portas de protocolo com as mesmas necessidades como um modelo, para que possa importar diretamente o modelo como o IP de origem/destino ou a porta de protocolo ao adicionar regras de grupo de segurança. Os modelos de parâmetros, se usados corretamente, podem aumentar a eficiência no uso de grupos de segurança.

## Casos de uso
Os modelos de parâmetros são adequados principalmente para os seguintes cenários:
- Gerenciar vários grupos de endereços IP ou de portas de protocolo com os mesmos requisitos.
- Gerenciar vários grupos de endereços IP ou de portas de protocolo com necessidades de edição frequentes.

## Tipos de modelos de parâmetros
A Tencent Cloud aceita os quatro tipos de modelos de parâmetros a seguir:
- Endereço IP: também conhecido como objeto de endereço IP, esse modelo é um conjunto de endereços IP e aceita um único IP, bloco CIDR e intervalo de IP.
- Grupo de endereços IP: também conhecido como objeto de grupo de endereços IP, esse modelo é um conjunto de vários objetos de endereço IP.
- Porta de protocolo: também conhecido como objeto de porta de protocolo, esse modelo é um conjunto de portas de protocolo e aceita uma única porta, várias portas, intervalo de portas e todas as portas. Ele aceita os protocolos TCP, UDP, ICMP e GRE.
- Grupo de portas de protocolo: também conhecido como objeto de grupo de portas de protocolo, esse modelo é um conjunto de objetos de porta de protocolo.
