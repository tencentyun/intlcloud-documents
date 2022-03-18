## Introdução
LNMP se refere a uma arquitetura de servidor web comum que consiste em Nginx, MySQL ou MariaDB e PHP em execução no Linux. Este artigo descreve como implantar LNMP em um Tencent Cloud Virtual Machine (CVM).
É preciso instalar vários pacotes de software no Linux. Se não souber como executar a instalação do software no Linux, consulte [este artigo](https://intl.cloud.tencent.com/document/product/213/2047).

## Software
Este artigo usa o seguinte software para construir o ambiente LNMP:
- OS: openSUSE 42.3
- Servidor da web: Nginx 1.14.2
- Base de dados: MySQL 5.6.43
- Processador de hipertexto: PHP 7.0.7

##  Pré-requisitos
Você ter adquirido um CVM Linux. Se ainda não o fez, consulte [Introdução a CVMs Linux](http://intl.cloud.tencent.com/document/product/213/2936).

## Instruções
### Etapa 1: login em uma instância do Linux
- [Faça login em uma instância do Linux usando o modo de login padrão (recomendado)](https://intl.cloud.tencent.com/document/product/213/5436). Você também pode usar outros métodos de login, conforme necessário:
- [Faça login em uma instância do Linux usando software de login remoto](https://intl.cloud.tencent.com/document/product/213/32502).
- [Faça login em uma instância do Linux usando SSH](https://intl.cloud.tencent.com/document/product/213/32501).

### Etapa 2: Adicionar origem de imagem
1. Faça login no CVM.
2. Execute os seguintes comandos para adicionar a origem da imagem:
```
zypper ar https://mirrors.cloud.tencent.com/opensuse/distribution/leap/42.3/repo/oss suseOss
zypper ar https://mirrors.cloud.tencent.com/opensuse/distribution/leap/42.3/repo/non-oss suseNonOss
```
3. Execute o seguinte comando para atualizar a origem que acabou de adicionar.
```
zypper ref
```

### Etapa 3: Instalação e configuração do Nginx
1. Execute o seguinte comando para instalar o Nginx.
``` 
zypper install -y nginx
```
2. Execute o seguinte comando para iniciar o servidor Ngnix e defina-o para iniciar automaticamente quando o CVM for inicializado.
```
systemctl start nginx
systemctl enable nginx
```
3. Execute o seguinte para editar o arquivo de configuração Nginx.
```
Vi /etc/nginx/nginx.conf
```
4 Pressione **i** para alternar para o modo de edição.
5. Encontre **server{...}** e substitua pelo seguinte conteúdo:
```
server {
	listen       80;
	server_name  localhost;
	#access_log  /var/log/nginx/log/host.access.log  main;
	location / {
			root   /srv/www/htdocs/;
			index index.php index.html index.htm;
	}
	#error_page  404              /404.html;
	#redirect server error pages to the static page /50x.html
	error_page   500 502 503 504  /50x.html;
	location = /50x.html {
			root   /srv/www/htdocs/;
	}
	#pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    location ~ .php$ {
			root           /srv/www/htdocs/;
			fastcgi_pass   127.0.0.1:9000;
			fastcgi_index  index.php;
			fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
			include        fastcgi_params;
	}
}
```
7. Ao terminar, pressione **Esc** para sair do modo de edição. Em seguida, digite **:wq** para salvar o arquivo e sair do Vi.
8. Execute o seguinte comando para reiniciar o serviço Nginx.
```
systemctl restart nginx
```
9. Execute o seguinte comando para criar uma página de índice chamada `index.html`.
```
vi /srv/www/htdocs/index.html
```
10. Pressione **i** para alternar para o modo de edição e **digite** o seguinte.
```html
<p> hello world!</p>
```
11. Quando terminar, pressione **Esc** para sair do modo de edição. Em seguida, digite **:wq** para salvar o arquivo e sair do Vi.
12. Acesse o IP público do seu CVM no navegador para verificar se o seu Nginx está funcionando corretamente.
Se for exibido o seguinte, o Nginx foi instalado e configurado com êxito.
![](https://main.qcloudimg.com/raw/df09d1fe6baed50cebd89ef7402db4b2.png)

## Etapa 4: Instalação e configuração do MySQL
1. Execute o seguinte comando para instalar o MySQL.
```
zypper install -y mysql-community-server mysql-community-server-tools
```
2. Execute o seguinte comando para iniciar o serviço MySQL e defina-o para inicialização automática quando o CVM for inicializado.
```
systemctl start mysql 
systemctl enable mysql
```
3. Execute o seguinte comando para fazer login no MySQL.
> Ao fazer o login pela primeira vez, o MySQL solicitará que você configure uma senha. Se você não quiser fazer isso, pressione **Enter** para pular a etapa.
>
```
mysql -u root -p
```
Se o seguinte for exibido, você fez o login com sucesso.
![](https://main.qcloudimg.com/raw/1e9daf876fb08c70674789865688f695.png)
4. Execute o seguinte comando para alterar a senha do root.
```
update mysql.user set password = PASSWORD('NEW_PASSWORD') where user='root';
```
5. Execute o seguinte comando para aplicar a configuração:
```
flush privileges;
```
6. Execute o seguinte comando para sair do MySQL.
```
\q
```

### Etapa 5: Instalação PHP
Execute o seguinte comando para instalar o PHP:
```
zypper install -y php7 php7-fpm php7-mysql
```

### Etapa 6: Configuração do Nginx com PHP-FPM
1. Execute os seguintes comandos para navegar para `/etc/php7/fpm` e renomeie `php-fpm.conf.default` para `php-fpm.conf`.
```
cd /etc/php7/fpm
cp php-fpm.conf.default php-fpm.conf
``` 
2. Execute os seguintes comandos para navegar para `/etc/php7/fpm/php-fpm.d` e renomeie `www.conf.default` para `www.conf`.
```
cd /etc/php7/fpm/php-fpm.d
cp www.conf.default www.conf
```
3. Execute os seguintes comandos para iniciar o PHP-FPM e defina-o para inicialização automática quando o CVM for inicializado.
```
systemctl start php-fpm
systemctl enable php-fpm
```

## Verificação de configuração
1. Execute o seguinte comando para criar um arquivo denominado index.php.
```
Vi /srv/www/htdocs/index.php
```
2. Pressione **i** para alternar para o modo de edição e digite o seguinte:
```
<?php
	echo "hello new world!";
?>
```
3. Pressione **Esc** para sair do modo de edição. Em seguida, digite **:wq** para salvar o arquivo e sair.
4. Acesse o IP público do seu CVM no navegador.
Se o seguinte for exibido, sua configuração LNMP foi instalada e configurada com sucesso.
![](https://main.qcloudimg.com/raw/0adc6168e7407931c597228520b35413.png)

## Consulte também
Depois que o ambiente LNMP for construído, você pode usá-lo para [configurar um site WordPress](https://intl.cloud.tencent.com/document/product/213/8044) para se familiarizar com seu CVM e o que ele pode fazer.

## Perguntas frequentes
Se você encontrar problemas ao usar o CVM, consulte os seguintes documentos para solução de problemas:
Para questões relacionadas ao login do CVM, consulte [Login de senha e de chave SSH](https://intl.cloud.tencent.com/document/product/213/18120) e [Login e acesso remoto](https://intl.cloud.tencent.com/document/product/213/17278).
Para questões relacionadas à rede do CVM, consulte [Endereços IP](https://intl.cloud.tencent.com/document/product/213/17285) e [Portas e grupos de segurança](https://intl.cloud.tencent.com/document/product/213/2502).
Para questões relacionadas aos discos CVM, consulte [Discos de sistema e dados](https://intl.cloud.tencent.com/document/product/213/17351).



