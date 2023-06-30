## Visão geral

O cloud-init permite que você personalize as configurações durante a primeira inicialização de uma instância. Se a imagem importada não tiver o serviço cloud-init instalado, as instâncias inicializadas por meio da imagem não podem ser inicializadas corretamente. Como resultado, a imagem não será importada. Este documento descreve como instalar o serviço cloud-init.
É possível usar um dos seguintes métodos para instalar o cloud-init:

- [Download manual do pacote de origem do cloud-init](#ManualDown) 
- [Uso do pacote do cloud-init de origem do software](#SoftSources)


## Pré-requisitos
O servidor com o serviço cloud-init instalado pode acessar a rede pública.

## Instruções


<span id="ManualDown"></span>
### Download manual do pacote de origem do cloud-init 

#### Download do pacote de origem do cloud-init
>?  
> - A versão cloud-init-17.1 é a mais compatível com o Tencent Cloud. Isso garante que todos os itens de configuração de CVMs criados por meio da imagem possam ser inicializados corretamente. Recomendamos que você instale a versão **cloud-init-17.1.tar.gz**. Você também pode [clicar aqui](https://launchpad.net/cloud-init/+download) para baixar outras versões. Este documento usa a versão cloud-init-17.1 como exemplo.
> - Se a instalação falhar, [baixe manualmente o pacote do green cloud-init](#greeninitCloudInit) para instalar o serviço.
>
Execute o seguinte comando para baixar o pacote de origem do cloud-init:
```
wget https://launchpad.net/cloud-init/trunk/17.1/+download/cloud-init-17.1.tar.gz
```

#### Instalação do cloud-init
1. Execute o seguinte comando para descompactar o pacote de instalação do cloud-init:
>? Se você estiver usando o sistema operacional Ubuntu, execute este comando com a conta “raiz”.
>
```
tar -zxvf cloud-init-17.1.tar.gz 
```
2. Execute o seguinte comando para inserir o diretório descompactado do pacote de instalação do cloud-init; ou seja, o diretório cloud-init-17.1:
```
cd cloud-init-17.1
```
3. Instale o Python-pip de acordo com a versão do sistema operacional.
 - Para CentOS 6/7, execute o seguinte comando:
```
yum install python-pip -y
```
 - Para Ubuntu, execute o seguinte comando:
```
apt-get install python-pip -y
```
Durante a instalação, se ocorrer um erro como “failed to install (falha ao instalar)” ou “installation package not found (pacote de instalação não encontrado)”, consulte [solução da falha de instalação do Python-pip](#updateSoftware) para solucioná-lo.
4. Execute o seguinte comando para instalar as dependências:
>!  O Python 2.6 não é compatível quando o cloud-init usa solicitações 2.20.0 ou posteriores. Se o interpretador Python instalado no ambiente de imagem for o Python versão 2.6 ou anterior, execute o comando `pip install 'requests<2.20.0'` para instalar as solicitações 2.20.0 ou posteriores antes de instalar as dependências do cloud-init.
>
```
pip install -r requirements.txt
```
5. Instale o componente cloud-utils de acordo com a versão do sistema operacional.
 - Para CentOS 6, execute o seguinte comando:
```
yum install cloud-utils-growpart dracut-modules-growroot -y
dracut -f
```
 - Para CentOS 7, execute o seguinte comando:
```
yum install cloud-utils-growpart -y
```
 - Para Ubuntu, execute o seguinte comando:
```
apt-get install cloud-guest-utils -y
```
6. Execute os seguintes comandos para instalar o cloud-init:
```
python setup.py build
python setup.py install --init-system systemd
```
>! O `--init-system` pode ser seguido por qualquer um dos systemd, sysvinit, sysvinit_deb, sysvinit_freebsd, sysvinit_openrc, sysvinit_suse ou upstart [default: None]. Configure os parâmetros com base no método de gerenciamento de serviço de inicialização automática do sistema operacional. Se parâmetros incorretos forem configurados, o serviço cloud-init não pode ser iniciado automaticamente na inicialização do sistema. Este documento usa o método de gerenciamento de serviço de inicialização automática systemd como exemplo.

#### Modificação do arquivo de configuração do cloud-init

1. Baixe o cloud.cfg para seu sistema operacional.
 - [Clique aqui](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg) para baixar o cloud.cfg para Ubuntu.
 - [Clique aqui](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg) para baixar o cloud.cfg para CentOS.
2. Substitua o conteúdo de `/etc/cloud/cloud.cfg` pelo do arquivo cloud.cfg baixado.

#### Adição de um usuário syslog
Execute o seguinte comando para adicionar um usuário syslog:
```
useradd syslog
```

#### Configuração do serviço cloud-init para inicialização automática
- **Se o seu sistema operacional usa o método de gerenciamento de serviço de inicialização automática systemd, execute os seguintes comandos.**
>? Para verificar se o sistema operacional usa o systemd, execute o comando `strings /sbin/init | grep "/lib/system"`, e você receberá uma mensagem de retorno.
>
 1. **Execute o seguinte comando no Ubuntu ou Debian:**
```
 ln -s /usr/local/bin/cloud-init /usr/bin/cloud-init 
```
 2. **Execute os seguintes comandos em todos os sistemas operacionais:**
```
systemctl enable cloud-init-local.service 
systemctl start cloud-init-local.service
systemctl enable cloud-init.service
systemctl start cloud-init.service
systemctl enable cloud-config.service
systemctl start cloud-config.service
systemctl enable cloud-final.service
systemctl start cloud-final.service
systemctl status cloud-init-local.service
systemctl status cloud-init.service
systemctl status cloud-config.service
systemctl status cloud-final.service
```
 3. **Execute o seguinte comando no CentOS ou Redhat.**
 Substitua o conteúdo de `/lib/systemd/system/cloud-init-local.service` pelo seguinte:
```
[Unit]
Description=Initial cloud-init job (pre-networking)
Wants=network-pre.target
After=systemd-remount-fs.service
Before=NetworkManager.service
Before=network-pre.target
Before=shutdown.target
Conflicts=shutdown.target
RequiresMountsFor=/var/lib/cloud
[Service]
Type=oneshot
ExecStart=/usr/bin/cloud-init init --local
ExecStart=/bin/touch /run/cloud-init/network-config-ready
RemainAfterExit=yes
TimeoutSec=0
# Output needs to appear in instance console output
StandardOutput=journal+console
[Install]
WantedBy=cloud-init.target
```
Substitua o conteúdo de `/lib/systemd/system/cloud-init.service` pelo seguinte:
```
[Unit]
Description=Initial cloud-init job (metadata service crawler)
Wants=cloud-init-local.service
Wants=sshd-keygen.service
Wants=sshd.service
After=cloud-init-local.service
After=systemd-networkd-wait-online.service
After=networking.service
After=systemd-hostnamed.service
Before=network-online.target
Before=sshd-keygen.service
Before=sshd.service
Before=systemd-user-sessions.service
Conflicts=shutdown.target
[Service]
Type=oneshot
ExecStart=/usr/bin/cloud-init init
RemainAfterExit=yes
TimeoutSec=0
# Output needs to appear in instance console output
StandardOutput=journal+console
[Install]
WantedBy=cloud-init.target
```
- **Se o seu sistema operacional usa o método de gerenciamento de serviço de inicialização automática sysvinit, execute os seguintes comandos:**
>? Para verificar se o sistema operacional usa o sysvinit, execute o comando `strings /sbin/init | grep "sysvinit"`, e você receberá uma mensagem de retorno.
>
```
chkconfig --add cloud-init-local
chkconfig --add cloud-init
chkconfig --add cloud-config
chkconfig --add cloud-final
chkconfig cloud-init-local on 
chkconfig cloud-init on 
chkconfig cloud-config on 
chkconfig cloud-final on 
```


<span id="SoftSources"></span>
### Uso do pacote do cloud-init de origem do software

#### Instalação do cloud-init

Execute o seguinte comando para instalar o cloud-init:
```
apt-get/yum install cloud-init
```
>? Por padrão, a versão do cloud-init instalada executando `apt-get` ou` yum` é a versão padrão do cloud-init na origem do software configurada para o sistema operacional. Alguns itens de configuração de instâncias criadas usando a imagem cujo cloud-init está instalado dessa forma podem não ser inicializados conforme o esperado. Portanto, recomendamos que você instale o serviço pelo [download manual do pacote de origem do cloud-init](#ManualDown).
>

#### Modificação do arquivo de configuração do cloud-init
1. Baixe o cloud.cfg para seu sistema operacional.
 - [Clique aqui](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg) para baixar o cloud.cfg para Ubuntu.
 - [Clique aqui](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg) para baixar o cloud.cfg para CentOS.
2. Substitua o conteúdo de `/etc/cloud/cloud.cfg` pelo do arquivo cloud.cfg baixado.

## Operações relevantes
>! Não reinicie o servidor depois de realizar as operações acima. Caso contrário, você precisará realizá-las novamente.
>
1. Execute os comandos a seguir para verificar se a configuração do cloud-init foi bem-sucedida.
```
cloud-init init --local
rm -rf /var/lib/cloud
```
2. Execute o seguinte comando no Ubuntu ou Debian:
```
rm -rf /etc/network/interfaces.d/50-cloud-init.cfg
```
3. Para Ubuntu ou Debian, substitua o conteúdo de `/etc/network/interfaces` pelo seguinte:
```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
source /etc/network/interfaces.d/*
```

## Observações

<span id="greeninitCloudInit"></span>
### Download da edição portátil do pacote do cloud-init
Se você não conseguir instalar o cloud-init conforme instruído em [Download manual do pacote de origem do cloud-init](#ManualDown), tente as seguintes etapas:
1. [Clique aqui](https://image-tools-1251783334.cos.ap-guangzhou.myqcloud.com/greeninit-x64-beta.tgz) para obter a edição portátil do pacote do cloud-init.
2. Execute o seguinte comando para descompactar o pacote portátil:
```
tar xvf greeninit-x64-beta.tgz 
```
3. Execute o seguinte comando para inserir o diretório do pacote descompactado; ou seja, o diretório `greeninit`:
```
cd greeninit
```
4. Execute o seguinte comando para instalar o cloud-init:
```
sh install.sh 
```

<span id="updateSoftware"></span>

### Solução da falha de instalação do Python-pip

Durante a instalação, se ocorrer um erro como “failed to install (falha ao instalar)” ou “installation package not found (pacote de instalação não encontrado)”, solucione o problema com base no sistema operacional da seguinte forma:
- Para CentOS 6/7:
  1. Execute o seguinte comando para configurar o repositório de armazenamento EPEL.
```
yum install epel-release -y
```
  2. Execute o seguinte comando para instalar o Python-pip.
```
yum install python-pip -y
```
- Para Ubuntu:
  1. Execute o seguinte comando para atualizar a lista de pacotes de software.
```
apt-get update -y
```
  2. Execute o seguinte comando para instalar o Python-pip.
```
apt-get install python-pip -y
```


