
### Por que, por padrão, um grupo de segurança tem uma regra de rejeição?

As regras dos grupos de segurança entram em vigor sequencialmente de cima para baixo. Se uma regra de permissão pré-definida entrar em vigor, por padrão, as outras regras serão rejeitadas. Se essa regra de permissão abrir todas as portas para a Internet, a última regra de rejeição não terá efeito. Fornecemos essa configuração padrão por questões de segurança.

### Como posso ajustar a prioridade de um grupo de segurança?

Para mais informações, consulte [Ajuste da prioridade de grupos de segurança](https://intl.cloud.tencent.com/document/product/213/35375).

### Caso eu vincule um grupo de segurança incorreto a uma instância, qual será o impacto? Como posso corrigir esse problema?

**Problemas possíveis**

- Pode falhar ao se conectar remotamente a uma instância do Linux por SSH ou a uma instância do Windows por meio da Área de Trabalho Remota.
- Pode falhar ao executar ping remotamente nos endereços IP público e privado da instância da CVM nesse grupo de segurança.
- Pode falhar ao acessar por HTTP os serviços da Web expostos pela instância da CVM nesse grupo de segurança.
- A instância da CVM nesse grupo de segurança pode falhar ao acessar os serviços da Internet.

**Soluções**

- Se ocorrer algum dos problemas mencionados acima, você pode acessar os **Security Groups (Grupos de segurança)** no console e modificar a regra do grupo de segurança. Por exemplo, você pode alterar a regra para “bind only all-ports-open security groups by default (vincular apenas os grupos de segurança de todas as portas abertas por padrão)”.
- Para mais informações sobre como definir uma regra de grupo de segurança, consulte [Grupos de segurança](https://intl.cloud.tencent.com/document/product/213/12452).

### O que significam a direção e a política do grupo de segurança?

Existem direções do grupo de segurança de entrada e de saída. A direção de saída filtra o tráfego de saída da instância da CVM, já a direção de entrada filtra o tráfego de entrada da instância da CVM.
As políticas de grupos de segurança são divididas entre as que **permitem** e as que **recusam** o tráfego.

### Em que ordem as políticas de grupos de segurança entram em vigor?

As políticas de grupos de segurança entram em vigor sequencialmente de cima para baixo quando o tráfego flui pelo grupo de segurança. Assim que o tráfego corresponder a uma política, ela entrará em vigor imediatamente.

### Por que um endereço IP rejeitado por um grupo de segurança ainda pode acessar a instância da CVM?

Os motivos possíveis são:
- A CVM está vinculado a vários grupos de segurança, e esse endereço IP é permitido por outro grupo de segurança entre eles.
- Este endereço IP pertence a um serviço público aprovado da Tencent Cloud.

### O iptables pode ser usado junto com os grupos de segurança?

Sim. Os grupos de segurança e o iptables podem ser usados ao mesmo tempo. Seu tráfego será filtrado duas vezes nas seguintes direções:
- Saída: processos na instância > iptables > grupos de segurança.
- Entrada: grupos de segurança > iptables > processos na instância.

### Por que os grupos de segurança não podem ser excluídos mesmo que todas as instâncias da CVM tenham sido retornadas?

Verifique se ainda existem instâncias da CVM na lixeira. Se os grupos de segurança ainda estiverem vinculados a uma instância da CVM na lixeira, eles não poderão ser excluídos.

### O nome de um grupo de segurança clonado pode ser o mesmo de um grupo de segurança na região de destino?

Não. O nome deve ser diferente de qualquer grupo de segurança existente na região de destino.

### Um grupo de segurança pode ser clonado entre diferentes usuários?

Não. Atualmente, essa funcionalidade não é compatível.

### Existe alguma API da Tencent Cloud que permita a clonagem de um grupo de segurança entre projetos e regiões?

Embora o suporte do MC seja fornecido para ajudar os clientes que usam o console, nenhuma API da Tencent Cloud pode ser usada diretamente para essa finalidade no momento. Você pode usar as APIs originais da Tencent Cloud para importação e exportação em lote de regras de grupo de segurança, a fim de clonar indiretamente um grupo de segurança entre projetos e regiões.

### Quando clono um grupo de segurança entre projetos e regiões, as instâncias da CVM gerenciadas pelo grupo de segurança também serão copiadas?

Não. Quando um grupo de segurança é clonado entre regiões, somente as regras de entrada e de saída do grupo de segurança original serão copiadas. Portanto, você precisa vincular as instâncias da CVM ao grupo de segurança separadamente.

### O que é um grupo de segurança?
Um grupo de segurança é um firewall virtual que oferece filtragem de pacotes de dados com monitoração de estado. Ele é usado para configurar o controle de acesso à rede da CVM, do Cloud Load Balancer, do TencentDB e de outras instâncias, além de controlar o seu tráfego de saída e de entrada. É um meio importante de isolamento de segurança de rede.

Cada instância da CVM está vinculada a pelo menos um grupo de segurança, que deve ser especificado quando ela é criada. As instâncias da CVM são interconectadas no mesmo grupo de segurança, mas não podem se comunicar com as instâncias da CVM entre grupos de segurança. No entanto, você pode autorizar a interconexão entre dois grupos de segurança. Para mais informações, consulte [Grupos de segurança](https://intl.cloud.tencent.com/document/product/213/12452).

### Por que preciso escolher um grupo de segurança ao criar instâncias da CVM?
Antes de criar instâncias da CVM, você deve escolher um grupo de segurança para particionar os domínios de segurança do ambiente de aplicativos e autorizar as regras do grupo de segurança para implementar adequadamente o isolamento de segurança de rede.

### O que devo fazer ao criar instâncias da CVM se não tiver criado um grupo de segurança?
Nesse caso, você pode criar um grupo de segurança.
Um grupo de segurança aceita as regras a seguir. Você pode abrir os IPs e as portas conforme necessário.
- ICMP: abre para o protocolo ICMP e permite o ping do servidor na rede pública.
- TCP:80: abre a porta 80 e permite o acesso a serviços Web por HTTP.
- TCP:22: abre a porta 22 e permite uma conexão remota com os CVMs do Linux por SSH.
- TCP:443: abre a porta 443 e permite o acesso a serviços Web por HTTPS.
- TCP:3389: abre a porta 3389 e permite uma conexão remota com as CVMs do Windows por RDP.
- Open the private network (Abrir a rede privada): abre para a rede privada e permite o acesso à rede privada entre diferentes recursos de nuvem (IPv4).


### Em que situações a regra de grupo de segurança padrão será usada para um grupo de segurança?
A regra de grupo de segurança padrão será usada nas seguintes situações:
- Se você adquirir e criar uma instância da CVM com **Custom Configuration (Configuração personalizada)**, um grupo de segurança padrão que usa a regra de segurança padrão será criado automaticamente. A regra de entrada desse grupo abre todas as portas e a regra de saída permite todos os acessos.
No entanto, por motivos de segurança, recomendamos que você associe sua CVM a um novo grupo de segurança que só abre as portas quando realmente for aplicável, a fim de evitar riscos de segurança desnecessários.
- Você pode escolher um modelo ao criar um grupo de segurança no console da CVM. Atualmente, os modelos compatíveis incluem login do Windows, login do Linux, Ping, HTTP(80) e HTTPS(443).
