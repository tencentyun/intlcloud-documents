## Visão geral
Gargalo de largura de banda e tempo de propagação de ida e volta (BBR) é um algoritmo de controle de congestionamento de TCP desenvolvido pelo Google em 2016. Ele ajuda a melhorar significativamente o rendimento e a latência de conexão TCP dos servidores Linux. No entanto, a ativação do BBR requer uma versão 4.10 ou posterior do kernel Linux. Se você usa uma versão anterior, precisará atualizar seu kernel. Este documento o orienta sobre como alterar manualmente o kernel e habilitar o BBR em seu servidor Linux.

## Instruções

### Atualização do pacote kernel
1. Execute o seguinte comando para verificar a versão atual do kernel.
```
uname -r
```
2. Execute o seguinte comando para atualizar o pacote de software.
```
yum update -y
```
3. Execute o seguinte comando para importar a chave pública de ELRepo.
```
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
```
4. Execute o seguinte comando para instalar o repositório yum do ELRepo.
```
yum install https://www.elrepo.org/elrepo-release-7.0-4.el7.elrepo.noarch.rpm
```


### Instalação de um novo kernel
1. Execute o seguinte comando para verificar o pacote kernel compatível no repositório ELRepo.
```
yum --disablerepo="*" --enablerepo="elrepo-kernel" list available
```
2. Execute o seguinte comando para instalar o kernel estável da linha principal mais recente.
```
yum --enablerepo=elrepo-kernel install kernel-ml
```

### Modificação da configuração do grub
1. Execute o seguinte comando para abrir o arquivo `/etc/default/grub`.
```
vim /etc/default/grub
```
2. Pressione **i** para alternar para o modo de edição e altere `GRUB_DEFAULT=saved` para `GRUB_DEFAULT=0`.
![](https://main.qcloudimg.com/raw/484e7a6e818dc44c2d4debb9230e0b46.png)
3. Pressione **Esc** e digite **:wq** para salvar e fechar o arquivo.
4. Execute o seguinte comando para gerar a configuração do kernel novamente.
```
grub2-mkconfig -o /boot/grub2/grub.cfg
```
5. Execute o seguinte comando para reiniciar o servidor.
```
reboot
```
6. Execute o seguinte comando para verificar se a modificação foi bem-sucedida.
```
uname -r
```

### Exclusão de kernels desnecessários
1. Execute o seguinte comando para visualizar todos os kernels.
```
rpm -qa | grep kernel
```
2. Execute o seguinte comando para excluir o kernel antigo.
```
yum remove kernel-old_kernel_version
```
Por exemplo:
```
yum remove kernel-3.10.0-957.el7.x86_64
```

### Habilitação do BBR
1. Execute o seguinte comando para editar o arquivo `/ etc / sysctl.conf`.
```
vim /etc/sysctl.conf
```
2. Pressione **i** para alternar para o modo de edição e digite o seguinte:
```
net.core.default_qdisc=fq
net.ipv4.tcp_congestion_control=bbr
```
3. Pressione **Esc** e digite **:wq** para salvar e fechar o arquivo.
4. Execute o seguinte comando para carregar as configurações dos parâmetros do kernel no arquivo de configuração `/etc/sysctl.conf`.
```
sysctl -p
```
5. Execute os comandos a seguir para verificar se o BBR foi ativado com êxito.
```
sysctl net.ipv4.tcp_congestion_control
# O seguinte será exibido se a configuração for bem-sucedida:
# net.ipv4.tcp_congestion_control = bbr
```
```
sysctl net.ipv4.tcp_available_congestion_control
# O seguinte será exibido se a configuração for bem-sucedida:
# net.ipv4.tcp_available_congestion_control = reno cubic bbr
```
6. Execute o comando a seguir para verificar se o módulo do kernel está carregado.
```
lsmod | grep bbr
```
Se as informações a seguir forem retornadas, o BBR foi ativado com êxito.
![](https://main.qcloudimg.com/raw/7d736afd8ce22f421315e149a86527e5.png)



