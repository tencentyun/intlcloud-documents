## Classiclink
### Cenário de operação
Por padrão, um VPC é um espaço de rede totalmente isolado que não consegue se interconectar com outras instâncias do VPC ou com a rede clássica por meio de uma rede privada. O [Peering Connection](https://intl.cloud.tencent.com/document/product/553) permite que instâncias diferentes do VPC se comuniquem entre si, e o Classiclink permite que as instâncias do VPC se comuniquem com a rede clássica.

Os CVMs da rede clássica conseguem acessar recursos de nuvem em um VPC, como CVMs, bancos de dados em nuvem, CLBs de rede privada e caches em nuvem. No entanto, os CVMs no VPC conseguem acessar apenas os CVMs da rede clássica que estão interconectados com ele, mas não outros recursos de computação dentro da rede clássica.

>?O Classiclink está disponível apenas para interconexão intra-região.

### Impactos da configuração básica
- Os endereços IP privados dos CVMs da rede clássica associados serão adicionados automaticamente à política local da tabela de rotas do VPC. Dessa forma, os CVMs no VPC e os CVMs nessa rede clássica comunicam entre si, sem a necessidade de modificar manualmente a política da tabela de rotas no VPC atual. 
- Depois que o CVM da rede clássica for associado ao VPC, os firewalls de segurança e ACLs de rede do CVM permanecerão efetivos.
É possível configurar a ACL de rede para a sub-rede do VPC, a fim de restringir o acesso do CVM da rede clássica associado. Também é possível configurar regras de grupo de segurança para os CVMs na rede clássica e o VPC, a fim de restringir as tentativas de acesso à rede em ambas as direções.

### Limites de uso
#### Restrições
- Apenas a interconexão entre as instâncias do VPC e a rede clássica **na mesma região** é compatível.
- A funcionalidade Classiclink está disponível apenas para as instâncias do VPC dentro do segmento de rede de `10.[0-47].0.0/16`. O intervalo de IP para instâncias do VPC em outros segmentos de rede pode entrar em conflito com o segmento de IP da rede clássica.
- Um CVM da rede clássica pode ser associado a um VPC por vez.
- Um VPC pode ser associado a no máximo 100 CVMs da rede clássica.
- Os recursos do VPC só conseguem acessar os CVMs na rede clássica, em vez de outros recursos na rede clássica, como bancos de dados em nuvem e CLBs.

#### Observações
- A instância do CLB em um VPC não pode ser vinculada a um CVM da rede clássica interconectado com o mesmo VPC.
- Alterar o endereço IP privado de um CVM da rede clássica cancela a associação com o VPC, o que significa que o registro de associação original se tornará inválido. Adicione o registro novamente no console do VPC se quiser associá-los mais uma vez.
- O relacionamento de interconexão com o VPC não será desvinculado por ações tomadas em relação ao CVM, como o isolamento devido a pagamentos em atraso, o isolamento de segurança, a migração a frio, o failover, a modificação de configuração e a troca de sistema operacional.
- O relacionamento de interconexão com o VPC será desvinculado automaticamente se o CVM for retornado.
- Em situações com Classiclink, o tráfego do CVM só pode ser roteado para endereços IP privados dentro do VPC, mas não para destinos fora do VPC. Ou seja, o CVM da rede clássica não consegue acessar os recursos da internet ou do VPC fora do VPC atual por meio de dispositivos de rede, como seu gateway VPN, gateway do Direct Connect, gateway público, Peering Connection e NAT Gateway. Da mesma forma, o par de um gateway VPN, gateway do Direct Connect e Peering Connection não conseguem acessar o CVM da rede clássica.

### Etapas
Para obter informações sobre como operar o Classiclink, consulte [Gerenciamento da rede clássica](https://intl.cloud.tencent.com/document/product/215/31807).

## Conexões de terminal
A conexão de terminal é outro método para conectar as instâncias do VPC e a rede clássica. Ela conecta as instâncias em um VPC e as instâncias que não são do CVM na rede clássica por meio de uma rede privada. Os produtos da rede clássica que são compatíveis com as conexões de terminal incluem o CLB, o MySQL, o Memcached, o Redis e o MongoDB.

Uma conexão de terminal estabelece o mapeamento entre endereços IP de instâncias da rede clássica e endereços IP do VPC, para que as instâncias da rede clássica possam ser acessadas pelos endereços IP do VPC.

>?As conexões de terminal entre regiões ou entre contas não são compatíveis. Caso precise estabelecer uma conexão de terminal nessas situações, envie um [tíquete para solicitá-la](https://console.cloud.tencent.com/workorder/category).


