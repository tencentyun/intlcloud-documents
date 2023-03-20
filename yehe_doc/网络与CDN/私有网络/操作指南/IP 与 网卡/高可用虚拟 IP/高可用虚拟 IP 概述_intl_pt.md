Um IP virtual de alta disponibilidade (HAVIP, na sigla em inglês) é um endereço IP privado atribuído do bloco CIDR de uma sub-rede da VPC. Geralmente, é usado em conjunto com software de alta disponibilidade, como Keepalived e cluster de failover do Windows Server, para criar um cluster principal/secundário altamente disponível.
>?
>- Atualmente, o HAVIP está em versão beta, e podem levar 10 segundos para alternar entre os servidores principal/secundário. Para testá-lo, inscreva-se para ser um usuário beta.
>- Para garantir a alta disponibilidade da CVM em um cluster principal/secundário, recomendamos atribuir CVMs a hosts diferentes usando [grupos de posicionamento](https://intl.cloud.tencent.com/document/product/213/15486). Para mais informações sobre grupos de posicionamento, consulte [Grupo de posicionamento](https://intl.cloud.tencent.com/document/product/213/15486).
>- O software de alta disponibilidade deve permitir o envio de mensagens ARP.

## Funcionalidades
- É possível solicitar vários endereços HAVIP no console para cada VPC.
- Você deve vincular o HAVIP no arquivo de configuração da CVM.


## Arquitetura e princípio
Normalmente, um cluster principal/secundário de alta disponibilidade consiste em dois servidores: um servidor principal ativo e um servidor secundário em espera. Os dois servidores compartilham o mesmo VIP (IP virtual). O VIP só pode trabalhar em um servidor principal ao mesmo tempo. Quando o servidor principal falhar, o servidor secundário assumirá o VIP para continuar fornecendo serviços.
+ Em redes físicas tradicionais, o status principal/secundário pode ser negociado com o protocolo VRRP do Keepalived. O dispositivo principal envia periodicamente mensagens ARP gratuitas para limpar a tabela MAC ou a tabela ARP do terminal da troca de uplink, de modo a acionar a migração VIP para o dispositivo principal.
+ Em uma VPC, um cluster principal/secundário de alta disponibilidade também pode ser implementado ao implantar o Keepalived em CVMs. No entanto, uma instância da CVM geralmente não pode obter um IP privado por meio de anúncio ARP por motivos de segurança, como falsificação de ARP. O VIP deve ser um HAVIP solicitado da Tencent Cloud, que é específico da sub-rede. Portanto, o HAVIP só pode ser vinculado a um servidor na mesma sub-rede por meio de anúncio.
>?O Keepalived é um software de alta disponibilidade baseado em VRRP. Para usar o Keepalived, primeiro conclua sua configuração no arquivo `Keepalived.conf`.

A figura a seguir mostra a arquitetura do HAVIP.
![](https://main.qcloudimg.com/raw/e8d0e60cbd3221089256087c5686588f.png)
De acordo com a figura de exemplo, o CVM1 e o CVM2 podem ser criados em um cluster principal/secundário de alta disponibilidade com as seguintes etapas:

1. Instale o Keepalived no CVM1 e no CVM2, configure o HAVIP como VIP do VRRP e defina as prioridades dos servidores principal e secundário. Valores maiores representam prioridades mais altas.
2. O Keepalived usa o protocolo VRRP para comparar as prioridades iniciais de CVM1 e CVM2, e determina o CVM1 como o servidor principal devido à sua prioridade mais alta.
3. O servidor principal envia mensagens ARP, anuncia o VIP (um HAVIP) e atualiza o VIP para os mapeamentos MAC. Neste caso, o CVM1 é o servidor principal e fornece serviços utilizando o IP privado (HAVIP) para comunicação. Você pode ver que o HAVIP está vinculado ao servidor principal do CVM1 no console do HAVIP.   
4. (Opcional) Vincule um EIP ao HAVIP no console para implementar a comunicação na rede pública.
5. O servidor principal envia mensagens VRRP ao servidor secundário de forma periódica. Se o servidor principal não conseguir enviar mensagens VRRP dentro de um determinado período, o servidor secundário será definido como principal e enviará mensagens de atualização ARP que carregam seu endereço MAC. Nesse caso, o CVM2 passa a ser o servidor principal para fornecer serviços de comunicação e tratar solicitações de acesso externo. Você verá que a CVM vinculado ao HAVIP muda para o CVM2 no console do HAVIP.

## Casos de uso comuns
- **Alta disponibilidade do Cloud Load Balancer**
  Para implantar o Cloud Load Balancer (CLB), você geralmente usará alta disponibilidade (HA, na sigla em inglês) entre instâncias do CLB e configurará servidores reais como um cluster. Portanto, você deve implantar e usar o HAVIP como um IP virtual entre dois servidores do CLB.
- **Banco de dados relacional principal/secundário**
  Se o Keepalived ou o cluster de failover do Windows Server forem usados entre dois bancos de dados para criar um cluster principal/secundário altamente disponível, use o HAVIP como um IP virtual. Para mais informações, consulte [Criação de cluster principal/secundário de alta disponibilidade usando HAVIP + Keepalived](https://intl.cloud.tencent.com/document/product/215/31877) e [Criação de um banco de dados de alta disponibilidade usando HAVIP + cluster de failover do Windows Server](https://intl.cloud.tencent.com/document/product/215/31878) em Práticas recomendadas.


## Perguntas frequentes

### Por que devo usar o HAVIP junto com o Keepalived em uma VPC?
Alguns fornecedores de nuvem pública não aceitam vincular um IP privado ao CVM por meio do anúncio ARP por motivos de segurança, como falsificação de ARP. Se você usar diretamente um IP privado como o IP virtual no arquivo “Keepalived.conf”, o Keepalived não conseguirá atualizar o mapeamento de IP para MAC durante a alternância de IP virtual do servidor principal/secundário. Neste caso, você deve chamar uma API para alternar o IP.
Usando a configuração do Keepalived como exemplo, as configurações de IP são as seguintes:
```plaintext
vrrp_instance VI_1 {
    state BACKUP           #Dispositivo secundário
    interface eth0          #Nome da ENI 
    virtual_router_id 51
    nopreempt                   #Modo Non-preempt
    #preempt_delay 10
    priority 80
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass 1111
    }
    unicast_src_ip 172.17.16.7 #IP privado do dispositivo local
    unicast_peer{
        172.17.16.13           #Endereço IP do dispositivo de par, por exemplo: 10.0.0.1
    }

    virtual_ipaddress {

        172.17.16.3  #Insira o endereço HAVIP que você solicitou no console.

    }

    garp_master_delay 1
    garp_master_refresh 5

    track_interface {
        eth0              
    }

    track_script {
        checkhaproxy
    }
}
```
Se não houver HAVIP, a seção a seguir do arquivo de configuração será inválida.
```plaintext
virtual_ipaddress {
   172.17.16.3 #Insira o endereço HAVIP que você solicitou no console.
}
```

## Referência
- Para mais informações sobre os limites de uso do HAVIP, consulte [Limites](https://intl.cloud.tencent.com/document/product/215/31818).
- Para mais informações sobre o guia de operação do HAVIP, consulte [Gerenciamento de HAVIP](https://intl.cloud.tencent.com/document/product/215/31820).
