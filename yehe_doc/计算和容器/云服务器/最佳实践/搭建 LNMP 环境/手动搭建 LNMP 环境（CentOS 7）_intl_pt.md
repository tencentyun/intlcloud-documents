## Cenário
LNMP se refere a uma arquitetura de servidor web comum que consiste em Nginx, MySQL ou MariaDB e PHP em execução no Linux. Este artigo descreve como implantar LNMP em um Tencent Cloud Virtual Machine (CVM).

Para construir manualmente um ambiente LNMP, é preciso estar familiarizado com os comandos do Linux (consulte [Instalação do software usando YUM em um ambiente CentOS](https://intl.cloud.tencent.com/document/product/213/2046), para alguns exemplos), uso e compatibilidade de versão do software a ser instalado.

## Versões de software de amostra
Neste exemplo, as seguintes versões de software são usadas para construir o ambiente LNMP:
- Linux: Sistema operacional Linux. Neste exemplo, é usado CentOS 7.6.
- Nginx: web server. Neste exemplo, é usado Nginx 1.17.7.
- MariaDB: banco de dados. Neste exemplo, é usado MariaDB 10.4.8.
- PHP: linguagem de script. Neste exemplo, é usado PHP 7.2.22.


## Pré-requisitos
Você ter adquirido um CVM Linux.


## Instruções

### Etapa 1: login em uma instância do Linux
[Faça login em uma instância do Linux usando o modo padrão (recomendado)](https://intl.cloud.tencent.com/document/product/213/5436). Você também pode usar outros métodos de login, conforme necessário:
- [Faça login em uma instância do Linux usando software de login remoto](https://intl.cloud.tencent.com/document/product/213/32502)
- [Faça login em uma instância do Linux usando SSH](https://intl.cloud.tencent.com/document/product/213/32501)

### Etapa 2: Instalação do Nginx
1. Execute o seguinte comando para criar um arquivo chamado 
`/etc/yum.repos.d/`.
```
vi /etc/yum.repos.d/nginx.repo
```
2. Pressione **i** para alternar para o modo de edição e digite o seguinte.
```
[nginx] 
name = nginx repo 
baseurl = https://nginx.org/packages/mainline/centos/7/$basearch/ 
gpgcheck = 0 
enabled = 1
```
3. Pressione **Esc**, digite **:wq**, salve o arquivo e retorne.
4. Execute o seguinte comando para instalar o Nginx.
```
yum install -y nginx
```
5. Execute o seguinte comando para abrir o `nginx.conf`.
```
vim /etc/nginx/nginx.conf
```
6. Pressione i para alternar para o modo de edição e edite o arquivo `nginx.conf`.
7. Encontre `server{...}` e substitua a string dentro das chaves pelo seguinte. Isso cancela a escuta do endereço IPv6 e configura o Nginx para realizar a ligação com o PHP.
> Você pode usar `Ctrl+F` para page down e`Ctrl+B` para page up para visualizar o arquivo.
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
Se você não conseguir encontrar `server{...}` em `nginx.conf`, adicione o seguinte antes de `include/etc/nginx/conf.d/*conf;`, como mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/901a3957ccd992c2fb345287271c4bef.png)
7. Pressione **Esc**, digite **:wq**, salve o arquivo e retorne.
8. Execute o seguinte comando para iniciar o Nginx.
```
systemctl start nginx
```
9. Execute o seguinte comando para configurar a ativação automática do Nginx na inicialização.
```
systemctl enable nginx 
```
10. Em um navegador local, visite o seguinte URL para verificar se o serviço Nginx está funcionando corretamente.
```
http://<Public IP address of the CVM instance>
```
Se for exibido o seguinte, o Nginx foi instalado e configurado com êxito.
![](https://main.qcloudimg.com/raw/fdc40877928729679d392eb304a3f12c.png)


### Etapa 3: Instalação da base de dados
1. Execute o seguinte comando para verificar se o MariaDB já está instalado 
```
rpm -qa | grep -i mariadb
```
 - Se for exibido o seguinte, o MariaDB foi instalado.
![](https://main.qcloudimg.com/raw/6fa7fb51de4a61f4da08eb036b6c3e85.png)
Para evitar conflitos entre versões diferentes, execute o seguinte comando para remover o MariaDB instalado.
```
yum -y remove <Package name>
```
 - Se nada for retornado, o MariaDB não está instalado. Nesse caso, prossiga para a próxima etapa.
2. Execute o seguinte comando para criar o arquivo `MariaDB.repo` em `/etc/yum.repos.d/`.
```
vi /etc/yum.repos.d/MariaDB.repo
```
3. Pressione i para mudar para o modo de edição e digite o seguinte para adicionar MariaDB.
> Diferentes sistemas operacionais usam diferentes versões do MariaDB. Para obter informações de instalação sobre outras versões de sistema operacional, visite o [site do MariaDB](https://downloads.mariadb.org).
>
```
# MariaDB 10.4 CentOS repository list - created 2019-11-05 11:56 UTC
# http://downloads.mariadb.org/mariadb/repositories/
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.4/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```
4. Pressione **Esc**, digite **:wq**, salve o arquivo e retorne.
5. Execute o seguinte comando para instalar o MariaDB. Preste atenção ao progresso da instalação e aguarde até que ela seja concluída.
```
yum -y install MariaDB-client MariaDB-server
```
6. Execute o seguinte comando para iniciar o serviço MariaDB.
```
systemctl start mariadb
```
7. Execute o seguinte comando para configurar a ativação automática do MariaDB na inicialização.
```
systemctl enable mariadb
```
8. Execute o seguinte comando para verificar se o MariaDB foi instalado com sucesso.
```
mysql
```
Se aparecer o seguinte, o MariaDB foi instalado com sucesso.
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
2. Execute o comando a seguir para instalar os pacotes necessários para o PHP 7.2.
```
yum -y install mod_php72w.x86_64 php72w-cli.x86_64 php72w-common.x86_64 php72w-mysqlnd php72w-fpm.x86_64
```
3. Execute o seguinte comando para iniciar o serviço PHP-FPM.
```
systemctl start php-fpm
```
4. Execute o seguinte comando para configurar a ativação automática do PHP- FPM na inicialização.
```
systemctl enable php-fpm
```

## Verificação de configuração
Após finalizar a configuração de ambientes, conclua as etapas a seguir para verificar se o ambiente LNMP foi construído com sucesso.
1. Execute o seguinte comando para criar um arquivo de teste.
```
echo "<?php phpinfo(); ?>" >> /usr/share/nginx/html/index.php
```
2. Execute o seguinte comando para reiniciar o serviço Nginx.
```
systemctl restart nginx
```
3. Em um navegador local, visite o seguinte URL para verificar se a configuração do ambiente foi bem-sucedida.
```
http://<Public IP address of the CVM instance>
```
Se os resultados a seguir forem exibidos, a configuração do ambiente foi bem-sucedida.
![](https://main.qcloudimg.com/raw/640812413941a61efe29d7faa546ad80.png)


## Operações relevantes
Depois que o ambiente LNMP for construído, você poderá [criar um site WordPress](https://intl.cloud.tencent.com/document/product/213/8044).

## Perguntas frequentes
Se você encontrar um problema ao usar o CVM, consulte os seguintes documentos para solucionar problemas com base em sua situação real.
- Para questões relacionadas ao login do CVM, consulte [Login de senha e login de chave SSH](https://intl.cloud.tencent.com/document/product/213/18120) e [Login e acesso remoto](https://intl.cloud.tencent.com/document/product/213/17278).
- Para questões relacionadas à rede CVM, consulte [Endereços IP](https://intl.cloud.tencent.com/document/product/213/17285) e [Portas e grupos de segurança](https://intl.cloud.tencent.com/document/product/213/2502).
- Para questões relacionadas aos discos CVM, consulte [Discos de sistema e discos de dados](https://intl.cloud.tencent.com/document/product/213/17351).




