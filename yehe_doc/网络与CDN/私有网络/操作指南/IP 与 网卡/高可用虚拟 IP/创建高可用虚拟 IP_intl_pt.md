Este documento descreve como criar um HAVIP no console e configurá-lo em um software de terceiros.

## Instruções
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc/) e selecione **IP and Interface (IP e interface)** > **HAVIP** na barra lateral esquerda. 
2. Selecione a região em questão na página de gerenciamento do HAVIP e clique em **Apply (Solicitar)**.
3. Na caixa de diálogo pop-up, configure os parâmetros do HAVIP.
 + **Name (Nome)**: insira um nome para o HAVIP.
 + **Virtual Private Cloud**: selecione um VPC no qual o HAVIP a ser criado está localizado.
 + **Subnet (Sub-rede)**: selecione uma sub-rede específica para o HAVIP.
 + **IP address (Endereço IP)**: o endereço IP do HAVIP pode ser atribuído automaticamente ou especificado de forma manual. Se você escolher **Automatic Assignment (Atribuição automática)**, um endereço IP da sub-rede será atribuído automaticamente. Se você escolher **Enter manually (Inserir manualmente)**, certifique-se de que o endereço IP inserido esteja no intervalo de IP da sub-rede e não seja um endereço IP reservado do sistema. Por exemplo, se o intervalo de IP da sub-rede for `10.0.0.0/24`, o endereço IP privado inserido deve estar dentro de `10.0.0.2-10.0.0.254`.
4. Clique em **OK**. Depois que o HAVIP for criado, ele será exibido na lista e seu status será **Not bound with CVM yet (Ainda não vinculado ao CVM)**.

## Configuração de um HAVIP
Um HAVIP é projetado para ser usado junto com um software de alta disponibilidade (HA, na sigla em inglês) de terceiros, que deve ser configurado no software de HA de terceiros. Um HAVIP é apenas um objeto de operação e um endereço IP privado que pode ser vinculado por meio de anúncio. Portanto, a vinculação e a desvinculação de HAVIP a CVMs não são feitas no console do Tencent Cloud. Em vez disso, basta especificar o HAVIP como um endereço IP virtual (VIP) flutuante no software de HA de terceiros, que por sua vez especifica um ENI a ser vinculado ao HAVIP por meio do ARP. Veja abaixo como vincular ou desvincular um HAVIP:
![](https://main.qcloudimg.com/raw/1007a3d550fda9bf404673be571bf2dc.png)
Em um ambiente de dispositivo físico tradicional, todos os endereços IP privados são vinculados a ENIs por meio do ARP, por padrão, e podem ser especificados como endereços IP flutuantes no software de HA. Em um ambiente de nuvem pública, um IP privado não pode usar o ARP ou ser especificado como um endereço IP flutuante no software de HA. Portanto, é necessário seguir as mesmas etapas do software de terceiros para especificar o HAVIP como um endereço IP flutuante.

>?Programas de software de HA comuns incluem: o Linux HeartBeat, o Keepalived, o Pacemaker e o Windows MSCS.
>
Ao especificar um VIP no arquivo de configuração do software de HA, basta inserir o HAVIP que você criou:

```	
vrrp_instanceVI_1 {
# Selecione os parâmetros adequados para os CVMs principais e secundários.
    state MASTER               #Defina o status inicial como `Backup`.
    interface eth0              #O ENI (tais como `eth0`) usado para vincular um VIP
    virtual_router_id 51        #O valor `virtual_router_id` para o cluster
		nopreempt                   #Modo Non-preempt
		preempt_delay 10           #Defina o atraso de preempção para 10 minutos
    priority 100               #Prioridade. Quanto maior o valor, maior a prioridade
    advert_int 1               #Intervalo de verificação. O valor padrão é 1 segundo
    authentication {           #Autenticação
        auth_type PASS          #Método de autenticação
        auth_pass 1111          #Senha de autenticação
    }
		unicast_src_ip 172.16.16.5 #Endereço IP privado do dispositivo local
		unicast_peer{
		172.16.16.6                #Endereço IP do dispositivo de par
		}
    virtual_ipaddress {     
		172.16.16.12               #HAVIP
    }
	}
```

Depois que as configurações forem concluídas no software de HA do CVM, o status do HAVIP mudará para **Bound with CVM (Vinculado ao CVM)** no console.

Consulte os seguintes casos para realizar as suas configurações:
> + [Criação de cluster principal/secundário de alta disponibilidade usando HAVIP + Keepalived](https://intl.cloud.tencent.com/document/product/215/31877) 
> + [Criação de um banco de dados de alta disponibilidade usando HAVIP + cluster de failover do Windows Server](https://intl.cloud.tencent.com/document/product/215/31878) 

## Documentação
Semelhante a um IP privado, um HAVIP também pode ser vinculado ou desvinculado de um EIP no console. Se você precisar de comunicação de rede pública, consulte [Vinculação ou desvinculação de EIP](https://intl.cloud.tencent.com/document/product/215/40083).


