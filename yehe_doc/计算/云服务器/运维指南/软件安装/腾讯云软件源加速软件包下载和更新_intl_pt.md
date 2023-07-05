## Visão geral

Para resolver o problema de acesso lento a fontes oficiais ao instalar dependências, o Tencent Cloud configurou um serviço de cache para alguns softwares. Você pode acelerar a instalação de dependências usando o repositório de software do Tencent Cloud, que atualmente permite o acesso à rede pública e privada.
- Endereço de acesso da rede pública: `http://mirrors.tencent.com`
- Endereço de acesso da rede privada: `http://mirrors.tencentyun.com/`

>?
> - Este documento usa o endereço de acesso à rede pública do repositório de software do Tencent Cloud como exemplo para apresentar como usar os fontes de software no repositório de software do Tencent Cloud no CVM. Se você acessar o repositório usando uma rede privada, substitua o endereço de acesso à rede pública **pelo endereço de acesso à rede privada**.
> - O endereço de fonte usado neste documento é apenas para referência. Obtenha o endereço mais recente no **repositório de software do Tencent Cloud**.

## Observação

O repositório de software do Tencent Cloud atualiza os fontes de software do site oficial de cada fonte de software uma vez por dia.

## Pré-requisitos

Você já está logado no CVM.

## Instruções

### Aceleração de pip usando a fonte de imagem do Tencent Cloud
>! Antes de usar a fonte de imagem do Tencent Cloud, verifique se o seu CVM tem o Python instalado.

#### Usar o caminho da fonte do software temporariamente
Execute o comando a seguir para instalar o pip usando o PyPI do Tencent Could.
```
pip install pip -i  o diretório onde o PyPI está localizado
```
Por exemplo, se o PyPI que você precisa usar estiver no diretório `http://mirrors.cloud.tencent.com/pypi/simple`, execute o seguinte comando:
```
pip install 17monip -i http://mirrors.cloud.tencent.com/pypi/simple --trusted-host mirrors.cloud.tencent.com 
```

#### Definir o caminho da fonte do software padrão
Execute o seguinte comando para modificar o parâmetro `index-url` no arquivo `~/.pip/pip.conf` para o caminho da fonte do repositório de software do Tencent Cloud.

```
[global]
index-url = o diretório onde o PyPI está localizado
trusted-host = endereço de acesso à rede privada/pública
```
Por exemplo, se o PyPI que você precisa usar estiver no diretório `http://mirrors.cloud.tencent.com/pypi/simple`, execute o seguinte comando:
```
[global]
index-url = http://mirrors.cloud.tencent.com/pypi/simple
trusted-host = mirrors.cloud.tencent.com
```

### Aceleração do Maven usando a fonte de imagem do Tencent Cloud
>! Antes de usar a fonte de imagem do Tencent Cloud, verifique se o seu CVM tem o JDK e o Maven instalados.

1. Abra o arquivo de configuração `settings.xml` do Maven.
2. Localize o bloco de código `<mirrors> ... </ mirrors>` e configure o conteúdo a seguir nele.
```
    <mirror>
        <id>nexus-tencentyun</id>
        <mirrorOf>*</mirrorOf>
        <name>Nexus tencentyun</name>
        <url>http://mirrors.cloud.tencent.com/nexus/repository/maven-public/</url>
    </mirror> 
```

### Aceleração do NPM usando a fonte de imagem do Tencent Cloud
>! Antes de usar a fonte de imagem do Tencent Cloud, verifique se o seu CVM tem o Node.js e o NPM instalados.
>
Execute o comando a seguir para instalar o NPM usando o NPM do Tencent Could.
```
npm config set registry http://mirrors.cloud.tencent.com/npm/
```

### Aceleração do Docker usando a fonte de imagem do Tencent Cloud

#### Uso do Docker do Tencent Cloud no cluster TKE

Não é necessária configuração manual. Quando o CVM no cluster Tencent Kubernetes Engine (TKE) cria um nó, o Docker é instalado automaticamente e configurado com a imagem de rede privada do Tencent Cloud.

#### Uso do Docker do Tencent Cloud no CVM

>! Antes de usar o Docker do Tencent Cloud, verifique se o seu CVM o tem instalado.
>  Apenas o Docker 1.3.2 ou versões posteriores são compatíveis com o mecanismo Docker Hub Mirror. Se você não instalou o Docker 1.3.2 ou versões posteriores, ou se a versão instalada for muito antiga, instale ou atualize-a primeiro.
 
Escolha etapas de operação diferentes com base no sistema operacional do CVM.
- As etapas a seguir são para Ubuntu 14.04, Debian, CentOS 6, Fedora, openSUSE e outros sistemas operacionais. As etapas específicas para outras versões de sistemas operacionais podem variar:
 1. Execute o seguinte comando para abrir o arquivo de configuração `/etc/default/docker`.
```
vim /etc/default/docker
```
 2. Pressione **i** para mudar para o modo de edição, insira o conteúdo a seguir e salve.
```
DOCKER_OPTS="--registry-mirror=https://mirror.ccs.tencentyun.com"
```
- Para CentOS 7:
 1. Execute o seguinte comando para abrir o arquivo de configuração `/etc/docker/daemon.json`.
```
vim /etc/docker/daemon.json
```
 2. Pressione **i** para mudar para o modo de edição, insira o conteúdo a seguir e salve.
```
{
   "registry-mirrors": [
       "https://mirror.ccs.tencentyun.com"
  ]
}
```
- Para Windows com o Boot2Docker instalado:
 1. Acesse o Boot2Docker Start Shell e execute o seguinte comando:
```
sudo su echo "EXTRA_ARGS=\"–registry-mirror=https://mirror.ccs.tencentyun.com\"" >> /var/lib/boot2docker/profile exit 
```
 2. Reinicie o Boot2Docker.

### Aceleração do MariaDB usando a imagem do Tencent Cloud
>? As etapas a seguir usam o CentOS 7 como exemplo. As etapas específicas variam de acordo com o sistema operacional.

1. Execute o comando a seguir para criar o arquivo `MariaDB.repo` em `/etc/yum.repos.d/`.
```
vi /etc/yum.repos.d/MariaDB.repo
```
2. Pressione **i** para mudar para o modo de edição, insira o conteúdo a seguir e salve.
```
# MariaDB 10.2 CentOS7-amd64
[mariadb]  
name = MariaDB  
baseurl = http://mirrors.cloud.tencent.com/mariadb/yum/10.2/centos7-amd64/
gpgkey = http://mirrors.cloud.tencent.com/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck=1  
```
3. Execute o comando a seguir para esvaziar o cache do YUM.
```
yum clean all
```
4. Execute o comando a seguir para instalar o MariaDB.
```
yum install MariaDB-client MariaDB-server
```

### Aceleração do MongoDB usando a imagem do Tencent Cloud
>? As etapas a seguir usam o MongoDB 4.0 como exemplo. Se você precisar instalar outra versão, altere o número da versão no caminho do espelho.

#### Uso do MongoDB do Tencent Cloud em CVMs com sistemas CentOS ou Redhat

1. Execute o comando a seguir para criar o arquivo `mongodb.repo` em `/etc/yum.repos.d/`.
```
vi /etc/yum.repos.d/mongodb.repo
```
2. Pressione **i** para mudar para o modo de edição, insira o conteúdo a seguir e salve.
```
[mongodb-org-4.0]
name=MongoDB Repository
baseurl=http://mirrors.cloud.tencent.com/mongodb/yum/el7-4.0
gpgcheck=0
enabled=1
```
3. Execute o comando a seguir para instalar o MongoDB.
```
yum install -y mongodb-org
```

#### Uso do MongoDB do Tencent Cloud em CVMs com o sistema Debian

1. Com base nas diferentes versões do Debian, execute o comando a seguir para importar a chave pública GPG do MongoDB.
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
```
2. Execute o comando a seguir para configurar o caminho do `mirror`.
```
#Debian 8
echo "deb http://mirrors.cloud.tencent.com/mongodb/apt/debian jessie/mongodb-org/4.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Debian 9
echo "deb http://mirrors.cloud.tencent.com/mongodb/apt/debian stretch/mongodb-org/4.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```
3. Execute o comando a seguir para limpar o cache.
```shell
sudo apt-get clean all
```
4. Execute o comando a seguir para atualizar a lista de pacotes de software.
```
sudo apt-get update
```
5. Execute o comando a seguir para instalar o MongoDB.
```
sudo apt-get install -y mongodb-org
```

#### Uso do MongoDB do Tencent Cloud em CVMs com o sistema Ubuntu

1. Execute o comando a seguir para importar a chave pública GPG do MongoDB.
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
```
2. Execute o comando a seguir para configurar o caminho do `mirror`.
```
#Ubuntu 14.04
echo "deb [ arch=amd64 ] http://mirrors.cloud.tencent.com/mongodb/apt/ubuntu trusty/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Ubuntu 16.04
echo "deb [ arch=amd64 ] http://mirrors.cloud.tencent.com/mongodb/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Ubuntu 18.04
echo "deb [ arch=amd64 ] http://mirrors.cloud.tencent.com/mongodb/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```
3. Execute o comando a seguir para limpar o cache.
```shell
sudo apt-get clean all
```
4. Execute o comando a seguir para atualizar a lista de pacotes de software.
```
sudo apt-get update
```
5. Execute o comando a seguir para instalar o MongoDB.
```
sudo apt-get install -y mongodb-org
```

### Aceleração do Rubygems usando a fonte de imagem do Tencent Cloud
>! Antes de usar a fonte de imagem do Tencent Cloud, verifique se o seu CVM tem o Ruby instalado.

Execute o comando a seguir para modificar o endereço da fonte do RubyGems.
```
gem source -r https://rubygems.org/
gem source -a http://mirrors.cloud.tencent.com/rubygems/
```
