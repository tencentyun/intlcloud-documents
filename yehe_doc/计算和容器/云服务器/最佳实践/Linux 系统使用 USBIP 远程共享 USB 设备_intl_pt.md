## Visão geral

O [USB/IP](http://usbip.sourceforge.net/) é um projeto de código aberto e foi incorporado ao kernel. Em um ambiente Linux, você pode usar o USB/IP para compartilhar dispositivos USB remotamente. Este documento usa as seguintes versões de ambiente como exemplos para descrever como usar o USB/IP para compartilhar dispositivos USB.
Cliente USB: CVM com CentOS 7.6
Servidor USB: PC local com Debian

## Observações
O método de instalação do USB/IP e o nome do módulo do kernel variam de acordo com as versões do sistema operacional Linux. Acesse as versões oficiais do Linux e verifique se o seu sistema operacional Linux atual é compatível com o recurso USB/IP.


## Instruções

### Configuração do servidor USB

1. No PC local, execute os seguintes comandos em sequência para instalar o USB/IP e carregar módulos de kernel relacionados:
```
sudo apt-get install usbip
sudo modprobe usbip-core
sudo modprobe vhci-hcd
sudo modprobe usbip_host
```
2. Insira um dispositivo USB e execute o seguinte comando para visualizar os dispositivos USB disponíveis:
```
usbip list --local
```
Por exemplo, se uma chave USB Feitian for inserida no PC local, o seguinte resultado será retornado:
```
busid 1-1.3(096e:031b)
Feitian Technologies, Inc.: unknown product(096e:031b)
```
3. Registre o valor busid e execute os seguintes comandos em sequência para habilitar a escuta, especifique a porta USB/IP e compartilhe o dispositivo USB:
```
sudo usbipd -D [--tcp-port PORT]
sudo usbip bind -b [busid]
```
Por exemplo, se a porta USB/IP especificada for a porta 3240 (porta USB/IP padrão) e busid for `1-1.3`, execute os seguintes comandos:
```
sudo usbipd -D
sudo usbip bind -b 1-1.3
```
(Opcional) 4. Execute o seguinte comando para criar um túnel SSH e usar a escuta da porta:
>? Pule esta etapa se o PC local tiver um endereço IP público.
>
```
ssh -Nf -R specified USB/IP port:localhost:specified USB/IP port root@your_host
```
`your_host` indica o endereço IP do CVM.
Por exemplo, se a porta USB/IP for a porta 3240 e o endereço IP do CVM for 192.168.15.24, execute o seguinte comando:
```
ssh -Nf -R 3240:localhost:3240 root@192.168.15.24
```


### Configuração do cliente USB

>? O seguinte usa um PC local sem um IP público como exemplo. Se o seu PC local tiver um IP público, substitua `127.0.0.1` nas etapas a seguir pelo IP público do seu PC local.
>

1. [Faça login em uma instância do Linux](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute os seguintes comandos em sequência para fazer download da origem do USB/IP:
```
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -ivh http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
```
3. Execute os seguintes comandos em sequência para instalar o USB/IP:
```
yum -y install kmod-usbip usbip-utils
modprobe usbip-core
modprobe vhci-hcd
modprobe usbip-host
```
4. Execute o seguinte comando para consultar os dispositivos USB disponíveis do CVM:
```
 usbip list --remote 127.0.0.1
```
Por exemplo, se as informações da chave USB Feitian forem localizadas, o seguinte resultado será retornado:
```
 Dispositivos USB exportáveis
 ======================
 -127.0.0.1 1-1.3: Feitian Technologies, Inc.: unknown product(096e:031b):/sys/devices/platform/scb/fd500000.pcie/pci0000:00/0000:00:00.0/0000:01:00.0/usb1/1-1/1-1.3:(Defined at Interface level)(00/00/00)
```
5. Execute o seguinte comando para vincular o dispositivo USB ao CVM:
```
 usbip attach --remote=127.0.0.1 --busid=1-1.3
```
6. Execute o seguinte comando para consultar a lista de dispositivos USB:
```
 lsusb
```
Se informações semelhantes às seguintes forem retornadas, o dispositivo USB foi compartilhado.
```
 Bus 002 Device 002:ID096e:031b Feitian Technologies, Inc.
 Bus 002 Device 001:ID1d6b:0002 Linux Foundation 2.0 root hub
 Bus 001 Device 001:ID1d6b:0001 Linux Foundation 1.1 root hub
```


