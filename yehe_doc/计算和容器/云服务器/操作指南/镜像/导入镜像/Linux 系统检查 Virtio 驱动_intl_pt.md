## Introdução
Para ser executado no Tencent Cloud, um CVM deve ter um kernel que seja compatível com os drivers virtio, incluindo o driver de dispositivo de bloco `virtio_blk` e o driver NIC `virtio_net`. Para garantir que um CVM criado com uma imagem personalizada possa inicializar corretamente, verifique se a sua imagem é compatível com os drivers virtio no servidor de origem antes de importar a imagem. Este documento usa o CentOS como exemplo para descrever como verificar se uma imagem é compatível com os drivers virtio.

## Instruções

<span id="CheckVirtioForKernel"></span>
### Etapa 1: verificar se o kernel é compatível com os drivers virtio
Execute o seguinte comando para verificar se o kernel atual é compatível com os drivers virtio:
```
grep -i virtio /boot/config-$(uname -r)
```
Uma resposta semelhante à seguinte será retornada:
![](https://main.qcloudimg.com/raw/8c32c3dd554700a0c17ff0c7e5675090.png)
 - Se o valor de `CONFIG_VIRTIO_BLK` e `CONFIG_VIRTIO_NET` for `m` na resposta, vá para a [Etapa 2](#CheckVirtioForInitramfs).
 - Se o valor de `CONFIG_VIRTIO_BLK` e `CONFIG_VIRTIO_NET` for `y` na resposta, o que significa que o sistema operacional contém os drivers virtio, é possível importar a imagem personalizada para o Tencent Cloud. Para obter detalhes, consulte [Importação de imagens > Visão geral](https://intl.cloud.tencent.com/document/product/213/4945).
 - Se você não conseguir encontrar `CONFIG_VIRTIO_BLK` e `CONFIG_VIRTIO_NET` na resposta, isso significa que as imagens com o sistema operacional **não podem** ser importadas para o Tencent Cloud. [Baixe e compile o kernel](#DownloadCompileKernel).

<span id="CheckVirtioForInitramfs"></span>
### Etapa 2: verificar se os drivers virtio estão no sistema de arquivos temporários
Se o valor dos parâmetros for `m` na [Etapa 1](#CheckVirtioForKernel), é necessário verificar se `initramfs` ou `initrd` contém os drivers `virtio`. Execute o comando correspondente de acordo com o sistema operacional:
- Para CentOS 6/CentOS 7/CentOS 8/RedHat 6/RedHat 7:
```
lsinitrd /boot/initramfs-$(uname -r).img | grep virtio
```
- Para RedHat 5/CentOS 5:
```
mkdir -p /tmp/initrd && cd /tmp/initrd
zcat /boot/initrd-$(uname -r).img | cpio -idmv
find . -name "virtio*"
```
- Para Debian/Ubuntu:
```
lsinitramfs /boot/initrd.img-$(uname -r) | grep virtio
```

Se um resultado semelhante ao seguinte for retornado:
<img src="https://main.qcloudimg.com/raw/a5e22f75f48ce26a6b03f65588a52877.png" />
Isso significa que o <code>initramfs</code> contém o driver <code>virtio_blk</code> e <code>virtio.ko</code>, <code>virtio_pci.ko</code> e <code>virtio_ring.ko</code> dos quais o driver depende. Nesse caso, é possível importar a imagem personalizada para o Tencent Cloud. Para obter detalhes, consulte <a href="https://intl.cloud.tencent.com/document/product/213/4945">Importação de imagens > Visão geral</a>.
Se o <code>initramfs</code> ou o <code>initrd</code> não contiver os drivers <code>virtio</code>, vá para a [Etapa 3](#ReconfigureInitramfs).

<span id="ReconfigureInitramfs"></span>
### Etapa 3: reconfigurar o sistema de arquivos temporários
Se você descobrir que o `initramfs` ou o `initrd` não contém os drivers `virtio` na [Etapa 2](#CheckVirtioForInitramfs), será necessário reconfigurar o sistema de arquivos temporários para garantir que o `initramfs` ou o `initrd` contém os drivers `virtio`. Execute o comando correspondente de acordo com o sistema operacional:
 - Para CentOS 6/CentOS 7/RedHat 6/RedHat 7:
```
cp /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r).img.bak
mkinitrd -f --with=virtio_blk --with=virtio_pci /boot/initramfs-$(uname -r).img $(uname -r)
```
 - Para RedHat 5/CentOS 5:
```
cp /boot/initrd-$(uname -r).img /boot/initrd-$(uname -r).img.bak
mkinitrd -f --with=virtio_blk --with=virtio_pci /boot/initrd-$(uname -r).img $(uname -r)
```
 - Para Debian/Ubuntu:
```
echo -e "virtio_pci\nvirtio_blk" >> /etc/initramfs-tools/modules
update-initramfs  -u
```

## Apêndice
<span id="DownloadCompileKernel"></span>
### Download e compilação do kernel

#### Download do pacote de instalação do kernel
1. Execute o seguinte comando para instalar os componentes necessários para a compilação do kernel.
```
yum install -y ncurses-devel gcc make wget
```
2. Execute o seguinte comando para visualizar a versão atual do kernel.
```
uname -r
```
Uma resposta semelhante à seguinte será retornada, indicando que a versão atual do kernel é 2.6.32-642.6.2.el6.x86_64.
![](https://main.qcloudimg.com/raw/739b19fc7af96d6de7872df0a498b7b6.png)
2. Vá para [página de download do kernel do Linux](https://www.kernel.org/pub/linux/kernel/?spm=a2c4g.11186623.2.26.7e4179b4zo5WVJ) para baixar o código-fonte da versão do kernel correspondente.
Por exemplo, para a versão `2.6.32-642.6.2.el6.x86_64`, é preciso baixar o `linux-2.6.32.tar.gz` em `https://mirrors.edge.kernel.org/pub/linux/kernel/v2.6/linux-2.6.32.tar.gz`.
4. Execute o seguinte comando para alternar o diretório.
```
cd /usr/src/
```
5. Execute o seguinte comando para baixar o pacote de instalação.
```
wget https://mirrors.edge.kernel.org/pub/linux/kernel/v2.6/linux-2.6.32.tar.gz
```
6. Execute o seguinte comando para descompactar o pacote de instalação.
```
tar -xzf linux-2.6.32.tar.gz
```
7. Execute o seguinte comando para fazer a conexão.
```
ln -s linux-2.6.32 linux
```
8. Execute o seguinte comando para alternar o diretório.
```
cd /usr/src/linux
```

#### Compilação do kernel

1. Execute os seguintes comandos para compilar o kernel.
```
make mrproper
cp /boot/config-$(uname -r) ./.config
make menuconfig
```
Entre na interface “Linux Kernel vX.X.XX Configuration”, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/72c3bea10627aaef022f1a72b72ac79a.png)
>? Se você não for direcionado para a interface "Linux Kernel vX.X.XX Configuration", vá para a [Etapa 18](#OptionalStep).
> Interface “Linux Kernel vX.X.XX Configuration”:
> - Pressione “Tab” ou “↑” “↓” para mover o cursor.
> - Pressione “Enter” para selecionar ou executar o item selecionado pelo cursor.
> - Pressione a barra de espaço para selecionar o item selecionado pelo cursor. “\*” significa compilar para o kernel e "M" significa compilar para um módulo. 
> 
2. Pressione a tecla "↓" para mover o cursor para "Virtualization (Virtualização)" e pressione a barra de espaço para selecionar "Virtualization (Virtualização)".
3. Pressione "Enter" para entrar na interface de detalhes de virtualização.
4. Na interface de detalhes de virtualização, verifique se a opção Kernel-based Virtual Machine (KVM) support (Suporte para máquina virtual baseada em kernel (KVM)) está selecionada conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/d5614d31ebaed0f0b270dc1046b9ff2e.png)
Se não estiver selecionada, pressione a barra de espaço para selecionar essa opção.
5. Pressione "Esc" para retornar à interface principal "Linux Kernel vX.X.XX Configuration".
6. Pressione a tecla "↓" para mover o cursor para "Processor type and features (Tipo e funcionalidades do processador)" e pressione "Enter" para entrar nessa interface de detalhes.
7. Pressione a tecla "↓" para mover o cursor para "Paravirtualized guest support (Compatibilidade para convidados paravirtualizados)" e pressione "Enter" para entrar nessa interface de detalhes.
8. Na interface de detalhes acima, verifique se as opções "KVM paravirtualized clock (Relógio paravirtualizado do KVM)" e "KVM Guest support (Compatibilidade para convidado do KVM)" estão selecionadas conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/2e49f9b46ecb9f9d272db36dffbade07.png)
Se elas não estiverem selecionadas, pressione a barra de espaço para selecioná-las.
9. Pressione "Esc" para retornar à interface principal "Linux Kernel vX.X.XX Configuration".
10. Pressione a tecla "↓" para mover o cursor para "Device Drivers (Drivers do dispositivo)" e pressione "Enter" para entrar nessa interface de detalhes.
11. Pressione a tecla "↓" para mover o cursor para "Block devices (Dispositivos de bloco)" e pressione "Enter" para entrar nessa interface de detalhes.
12. Na interface de detalhes acima, verifique se a opção "Virtio block driver (EXPERIMENTAL) (Driver de bloco Virtio (EXPERIMENTAL))" está selecionada como mostrado abaixo:
![](https://main.qcloudimg.com/raw/79f3e29a6d77224a164c6c716e41fa84.png)
Se não estiver selecionada, pressione a barra de espaço para selecionar essa opção.
13. Pressione “Esc” para retornar à interface de detalhes Device Drivers (Drivers do dispositivo).
14. Pressione a tecla "↓" para mover o cursor para "Network device support (Compatibilidade com dispositivos de rede)" e pressione "Enter" para entrar nessa interface de detalhes.
15. Na interface de detalhes acima, verifique se a opção "Virtio network driver (EXPERIMENTAL) (Driver de rede Virtio (EXPERIMENTAL))" está selecionada como mostrado abaixo:
![](https://main.qcloudimg.com/raw/811388c89393882ea83bceb7a00bc1b7.png)
Se não estiver selecionada, pressione a barra de espaço para selecionar essa opção.
16. Pressione "Esc" para sair da interface de configuração do kernel e selecione "YES (SIM)" para salvar o arquivo `.config`.
17. Realize a [Etapa 1: verificar se o kernel é compatível com os drivers virtio](#CheckVirtioForKernel) para verificar se os drivers virtio foram configurados corretamente.
18. <span id = "OptionalStep"></span> (Opcional) Execute o seguinte comando para editar manualmente o arquivo `.config`.
>? Essa etapa é recomendada se qualquer um dos dois cenários for verdadeiro:
> - O kernel ainda não contém as informações de configuração relacionadas aos drivers virtio após o término da verificação.
> - Ao compilar o kernel, não é possível entrar na interface de configuração do kernel ou salvar o arquivo `.config`.
> 
```
make oldconfig
make prepare
make scripts
make
make install
```
19. Execute os seguintes comandos para verificar a instalação dos drivers virtio.
```
find /lib/modules/"$(uname -r)"/ -name "virtio.*" | grep -E "virtio.*"
grep -E "virtio.*" < /lib/modules/"$(uname -r)"/modules.builtin
```
Se algum dos comandos retornar uma lista de arquivos como `virtio_blk`, `virtio_pci.virtio_console`, isso indica que os drivers virtio foram instalados corretamente.





