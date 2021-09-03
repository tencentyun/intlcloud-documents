> Desde 6 de dezembro de 2019, o Tencent Cloud não provê mais suporte à configuração de gateway da rede pública ao adquirir um CVM. Se for necessário configurar um gateway, siga estas instruções.
>

## Cenário

Se alguns dos seus CVMs no Tencent Cloud VPC não tiverem endereços IP públicos comuns, mas precisarem acessar a internet, é possível usar um CVM com um IP público (IP público comum ou elástico) como o gateway público para permitir o acesso à internet. O CVM de gateway público converte o IP de origem do tráfego de saída. Quando qualquer outro CVM acessa a internet pelo CVM de gateway público, ele converte seus IPs para o IP público dele, conforme mostrado na figura abaixo.
![](https://main.qcloudimg.com/raw/4879fa2798946972e8496c13a1bfa3cc.png)
## Pré-requisitos
- Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
- O CVM de gateway público e os CVMs que precisam acessar a internet por ele estão localizados em sub-redes diferentes porque o CVM de gateway público só consegue encaminhar solicitações de roteamento de outras sub-redes.
- O CVM de gateway público deve ser do Linux. Um CVM do Windows não pode servir como um gateway público.

## Instruções
### Etapa 1: Vincule um IP público elástico (opcional)
>Se o CVM que serve como gateway público já tiver um endereço IP público, ignore essa etapa.

1. No painel de navegação à esquerda, clique em **[EIP](https://console.cloud.tencent.com/cvm/eip)** para acessar a página de gerenciamento de EIPs.
2. Localize o IP público elástico de destino e selecione **More (Mais)** > **Bind (Vincular)** na coluna **Operation (Operação)** para abrir a janela **Bind resources (Vincular recursos)**.
![](https://main.qcloudimg.com/raw/c9e46426e64fd6de3d4a2a9dccb91822.png)
3. Selecione uma instância do CVM para servir como gateway público e vincule-a ao IP público elástico.
![](https://main.qcloudimg.com/raw/1642880850b505fa57a598d10247edbc.png)

### Etapa 2: Configure uma tabela de roteamento para a sub-rede do gateway
A sub-rede do gateway e outras sub-redes não podem usar a mesma tabela de rotas. É necessário criar uma tabela de rotas separada para a sub-rede do gateway.
1. Crie uma tabela de rotas personalizada
2. Associe a tabela de rotas com a sub-rede onde o CVM de gateway público está localizado, conforme solicitado.
![](https://main.qcloudimg.com/raw/4f804600a0d2120a959e722daf21fa59.png)

### Etapa 3: Configure uma tabela de rotas para as outras sub-redes
Essa tabela de rotas direciona todo o tráfego dos CVMs sem um IP público para o gateway, para que eles também possam acessar as redes públicas.
Na tabela de rotas da sub-rede comum, adicione a seguinte política de roteamento:
- Destination (Destino): IP público a ser acessado.
- Next-hop type (Tipo de próximo salto): CVM.
- Next hop (Próximo salto): IP privado da instância do CVM ao qual o IP público elástico foi vinculado na Etapa 1.
![](https://main.qcloudimg.com/raw/68e072841dc6d528fe2ff269e5a982a5.png)

### Etapa 4: Configure o gateway público
1. Faça login no CVM de gateway público, habilite o encaminhamento de rede e o proxy NAT e otimize os parâmetros relacionados.
 1. Execute o seguinte comando para criar um arquivo chamado `vpcGateway.sh` em `usr/local/sbin`.
	```
	vim /usr/local/sbin/vpcGateway.sh
	```
 2. Pressione **i** para entrar no modo de edição e adicione o seguinte código no script:
		```
	#!/bin/bash
	echo "----------------------------------------------------"
	echo "          `date`"

	echo "(1)ip_forward config......"
	file="/etc/sysctl.conf"
	grep -i "^net\.ipv4\.ip_forward.*" $file &>/dev/null && sed -i \
	's/net\.ipv4\.ip_forward.*/net\.ipv4\.ip_forward = 1/' $file || \
	echo "net.ipv4.ip_forward = 1"  >> $file
	echo 1 >/proc/sys/net/ipv4/ip_forward 
	[ `cat /proc/sys/net/ipv4/ip_forward` -eq 1 ] && echo "-->ip_forward:Success" || \
	echo "-->ip_forward:Fail"

	echo "(2)Iptables set......"
	iptables -t nat -A POSTROUTING -j MASQUERADE && echo "-->nat:Success" || echo "-->nat:Fail"
	iptables -t mangle -A POSTROUTING -p tcp -j TCPOPTSTRIP --strip-options timestamp && \
	echo "-->mangle:Success" || echo "-->mangle:Fail"

	echo "(3)nf_conntrack config......"
	echo 262144 >  /sys/module/nf_conntrack/parameters/hashsize
	[ `cat /sys/module/nf_conntrack/parameters/hashsize` -eq 262144 ] && \
	echo "-->hashsize:Success" ||  echo "-->hashsize:Fail"

	echo 1048576 > /proc/sys/net/netfilter/nf_conntrack_max
	[ `cat /proc/sys/net/netfilter/nf_conntrack_max` -eq 1048576 ] && \
	echo  "-->nf_conntrack_max:Success" ||  echo  "-->nf_conntrack_max:Fail"

	echo 10800 >/proc/sys/net/netfilter/nf_conntrack_tcp_timeout_established \
	[ `cat /proc/sys/net/netfilter/nf_conntrack_tcp_timeout_established` -eq 10800 ] \
	 && echo  "-->nf_conntrack_tcp_timeout_established:Success" ||  \
	 echo  "-->nf_conntrack_tcp_timeout_established:Fail"
	```
 3. Pressione **Esc** para sair do modo de edição e digite **:wq** para salvar o arquivo e voltar. Depois, execute os seguintes comandos:
		```
		chmod +x /usr/local/sbin/vpcGateway.sh
		echo "/usr/local/sbin/vpcGateway.sh  >/tmp/vpcGateway.log 2>&1" >> /etc/rc.local
		```

2. Defina o RPS do gateway público.

 1. Execute o seguinte comando para criar um arquivo chamado `setrps.sh` em `usr/local/sbin`.
	```
	vim /usr/local/sbin/set_rps.sh
	```
 2. Pressione **i** para entrar no modo de edição e adicione o seguinte código no script:
	```
	#!/bin/bash
	echo "--------------------------------------------"
	* date
	mask=0
	i=0
	total_nic_queues=0
	
	get_all_mask() {
			local cpu_nums=$1
			if [ $cpu_nums -gt 32 ]; then
					mask_tail=""
					mask_low32="ffffffff"
					idx=$((cpu_nums / 32))
					cpu_reset=$((cpu_nums - idx * 32))

					if [ $cpu_reset -eq 0 ]; then
							mask=$mask_low32
							for ((i = 2; i <= idx; i++)); do
									mask="$mask,$mask_low32"
							done
					else
						for ((i = 1; i <= idx; i++)); do
							mask_tail="$mask_tail,$mask_low32"
					done
					mask_head_num=$((2 ** cpu_reset - 1))
					mask=$(printf "%x%s" $mask_head_num $mask_tail)
				fi
			else
				mask_num=$((2 ** cpu_nums - 1))
				mask=$(printf "%x" $mask_num)
			fi
			echo $mask
}
set_rps() {
		  if ! command -v ethtool &>/dev/null; then
			source /etc/profile
		  fi
			
		  ethtool=$(which ethtool)
			
		  cpu_nums=$(cat /proc/cpuinfo | grep processor | wc -l)
		  if [ $cpu_nums -eq 0 ]; then
			  exit 0
		  fi
			
		  mask=$(get_all_mask $cpu_nums)
		  echo "cpu number:$cpu_nums  mask:0x$mask"
			
		  ethSet=$(ls -d /sys/class/net/eth*)
			
		  for entry in $ethSet; do
			  eth=$(basename $entry)
			  nic_queues=$(ls -l /sys/class/net/$eth/queues/ | grep rx- | wc -l)
			  if (($nic_queues == 0)); then
				  continue
			  fi
				
			  cat /proc/interrupts | grep "LiquidIO.*rxtx" &>/dev/null
			  if [ $? -ne 0 ]; then # not smartnic
				  #multi queue don't set rps
				  max_combined=$(
					  $ethtool -l $eth 2>/dev/null | grep -i "combined" | head -n 1 | awk '{print $2}'
				  )
				  #if ethtool -l $eth goes wrong.
				  [[ ! "$max_combined" =~ ^[0-9]+$ ]] && max_combined=1
				  if [ ${max_combined} -ge ${cpu_nums} ]; then
					  echo "$eth has equally nic queue as cpu, don't set rps for it..."
					  continue
				  fi
			  else
				 echo "$eth is smartnic, set rps for it..."
			  fi
				
			  echo "eth:$eth  queues:$nic_queues"
			  total_nic_queues=$(($total_nic_queues + $nic_queues))
			  i=0
			  while (($i < $nic_queues)); do
				  echo $mask >/sys/class/net/$eth/queues/rx-$i/rps_cpus
				  echo 4096 >/sys/class/net/$eth/queues/rx-$i/rps_flow_cnt
					i=$(($i + 1))
			 done
		  done
			
		  flow_entries=$((total_nic_queues * 4096))
		  echo "total_nic_queues:$total_nic_queues  flow_entries:$flow_entries"
		  echo $flow_entries >/proc/sys/net/core/rps_sock_flow_entries
	}
	set_rps
	```
 3. Pressione **Esc** para sair do modo de edição e digite **:wq** para salvar o arquivo e voltar. Depois, execute os seguintes comandos:
	```
	chmod +x /usr/local/sbin/set_rps.sh
	echo "/usr/local/sbin/set_rps.sh >/tmp/setRps.log 2>&1" >> /etc/rc.local
	```
	
3. Reinicialize o CVM de gateway para aplicar as configurações. Depois, teste se um CVM que não possui IP público consegue acessar a internet pelo CVM de gateway público.
