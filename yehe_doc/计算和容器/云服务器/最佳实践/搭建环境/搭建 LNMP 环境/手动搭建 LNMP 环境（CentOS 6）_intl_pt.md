## Introdução
O ambiente LNMP é uma arquitetura de servidor de site, executada em Linux, que consiste em Nginx, MySQL ou MariaDB e PHP. Este artigo descreve como configurar o LNMP em um CVM.

Para configurar o ambiente LNMP, você deve estar familiarizado com os comandos comuns do Linux, como [Instalação de software via YUM no CentOS](https://intl.cloud.tencent.com/document/product/213/2046) para alguns exemplos) e compreender as versões de software instalado.

## Software
Os seguintes softwares estão envolvidos:
O CentOS é uma distribuição do sistema operacional Linux. Usamos o CentOS 6.9 neste artigo.
O Nginx é um servidor web. Usamos o Nginx 1.17.5 neste artigo.
O MySQL é um software de banco de dados. Usamos MySQL 5.1.73.
PHP é uma linguagem de script. Usamos PHP 7.1.32 neste artigo.

## Pré-requisitos

Você precisa de um CVM Linux. Se você ainda não comprou um, consulte [Introdução aos CVMs Linux](http://intl.cloud.tencent.com/document/product/213/2936).


## Instruções
### Etapa 1: login em uma instância do Linux
[Faça login em uma instância do Linux usando WebShell (recomendado)](https://intl.cloud.tencent.com/document/product/213/5436). Você também pode usar outros métodos de login com os quais se sinta confortável:
- [Faça login em uma instância do Linux usando software de login remoto](https://intl.cloud.tencent.com/document/product/213/32502).
- [Faça login em uma instância do Linux usando SSH](https://intl.cloud.tencent.com/document/product/213/32501).

### Etapa 2: Instalação do Nginx
1. Execute o seguinte comando para criar um arquivo chamado 
`/etc/yum.repos.d/`.
```
vi /etc/yum.repos.d/nginx.repo
```
2. Pressione **i** para entrar no modo de edição e fazer as seguintes alterações.
```
[nginx]
name = nginx repo
baseurl=https://nginx.org/packages/mainline/centos/6/$basearch/
gpgcheck=0
enabled=1
```
5. Pressione **Esc** e insira **: wq** para salvar o arquivo e voltar.
4. Execute o seguinte comando para instalar o Nginx.
```
yum install -y nginx
```
5. Execute o seguinte comando para abrir o `nginx.conf`.
```
vim /etc/nginx/nginx.conf
```
6. Pressione **i** para mudar para o modo de edição.
7. Encontre `server{...}` e substitua o conteúdo dentro das chaves pelo seguinte.
   Isso cancela o monitoramento de endereços IPv6 e configura o Nginx para interagir com o PHP.
> Se você não conseguir encontrar `server{...}` em `nginx.conf`, adicione o seguinte acima de `include /etc/nginx/conf.d/*conf;`
>
```
server {
	listen       80;
	root   /usr/share/nginx/html;
	server_name  localhost;
	#charset koi8-r;
	#access_log  /var/log/nginx/log/host.access.log  main;
	#
	location / {
		  index index.php index.html index.htm;
	}
	#error_page  404              /404.html;
	#redirect server error pages to the static page /50x.html
	#
	error_page   500 502 503 504  /50x.html;
	location = /50x.html {
	  root   /usr/share/nginx/html;
	}
	#pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
	#
	location ~ .php$ {
	  fastcgi_pass   127.0.0.1:9000;
	  fastcgi_index  index.php;
	  fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
	  include        fastcgi_params;
	}
}
```
8. Pressione **Esc** e insira **: wq** para salvar o arquivo e voltar.
9. Execute o seguinte comando para iniciar o Nginx.
```
service nginx start
```
10. Execute o seguinte comando para definir que o Nginx inicie automaticamente junto com o sistema.
```bash
chkconfig --add nginx
```
```
chkconfig  nginx on
```
11. Em um navegador local, visite o seguinte URL para verificar se o serviço Nginx está funcionando corretamente.
```
http://[endereço IP público da instância CVM]
```
Se for exibido o seguinte, o Nginx foi instalado e configurado com êxito.
![](https://main.qcloudimg.com/raw/fdc40877928729679d392eb304a3f12c.png)


### Etapa 3: Instalação do MySQL
1. Execute o seguinte comando para verificar se o MySQL já está instalado.
```
rpm -qa | grep -i mysql
```
 - Se for exibido o seguinte, o MySQL já está instalado.
![](https://main.qcloudimg.com/raw/74e544638637d39209cc1e474083d11d.png)
Para evitar conflito entre versões diferentes, execute o seguinte comando para remover o MySQL existente.
```
yum -y remove [Package name]
``` 
 - Se nada for retornado, o MySQL não está instalado. Nesse caso, prossiga para a próxima etapa.
2. Execute o seguinte comando para instalar o MySQL.
```
yum install -y mysql-devel.x86_64 mysql-server.x86_64 mysql-libs.x86_64
```
3. Execute o seguinte comando para iniciar o MySQL.
```
service mysqld start 
```
4. Execute o seguinte comando para definir que o MySQL inicie automaticamente junto com o sistema.
```bash
chkconfig --add mysqld
```
```
chkconfig mysqld  on 
```
5. Execute o seguinte comando para verificar a instalação do MySQL.
```
mysql
```
Se for exibido o seguinte, o MySQL foi instalado com sucesso.
![](https://main.qcloudimg.com/raw/9c9347ad0264ddad5e98c8dd48adcc6a.png)
6. Execute o seguinte comando para sair do MySQL.
```
\q
```

### Etapa 4: Instalação e configuração do PHP
1. Execute os comandos a seguir para atualizar a origem do software PHP no Yum.
```
rpm -Uvh https://mirrors.cloud.tencent.com/epel/epel-release-latest-6.noarch.rpm
```
```
rpm -Uvh https://mirror.webtatic.com/yum/el6/latest.rpm
```
2. Execute o comando a seguir para instalar os pacotes necessários para o PHP 7.1.32.
```
yum -y install mod_php71w.x86_64 php71w-cli.x86_64 php71w-common.x86_64 php71w-mysqlnd php71w-fpm.x86_64
```
3. Execute o seguinte comando para iniciar o serviço PHP-FPM.
```
service php-fpm start
```
4. Execute o seguinte comando para definir a inicialização automática do serviço PHP-FPM.
```bash
chkconfig --add php-fpm  
```
```
chkconfig php-fpm on
```


## Verificação da configuração do ambiente.
1. Execute o seguinte comando para criar um arquivo de teste.
```
echo "<?php phpinfo(); ?>" >> /usr/share/nginx/html/index.php
```
2. Execute o seguinte comando para reiniciar o Nginx.
```
service nginx restart
```
3. Em um navegador local, visite o seguinte URL para verificar se a configuração do ambiente foi bem-sucedida.
```
http://[endereço IP público da instância CVM]
```
Se os resultados a seguir forem exibidos, a configuração do ambiente foi bem-sucedida.
![](https://main.qcloudimg.com/raw/64af927320f2121ae4daf15cf2eaba39.png)



## Operações relacionadas

Depois que o ambiente LNMP é construído, você pode [iniciar um site WordPress](https://intl.cloud.tencent.com/document/product/213/8044).

## Perguntas frequentes

Se você encontrar um problema ao usar o CVM, consulte os seguintes documentos para solucionar problemas com base em sua situação real.

- Para questões relacionadas ao login do CVM, consulte [Login de senha e login de chave SSH](https://intl.cloud.tencent.com/document/product/213/18120) e [Login e acesso remoto](https://intl.cloud.tencent.com/document/product/213/17278).
- Para questões relacionadas à rede CVM, consulte [Endereços IP](https://intl.cloud.tencent.com/document/product/213/17285) e [Portas e grupos de segurança](https://intl.cloud.tencent.com/document/product/213/2502).
- Para questões relacionadas aos discos CVM, consulte [Discos de sistema e dados](https://intl.cloud.tencent.com/document/product/213/17351).



