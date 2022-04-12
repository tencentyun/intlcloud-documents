## Perguntas frequentes sobre portas
### Quais portas devo abrir antes de fazer login em uma instância?
Normalmente, você precisa abrir a porta 22 para uma instância do Linux ou a porta 3389 para uma instância do Windows. Para mais informações, consulte [Casos de aplicação de grupos de segurança](https://intl.cloud.tencent.com/document/product/215/35519).

### Por que devo abrir uma porta, e como?
Você deve abrir a porta no grupo de segurança para usar os serviços relacionados. 
Por exemplo, se você deseja acessar páginas da Web usando a porta 8080, abra essa porta no grupo de segurança.
Etapas para abrir uma porta: 
1. Faça login no [console do grupo de segurança](https://console.cloud.tencent.com/vpc/securitygroup) e clique no ID/nome do grupo de segurança vinculado a essa instância para acessar sua página de detalhes.
2. Selecione **Inbound/Outbound rule (Regra de entrada/saída)** e clique em **Add a Rule (Adicionar uma regra)**.
3. Digite seu (intervalo de) endereço IP e a porta a ser aberta e selecione **Allow (Permitir)** para abrir a porta.
Para mais informações, consulte [Adição de regras de grupos de segurança](https://intl.cloud.tencent.com/document/product/215/35513).

### Meus negócios ficaram inacessíveis depois que modifiquei a porta.
Depois de modificar a porta de serviço, você também precisa abrir a porta correspondente no grupo de segurança.

### Quais portas não são permitidas pela Tencent Cloud?
As portas a seguir não são permitidas, pois apresentam riscos de segurança e provavelmente serão bloqueadas por ISPs.

| Protocolo   | Portas não permitidas                            |
| ---- | ---------------------------------------- |
| TCP  | 42, 135, 137, 138, 139, 445, 593, 1025, 1434, 1068, 3127, 3128, 3129, 3130, 4444, 5554, 5800, 5900 e 9996 |
| UDP  | 1026, 1027, 1434, 1068, 5554, 9996, 1028, 1433 e 135 - 139 |

## Não consigo me conectar a um endereço externo pela porta 25 do TCP.
- Para melhorar a qualidade do envio de e-mails por meio de endereços IP da Tencent Cloud, os CVMs são impedidos de usar a porta 25 do TCP para se conectarem a endereços externos por padrão. Para desbloquear essa porta, você pode fazer login no [console](https://console.cloud.tencent.com/), passar o mouse sobre a área de navegação da conta na parte superior e clicar em **Security Control (Controle de segurança)** que exibirá o link para desbloquear a porta 25.
- É possível desbloquear os CVMs cinco vezes em cada conta. Atenção: os CVMs com pagamento conforme o uso não são aceitos.

Para mais informações, consulte [Portas comuns do servidor](https://intl.cloud.tencent.com/document/product/215/35520).

## Perguntas frequentes sobre grupos de segurança
### Por que há uma regra de rejeição definida por padrão em um grupo de segurança?
As regras de grupos de segurança são selecionadas para entrar em vigor com base em sua ordem de cima para baixo; portanto, depois que a regra de permissão definida pela primeira vez for validada, as outras regras serão rejeitadas por padrão. Se a regra abrir todas as portas para a Internet, a regra de rejeição final será inválida. Fornecemos essa configuração padrão por questões de segurança.

### Se eu vincular um grupo de segurança incorreto a uma instância, qual será o efeito na instância? Como isso pode ser corrigido?
- **Possíveis problemas**
 - Você pode não conseguir se conectar remotamente a uma instância do Linux (SSH) ou fazer login remotamente na Área de Trabalho de uma instância do Windows.
 - Pode falhar ao executar ping remotamente nos endereços IP público e privado da instância da CVM nesse grupo de segurança.
 - Pode falhar ao acessar por HTTP os serviços da Web expostos pela instância da CVM nesse grupo de segurança.
 - Pode falhar ao acessar a Internet com a instância nesse grupo de segurança.
- **Soluções**
 - Caso aconteça algum dos problemas acima, você pode acessar “Security Group Management (Gerenciamento de grupos de segurança)” no console e redefinir a regra do grupo de segurança para, por exemplo, “only bind all-pass security groups by default (apenas vincular grupos de segurança passa-tudo por padrão)”.
 -Para mais detalhes sobre como definir as regras de grupos de segurança, consulte [Grupo de segurança - Regras de grupos de segurança](https://intl.cloud.tencent.com/document/product/213/12452).

### O que significam a direção e a política de grupos de segurança?
- A política de grupo de segurança funciona nas direções de saída e entrada. A primeira é para filtrar o tráfego de saída da CVM, e a segunda é para filtrar o tráfego de entrada da CVM.
- As políticas do grupo de segurança são divididas entre aquelas que **allow (permitem)** e **refuse (recusam)** o tráfego.

### Qual é a ordem em que as políticas de grupos de segurança entram em vigor?
A ordem em que as políticas de grupos de segurança entram em vigor é de cima para baixo. O tráfego passa pela sequência de correspondência do grupo de segurança de cima para baixo, e a política entra em vigor assim que houver uma correspondência bem-sucedida.

### Por que uma porta aberta para a Internet por um grupo de segurança não pode acessar a instância da CVM?
- A CVM está vinculada a vários grupos de segurança, e essa porta é rejeitada por outro grupo de segurança com prioridade mais alta.
- A ACL de rede ou o firewall foi configurado.

### Como um IP que não é permitido pelo grupo de segurança ainda pode acessar a CVM?
Motivos possíveis: 
- A CVM está vinculada a vários grupos de segurança, e o IP é permitido por outro grupo de segurança.
- Esse endereço IP pertence a um serviço público aprovado da Tencent Cloud.

### O iptables pode ser usado junto com grupos de segurança?
Sim, o iptables e os grupos de segurança podem ser usados ao mesmo tempo. O tráfego será filtrado duas vezes da seguinte forma:
- Saída: processos na instância > iptables > grupos de segurança.
- Entrada: grupos de segurança > iptables > processos na instância.

### Todos os CVMs associados ao grupo de segurança foram retornados. Mas ainda não consigo excluir o grupo de segurança.
Além de CVMs, um grupo de segurança também pode ser vinculado a instâncias do CLB, do ENI e de banco de dados na nuvem. Verifique se todas as instâncias vinculadas ao grupo de segurança a ser excluído foram desassociadas. 

### O nome de um grupo de segurança clonado pode ser o mesmo de um grupo de segurança na região de destino?
Sim.

### Posso clonar um grupo de segurança para outro projeto ou região usando uma API?
Sim. Para mais detalhes, consulte [CloneSecurityGroup](https://intl.cloud.tencent.com/document/product/215/39444).

### Quando eu clono um grupo de segurança para outro projeto ou região, os CVMs associados aos grupos de segurança também serão clonados?
Não. Apenas as regras de entrada e saída do grupo de segurança serão clonadas. Será necessário associar os CVMs novamente após a clonagem.
