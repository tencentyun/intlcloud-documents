
Este documento descreve como usar o Keepalived com o [HAVIP](https://intl.cloud.tencent.com/document/product/215/31817) para criar um cluster principal/secundário de alta disponibilidade no VPC do Tencent Cloud.
>?Atualmente, o HAVIP está em beta, e podem levar 10 segundos para alternar entre os servidores principal/secundário. Para testá-lo, registre-se como um usuário beta.
>

## Princípio básico
Normalmente, um cluster principal/secundário de alta disponibilidade consiste em dois servidores: um servidor principal ativo e um servidor secundário em espera. Os dois servidores compartilham o mesmo VIP (IP virtual), que é válido apenas para o servidor principal. Quando o servidor principal falhar, o servidor secundário assumirá o VIP para continuar fornecendo serviços. Este modo é amplamente usado na alternância de origem/réplica do MySQL e no acesso à web do Nginx.

O Keepalived é um software de alta disponibilidade baseado em VRRP que pode ser usado para criar um cluster principal/secundário de alta disponibilidade entre CVMs baseados no VPC. Para usar o Keepalived, primeiro conclua sua configuração no arquivo `keepalived.conf`.
![](https://main.qcloudimg.com/raw/28815d732550f9eebb66e8d81cea22fd.png)
- Em redes físicas tradicionais, o status principal/secundário pode ser negociado com o protocolo VRRP do Keepalived. O dispositivo principal envia mensagens ARP gratuitas periodicamente para limpar a tabela MAC ou a tabela ARP do terminal da troca de uplink, a fim de acionar a migração do VIP para o dispositivo principal.
- Em um VPC do Tencent Cloud, um cluster principal/secundário de alta disponibilidade também pode ser implementado ao implantar o Keepalived em CVMs, com as seguintes diferenças:
   - O VIP deve ser um [HAVIP](https://intl.cloud.tencent.com/document/product/215/31817) solicitado do Tencent Cloud.
   - O HAVIP é sensível à sub-rede e só pode ser vinculado a um servidor na mesma sub-rede por meio de anúncio.

## Observações
+ Recomendamos comunicações VRRP em modo unicast.
+ Recomendamos que você use o Keepalived **1.2.24 ou versões posteriores**.
+ Certifique-se de que os parâmetros `garp` foram configurados. Como o Keepalived depende de mensagens ARP para atualizar o endereço IP, essas configurações garantem que o dispositivo principal sempre envie mensagens ARP para a comunicação.
   ```plaintext
  garp_master_delay 1
  garp_master_refresh 5
  ```
+ Configure um ID de roteador VRRP exclusivo para cada cluster principal/secundário no VPC.
+ Não use o modo strict (estrito). Certifique-se de que as configurações “vrrp_strict” foram excluídas.
+ Controle a quantidade de HAVIPs vinculados a um único ENI para não ser mais do que cinco. Se você precisar usar vários VIPs, adicione ou modifique `vrrp_garp_master_repeat 1` na seção “global_defs” do arquivo de configuração do Keepalived.

## Instruções

>!
>Este documento usa os seguintes ambientes como exemplo. Substitua por suas configurações reais.
>+ CVM principal: HAVIP-01, 172.16.16.5
>+ CVM secundário: HAVIP-02, 172.16.16.6
>+ HAVIP: 172.16.16.12
>+ EIP: 81.71.14.118
>+ Imagem: CentOS 7.6 64 bits
>

<span id="step1"></span>
### Etapa 1: solicite um VIP
1. Faça login no [console do VPC](https://console.cloud.tencent.com/vpc/).
2. Selecione **IP and ENI (IP e ENI)** > **HAVIP** na barra lateral esquerda para acessar a página de gerenciamento do HAVIP. 
3. Selecione a região relevante na página de gerenciamento do HAVIP e clique em **Apply (Solicitar)**.
4. Na caixa de diálogo pop-up, digite o nome, selecione um VPC e uma sub-rede para o HAVIP e clique em **OK**.
>?O endereço IP do HAVIP pode ser atribuído automaticamente ou especificado manualmente. Se você optar por inserir um endereço IP, certifique-se de que o endereço IP privado inserido está dentro do intervalo de IP da sub-rede e não é um endereço IP reservado do sistema. Por exemplo, se o intervalo de IP da sub-rede for `10.0.0.0/24`, o endereço IP privado inserido deve estar dentro de `10.0.0.2 - 10.0.0.254`.
>
![](https://main.qcloudimg.com/raw/fc0224eda94238588f0dfc0178d08b77.png)
Depois disso, você pode exibir o HAVIP solicitado.
![](https://main.qcloudimg.com/raw/3cdee897dc6a5b69ff45ad47725444d9.png)

### Etapa 2: instale o Keepalived (versão 1.2.24 ou posterior) nos CVMs principal e secundário
Este documento usa CentOS 7.6 como exemplo para instalar o Keepalived. Se você precisar de outra imagem, entre em contato com nossa equipe de suporte técnico.
1. Execute o seguinte comando para verificar se a versão do Keepalived atende aos requisitos.
   ```plaintext
   yum list keepalived
   ```
 + Se sim, prossiga para a [Etapa 2](#substep2)
 + Caso contrário, prossiga para a [Etapa 3](#substep3)
2. <span id="substep2">Instale o pacote de software usando o comando `yum`.

   ```plaintext
   yum install -y keepalived
   ```

3. <span id="substep3">Instale o pacote de software usando o código-fonte.

   ```plaintext
   tar zxvf keepalived-1.2.24.tar.gz
   cd keepalived-1.2.24
   ./configure --prefix=/
   make; make install
   chmod +x /etc/init.d/keepalived   // Evite a ocorrência de env: /etc/init.d/keepalived: Permission denied
   ```

### Etapa 3: configure o Keepalived e vincule o HAVIP aos CVMs principal e secundário.
1. Faça login no HAVIP-01 do CVM principal e execute `vim /etc/keepalived/keepalived.conf` para modificar suas configurações.

   ```plaintext
   ! Configuration File for keepalived
   global_defs {
      notification_email {
        acassen@firewall.loc
        failover@firewall.loc
        sysadmin@firewall.loc
      }
      notification_email_from Alexandre.Cassen@firewall.loc
      smtp_server 192.168.200.1   
      smtp_connect_timeout 30
      router_id LVS_DEVEL
      vrrp_skip_check_adv_addr
      vrrp_garp_interval 0
      vrrp_gna_interval 0
   }
   vrrp_script checkhaproxy
   {
       script "/etc/keepalived/do_sth.sh"
        interval 5
   }
   vrrp_instance VI_1 {
   # Selecione os parâmetros adequados para os servidores mestre e escravo.
   state BACKUP                #Defina o status inicial como `Backup`
       interface eth0          #O ENI (tais como `eth0`) usado para vincular um VIP  
       virtual_router_id 51        #O valor `virtual_router_id` para o cluster
       nopreempt                   #Modo Non-preempt
       preempt_delay 10
       priority 100               #Prioridade. Quanto maior o valor, maior a prioridade
       advert_int 1        
       authentication {
           auth_type PASS
           auth_pass 1111
       }
       unicast_src_ip 172.16.16.5 #Endereço IP privado do dispositivo local
       unicast_peer {
           172.16.16.6                #Endereço IP do dispositivo de par
       }
       virtual_ipaddress {
           172.16.16.12              #HAVIP 
       }
       notify_master "/etc/keepalived/notify_action.sh MASTER"
       notify_backup "/etc/keepalived/notify_action.sh BACKUP"
       notify_fault "/etc/keepalived/notify_action.sh FAULT"
       notify_stop "/etc/keepalived/notify_action.sh STOP"
       garp_master_delay 1    # Quanto tempo levará para que o cache de ARP possa ser atualizado após o CVM mudar para o status principal
       garp_master_refresh 5   #Intervalo de tempo entre o qual o nó principal envia mensagens ARP
   
       track_interface {
                   eth0               # ENI (tais omo `eth0`) que vincula um VIP
           }
       track_script {
          checkhaproxy 
       }
   }
   ```

2. Pressione **Esc** para sair do modo de edição e digite **:wq!** para salvar e fechar o arquivo.

3. Faça login no HAVIP-02 do CVM secundário e execute `vim /etc/keepalived/keepalived.conf` para modificar suas configurações.

   ```plaintext
   ! Configuration File for keepalived
   global_defs {
      notification_email {
        acassen@firewall.loc
        failover@firewall.loc
        sysadmin@firewall.loc
      }
      notification_email_from Alexandre.Cassen@firewall.loc
      smtp_server 192.168.200.1
      smtp_connect_timeout 30
      router_id LVS_DEVEL
      vrrp_skip_check_adv_addr
      vrrp_garp_interval 0
      vrrp_gna_interval 0
   }
   vrrp_script checkhaproxy
   {
       script "/etc/keepalived/do_sth.sh"
        interval 5
   }
   vrrp_instance VI_1 {
   # Selecione os parâmetros adequados para os servidores mestre e escravo.
   state BACKUP                #Defina o status inicial como `Backup`
       interface eth0          #O ENI (tais como `eth0`) usado para vincular um VIP  
       virtual_router_id 51        #O valor `virtual_router_id` para o cluster
       nopreempt                   #Modo Non-preempt
       preempt_delay 10
       priority 50               #Prioridade. Quanto maior o valor, maior a prioridade
       advert_int 1        
       authentication {
           auth_type PASS
           auth_pass 1111
       }
       unicast_src_ip 172.16.16.6 #IP privado do dispositivo local
       unicast_peer {
           172.16.16.5                #Endereço IP do dispositivo de par
       }
       virtual_ipaddress {
           172.16.16.12              #HAVIP 
       }
       notify_master "/etc/keepalived/notify_action.sh MASTER"
       notify_backup "/etc/keepalived/notify_action.sh BACKUP"
       notify_fault "/etc/keepalived/notify_action.sh FAULT"
       notify_stop "/etc/keepalived/notify_action.sh STOP"
       garp_master_delay 1    # Quanto tempo levará para que o cache de ARP possa ser atualizado após o CVM mudar para o status principal
       garp_master_refresh 5   #Intervalo de tempo entre o qual o nó principal envia mensagens ARP
   
       track_interface {
                   eth0               # ENI (tais omo `eth0`) que vincula um VIP
           }
       track_script {
          checkhaproxy 
       }
   }
   ```

4. Pressione **Esc** para sair do modo de edição e digite **:wq!** para salvar e fechar o arquivo.

5. Reinicie o Keepalived para que a configuração tenha efeito.

   ```plaintext
   systemctl start keepalived
   ```

6. Verifique o status principal/secundário dos dois CVMs e confirme se ambos têm o HAVIP vinculado corretamente.
>?Neste exemplo, o HAVIP-01 tem uma prioridade mais alta e normalmente servirá como o nó principal.
>
Faça login no console do [HAVIP](https://console.cloud.tencent.com/vpc/havip). Você verá que o HAVIP está vinculado ao HAVIP-01 do CVM principal, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/1104e6a7305dec04ce1ea242db0c2c8c.png)

### Etapa 4: **vincule um EIP ao HAVIP (opcional)**  

1. Faça login no console do [HAVIP](https://console.cloud.tencent.com/vpc/havip), localize o HAVIP solicitado na [Etapa 1](#step1) e clique em **Bind (Vincular)**.
![](https://main.qcloudimg.com/raw/129cd10051b4d07e1d420b1bec710614.png)
2. Na caixa de diálogo pop-up, selecione o EIP a ser vinculado e clique em **OK**. Se nenhum EIP estiver disponível, acesse primeiro o console do [EIP](https://console.cloud.tencent.com/cvm/eip?rid=46) para solicitar.
![](https://main.qcloudimg.com/raw/8ca21593889529f42af52c5b68ec2f78.png)

### Etapa 5: use notify_action.sh para registro em log simples (opcional)
Os logs principais do Keepalived ainda são registrados em “/var/log/message”, e você pode adicionar o script “notify” para registro em log simples.

1. Faça login no CVM e execute o comando `vim /etc/keepalived/notify_action.sh` para adicionar o seguinte script “notify_action.sh”.

   ```plaintext
   #!/bin/bash
   #/etc/keepalived/notify_action.sh
   log_file=/var/log/keepalived.log
   log_write()
   {
       echo "[`date '+%Y-%m-%d %T'`] $1" >$log_file
   }
   
   [ ! -d /var/keepalived/ ] && mkdir -p /var/keepalived/
   
   case "$1" in
       "MASTER" )
           echo -n "$1" /var/keepalived/state
           log_write " notify_master"
           echo -n "0" /var/keepalived/vip_check_failed_count
           ;;
   
       "BACKUP" )
           echo -n "$1" /var/keepalived/state
           log_write " notify_backup"
           ;;
   
       "FAULT" )
           echo -n "$1" /var/keepalived/state
           log_write " notify_fault"
           ;;
   
       "STOP" )
           echo -n "$1" /var/keepalived/state
           log_write " notify_stop"
           ;;
       *)
           log_write "notify_action.sh: STATE ERROR!!!"
           ;;
   esac
   ```

2. Execute o comando `chmod a+x /etc/keepalived/notify_action.sh` para modificar a permissão do script.

### Etapa 6: verifique se o VIP e o IP público são alternados normalmente durante a alternância principal/secundária

Simule a falha do CVM reiniciando o processo do Keepalived ou reiniciando o CVM para verificar se o VIP pode ser migrado.

- Se a alternância principal/secundária tiver êxito, o CVM secundário se tornará o servidor vinculado ao HAVIP no console.
- Você também pode executar ping em um VIP de dentro do VPC para verificar o lapso de tempo desde a interrupção da rede até a recuperação. Cada alternância pode causar uma interrupção por cerca de 4 segundos. Se você executar ping no EIP vinculado ao HAVIP em uma rede pública, o resultado será o mesmo.
