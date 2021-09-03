## Cenário
Se você não conseguir [instalar o cloudinit](https://intl.cloud.tencent.com/document/product/213/12587) na sua imagem do Linux, use a **Forced Image Import (Importação forçada de imagem)** para importar a imagem. Se você usar essa imagem para importação, que não tem o cloudinit instalado, o Tencent Cloud não consegue inicializar seu CVM. Nesse caso, é necessário configurar o script por conta própria, a fim de configurar o CVM com base no arquivo de configuração fornecido pelo Tencent Cloud. Este documento descreve como configurar o CVM no caso da importação forçada da imagem.

O Tencent Cloud fornece ao usuário um dispositivo de CDROM contendo as informações de configuração. O usuário precisa montar o CDROM e ler as informações de `mount_point/qcloud_action/os.conf` para configuração. Se outros dados de configuração ou UserData precisarem ser usados, o usuário pode ler diretamente os arquivos em `mount_point/`.

## Arquivo de configuração os.conf
Veja o conteúdo do os.conf a seguir.
<pre>
hostname=VM_10_20_xxxx
password=GRSgae1fw9frsG.rfrF
eth0&#95;ip&#95;addr=10.104.62.201
eth0&#95;mac&#95;addr=52:54:00:E1:96:EB
eth0&#95;netmask=255.255.192.0
eth0&#95;gateway=10.104.0.1
dns&#95;nameserver="10.138.224.65 10.182.20.26 10.182.24.12"
</pre>
>? Os nomes dos parâmetros acima são para referência e os valores são usados apenas como exemplos.
>
Veja a descrição de cada parâmetro no arquivo de configuração os.conf:

| Nome do parâmetro | Descrição |
|----------|----------|
| hostname | Nome do CVM |
| password | Senha criptografada |
| eth0_ip_addr | IP da LAN do eth0 |
| eth0_mac_addr | Endereço MAC do eth0 |
| eth0_netmask | Máscara da sub-rede do eth0 |
| eth0_gateway | Gateway do eth0 |
| dns_nameserver | Servidor de resolução de DNS |


## Limites
- A imagem deve corresponder aos limites das imagens do Linux, conforme descrito em [Importação de imagens](https://intl.cloud.tencent.com/document/product/213/4945), exceto para o cloudinit.
- A partição do sistema para importar a imagem não está cheia.
- A imagem importada não contém vulnerabilidades que possam ser exploradas remotamente.
- Recomendamos que você altere a senha imediatamente após a instância ser criada com êxito no caso da importação forçada.

## Observações
Observe o seguinte ao configurar a análise de script:
- O script é executado automaticamente na inicialização. Implemente esse requisito com base em seu sistema operacional.
- Monte `/dev/cdrom` e leia o arquivo `os_action/os.conf` no ponto de montagem para obter as informações de configuração.
- A senha colocada no CDROM pelo Tencent Cloud é criptografada. Você pode definir uma nova senha com `chpasswd -e`.
**Observe que a senha criptografada pode conter caracteres especiais. Recomendamos que você coloque em um arquivo e, em seguida, defina a senha com `chpasswd -e < passwd_file`.**
- Ao usar a imagem de importação forçada para criar uma instância e, em seguida, criar uma imagem, é necessário garantir que o script ainda será executado, a fim de garantir que a instância esteja configurada corretamente. Também é possível instalar o cloudinit nessa instância.


## Instruções

>! O Tencent Cloud fornece um exemplo de script baseado no CentOS. É possível consultá-lo para criar um script para suas imagens. Durante a criação, observe que:
> - **O script deve ser colocado corretamente no sistema antes da importação da imagem**.
> - O script não é aplicável a todos os sistemas operacionais. É necessário modificá-lo de acordo com seus próprios sistemas operacionais.
> 


1. Crie um script `os_config` baseado no seguinte exemplo de script.
É possível modificar o script conforme necessário.

```
#!/bin/bash
### BEGIN INIT INFO
# Provides:          os-config
# Required-Start:    $local_fs $network $named $remote_fs
# Required-Stop:
# Should-Stop:
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: config of os-init job
# Description: run the config phase without cloud-init
### END INIT INFO
###################user settings#####################
cdrom_path=`blkid -L config-2`
load_os_config() {
	mount_path=$(mktemp -d /mnt/tmp.XXXX)
	mount /dev/cdrom $mount_path
	if [[ -f $mount_path/qcloud_action/os.conf ]]; then
		. $mount_path/qcloud_action/os.conf
		if [[ -n $password ]]; then
			passwd_file=$(mktemp /mnt/pass.XXXX)
			passwd_line=$(grep password $mount_path/qcloud_action/os.conf)
			echo root:${passwd_line#*=} > $passwd_file
		fi
		return 0
	else 
		return 1
	fi
}
cleanup() {
	umount /dev/cdrom
	if [[ -f $passwd_file ]]; then
		echo $passwd_file
		rm -f $passwd_file
	fi
	if [[ -d $mount_path ]]; then
		echo $mount_path
		rm -rf $mount_path
	fi
}
config_password() {
	if [[ -f $passwd_file ]]; then
		chpasswd -e < $passwd_file
	fi
}
config_hostname(){
	if [[ -n $hostname ]]; then
		sed -i "/^HOSTNAME=.*/d" /etc/sysconfig/network
		echo "HOSTNAME=$hostname" >> /etc/sysconfig/network
	fi
}
config_dns() {
    if [[ -n $dns_nameserver ]]; then
        dns_conf=/etc/resolv.conf
        sed -i '/^nameserver.*/d' $dns_conf
        for i in $dns_nameserver; do
            echo "nameserver $i" >> $dns_conf
        done
    fi
}
config_network() {
    /etc/init.d/network stop
    cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
DEVICE=eth0
IPADDR=$eth0_ip_addr
NETMASK=$eth0_netmask
HWADDR=$eth0_mac_addr
ONBOOT=yes
GATEWAY=$eth0_gateway
BOOTPROTO=static
EOF
    if [[ -n $hostname ]]; then
    	sed -i "/^${eth0_ip_addr}.*/d" /etc/hosts
		echo "${eth0_ip_addr} $hostname" >> /etc/hosts
	fi
    /etc/init.d/network start
}
config_gateway() {
	sed -i "s/^GATEWAY=.*/GATEWAY=$eth0_gateway" /etc/sysconfig/network
}
###################init#####################
start() {
	if load_os_config ; then
		config_password
		config_hostname
		config_dns
		config_network
		cleanup
		exit 0
	else 
		echo "mount ${cdrom_path} failed"
		exit 1
	fi
}
RETVAL=0
case "$1" in
	start)
		start
		RETVAL=$?
	;;
	*)
		echo "Usage: $0 {start}"
		RETVAL=3
	;;
esac
exit $RETVAL
```
2. Coloque o script `os_config` no diretório `/etc/init.d/` e execute o seguinte comando.
```
chmod +x /etc/init.d/os_config
chkconfig --add os_config
```
3. Execute o seguinte comando para verificar se `os_config` foi adicionado ao serviço de inicialização.
```
chkconfig --list
```
>? É necessário garantir que o script seja executado corretamente. Se você não conseguir se conectar à instância por SSH ou ocorrer uma exceção de rede após a importação da imagem, tente se conectar à instância pelo console para executar o script novamente. Se o problema persistir, entre em contato com o atendimento ao cliente.


