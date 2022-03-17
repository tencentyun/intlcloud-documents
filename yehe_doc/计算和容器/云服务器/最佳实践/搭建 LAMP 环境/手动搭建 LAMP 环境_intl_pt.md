## Cenário
LAMP é uma arquitetura de serviço comum da web, executada no Linux, que consiste em Apache, MySQL/MariaDB e PHP. Este artigo descreve como configurar o LAMP em um CVM Linux.

Você deve estar familiarizado com os comandos comuns do Linux, como [Instalação de software via YUM em um ambiente CentOS](https://intl.cloud.tencent.com/document/product/213/2046), e compreender as versões do software instalado.

## Software
Estes são os softwares envolvidos:
- O CentOS é uma distribuição do sistema operacional Linux. Usaremos a versão 7.6 neste artigo.
- Apache é um software de servidor web. Usaremos a versão 2.4.6 neste artigo.
- MariaDB é um sistema de gerenciamento de banco de dados. Usaremos a versão 10.4.8 neste artigo.
- PHP é uma linguagem de script. Usaremos a versão 7.0.33 neste artigo.

## Pré-requisitos
Você precisa de um CVM Linux. Se você ainda não comprou um, consulte [Introdução aos CVMs Linux](http://intl.cloud.tencent.com/document/product/213/2936).

## Instruções
### Etapa 1: login em uma instância do Linux
[Faça login em uma instância do Linux usando WebShell (recomendado)](https://intl.cloud.tencent.com/document/product/213/5436). Você também pode usar outros métodos de login com os quais se sinta confortável:
- [Faça login em uma instância do Linux usando software de login remoto](https://intl.cloud.tencent.com/document/product/213/32502).
- [Faça login em uma instância do Linux usando SSH](https://intl.cloud.tencent.com/document/product/213/32501)

### Etapa 2: Instalação do Apache
1. Execute o seguinte comando para instalar o Apache.
```
yum install httpd -y
```
2. Execute os comandos a seguir para iniciar o Apache e defina-o para iniciar automaticamente quando o sistema for iniciado.
```
systemctl start httpd
```
```
systemctl enable httpd
```
3. Abra uma janela do navegador e visite o seguinte URL para verificar se o Apache está funcionando corretamente.
```
http://[endereço IP público da instância CVM]
```
O seguinte aparecerá se o Apache estiver instalado corretamente:
![](https://main.qcloudimg.com/raw/f9dc3992f4d6e7e94bb63330fd5cadfe.png)


### Etapa 3: Instalação do MariaDB
1. Execute o seguinte comando para verificar se o MariaDB já está instalado
```
rpm -qa | grep -i mariadb
```
 - Se for exibido o seguinte, o MariaDB já está instalado.
 ![](https://main.qcloudimg.com/raw/6fa7fb51de4a61f4da08eb036b6c3e85.png)
Se for esse o caso, execute o seguinte para remover o MariaDB e evitar conflitos entre as diferentes versões.
```
yum -y remove [Package name]
```
 - Se nada for retornado, o MariaDB não está instalado. Nesse caso, prossiga para a próxima etapa.
2. Execute o seguinte comando para criar um arquivo chamado `MariaDB.repo` em `/etc/yum.repos.d/`. 
```
vi /etc/yum.repos.d/MariaDB.repo
```
3. Pressione **i** para mudar para o modo de edição e digite o seguinte.
```
# MariaDB 10.4 CentOS repository list - created 2019-11-05 11:56 UTC
# http://downloads.mariadb.org/mariadb/repositories/
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.4/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```
> Para informações de instalação de outras versões, visite o [site oficial do MariaDB](https://downloads.mariadb.org).
>
5. Pressione **Esc** e insira **: wq** para salvar o arquivo e voltar.
6. Execute o seguinte comando para instalar o MariaDB.
```
yum -y install MariaDB-client MariaDB-server
```
7. Execute os seguintes comandos para iniciar o MariaDB e defina-o para iniciar automaticamente junto com o sistema.
```
systemctl start mariadb
```
```
systemctl enable mariadb
```
8. Execute o seguinte comando para verificar se o MariaDB foi instalado com sucesso.
```
mysql
```
Se for exibido o seguinte, o MariaDB foi instalado com sucesso.
![](https://main.qcloudimg.com/raw/bfe9a604457f6de09933206c21fde13b.png)
9. Execute o seguinte comando para sair do MariaDB.
```
\q
```

### Etapa 4: Instalação e configuração do PHP
1. Execute os comandos a seguir para atualizar a origem do software PHP no Yum.
```
rpm -Uvh https://mirrors.cloud.tencent.com/epel/epel-release-latest-7.noarch.rpm 
```
```
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
```
2. Execute o comando a seguir para instalar os pacotes necessários para o PHP 7.0.33.
```
yum -y install php70w php70w-opcache php70w-mbstring php70w-gd php70w-xml php70w-pear php70w-fpm php70w-mysql php70w-pdo
```
3. Execute o seguinte comando para editar o arquivo de configuração do Apache.
```
vi /etc/httpd/conf/httpd.conf
```
4. Pressione **i** para entrar no modo de edição e fazer as seguintes alterações:
![](https://main.qcloudimg.com/raw/0b478ca5aa21124a531cfd5c8860cb70.png)
![](https://main.qcloudimg.com/raw/aeeb6fff1af9cf71735cae558455ee94.png)
![](https://main.qcloudimg.com/raw/cc840587150c3282c972a6b23e0c1a68.png)
![](https://main.qcloudimg.com/raw/de36e94d0e4791d1d84f141120125456.png)
 1. Encontre `ServerName www.example.com: 80` e inicie uma nova linha abaixo dele. Insira o seguinte:
 ```
ServerName localhost:80
```
 2. Encontre `Require all denied` em `<Directory>` e altere para` Require all granted`.
 3. Encontre `<IfModule dir_module>` e altere o conteúdo para `DirectoryIndex index.php index.html`.
 4. Inicie uma nova linha abaixo de `AddType application/x-gzip .gz .tgz` e insira o seguinte:
```
AddType application/x-httpd-php .php
AddType application/x-httpd-php-source .phps
```
5. Pressione **Esc** e insira **: wq** para salvar o arquivo e voltar.
6. Execute o seguinte comando para reiniciar o Apache.
```
systemctl restart httpd
```

## Verificação da configuração do ambiente.
1. Execute o seguinte comando para criar um arquivo de teste.
```
echo "<?php phpinfo(); ?>" >> /var/www/html/index.php
```
2. Abra uma janela do navegador em sua máquina local e visite a seguinte URL para verificar se a configuração do ambiente foi bem-sucedida.
```
http://CVM Public IP/index.php
```
Se o seguinte for exibido, o ambiente LAMP foi configurado com sucesso.
![](https://main.qcloudimg.com/raw/64681fb76bad29072de9ddc3250e66d1.png)

## Operações relevantes
Depois que o ambiente LAMP é construído, você pode [configurar manualmente o site Drupal](https://intl.cloud.tencent.com/document/product/213/34814).


## Perguntas frequentes
Se você encontrar um problema ao usar o CVM, consulte os seguintes documentos para solucionar problemas com base em sua situação real.
- Para questões relacionadas ao login do CVM, consulte [Login de senha e login de chave SSH](https://intl.cloud.tencent.com/document/product/213/18120) e [Login e acesso remoto](https://intl.cloud.tencent.com/document/product/213/17278).
- Para questões relacionadas à rede CVM, consulte [Endereços IP](https://intl.cloud.tencent.com/document/product/213/17285) e [Portas e grupos de segurança](https://intl.cloud.tencent.com/document/product/213/2502).
- Para questões relacionadas aos discos CVM, consulte [Discos de sistema e dados](https://intl.cloud.tencent.com/document/product/213/17351).

