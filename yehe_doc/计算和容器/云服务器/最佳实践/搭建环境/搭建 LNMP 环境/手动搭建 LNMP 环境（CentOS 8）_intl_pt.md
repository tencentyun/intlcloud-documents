## Visão geral
O ambiente LNMP é uma arquitetura de servidor de site que consiste em Nginx, MySQL ou MariaDB e PHP em execução no Linux. Este documento descreve como configurar manualmente o ambiente LNMP em um Tencent Cloud CVM.

Para configurar manualmente o ambiente LNMP, você deve se familiarizar com os comandos comuns do Linux e entender o uso e a compatibilidade de versão do software a ser instalado.

## Software
O seguinte software é usado para construir o ambiente LNMP.
O CentOS é uma distribuição do sistema operacional Linux. Este documento usa a versão CentOS 8.0 como exemplo.
O Nginx é um servidor web. Este documento usa o Nginx 1.18.0 como exemplo.
O MySQL é um software de banco de dados. Este documento usa o MySQL 8.0.21 como exemplo.
PHP é uma linguagem de script. Este documento usa o PHP 7.4.11 como exemplo.

## Pré-requisitos
Um CVM Linux é necessário para configurar um ambiente LNMP. Se você ainda não comprou um CVM Linux, consulte [Personalização das configurações do CVM Linux](https://intl.cloud.tencent.com/document/product/213/10517).

## Instruções
### Etapa 1: Fazer login em uma instância do Linux
Consulte [Fazer login na instância do Linux usando o método de login padrão](https://intl.cloud.tencent.com/document/product/213/5436). Você também pode usar outros métodos de login com os quais se sinta mais confortável:
- [Fazer login em instâncias do Linux por meio de ferramentas de login remoto](https://intl.cloud.tencent.com/document/product/213/32502)
- [Fazer login nas instâncias do Linux via chave SSH](https://intl.cloud.tencent.com/document/product/213/32501)

### Etapa 2: instalar e configurar o Nginx
1. Execute o seguinte comando para instalar o Nginx.
>?Este documento usa a instalação do Nginx 1.18.0 como exemplo. Você pode visualizar o [pacote de instalação do Nginx](http://nginx.org/packages/centos/8/x86_64/RPMS/?spm=a2c4g.11186623.2.31.557423bfYPMd6u) para obter mais versões compatíveis com o CentOS 8.
>
```
dnf -y install http://nginx.org/packages/centos/8/x86_64/RPMS/nginx-1.18.0-1.el8.ngx.x86_64.rpm
```
2. Execute o seguinte comando para visualizar a versão do Nginx.
```
nginx -v
```
Se o seguinte resultado for retornado, isso indica que o Nginx foi instalado com sucesso.
```
nginx version: nginx/1.18.0
```
3. Execute o seguinte comando para verificar o caminho do arquivo de configuração Nginx.
```
cat /etc/nginx/nginx.conf
```
O `/etc/nginx/conf.d/*.conf` no item de configuração `include` indica o caminho padrão do arquivo de configuração do Nginx.
4. Execute os comandos a seguir em sequência para fazer backup do arquivo de configuração no caminho padrão.
```
cd /etc/nginx/conf.d
```
```
cp default.conf default.conf.bak
```
5. Execute o seguinte comando para abrir o arquivo `default.conf`.
```
vim default.conf
```

6. Pressione **i** para alternar para o modo de edição visando modificar o arquivo `default.conf`.
  1. Adicione "index.php" ao `index` em `localização`, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/32df0b8ba82278cd96cf86152738677e.png)
  2. Exclua o prefixo `#` de `location ~  \\.php$` e modifique os seguintes itens de configuração:
    - Mude `root` para o diretório raiz do seu site. This document uses `/usr/share/nginx/html;` como exemplo.
    - Mude `fastcgi_pass` para `unix:/run/php-fpm/www.sock;`. Esta configuração deve ser igual a `listen` no arquivo `/etc/php-fpm.d/www.conf`, porque o Nginx está associado ao PHP-FPM através de soquetes UNIX.
    - Substitua `/scripts$fastcgi_script_name;` depois de `fastcgi_param  SCRIPT_FILENAME` por `$document_root$fastcgi_script_name;`.
    O resultado deve ser o seguinte:
![](https://main.qcloudimg.com/raw/2e4bff09d70399881bfbf995390a58d3.png) 
7. Pressione **Esc** e digite **:wq** para salvar e fechar o arquivo.
8. Execute os seguintes comandos em sequência para habilitar a inicialização automática do Ngnix.
```
systemctl start nginx
```
```
systemctl enable nginx
```

### Etapa 3: instalar e configurar o MySQL
1. Execute o seguinte comando para instalar o MySQL.
```
dnf -y install @mysql
```
2. Execute o seguinte comando para visualizar a versão do MySQL.
```
mysql -V
```
Se o seguinte resultado for retornado, isso indica que o MySQL foi instalado com sucesso.
```
mysql  Ver 8.0.21 for Linux on x86_64 (Source distribution)
```
3. Execute os seguintes comandos em sequencia para habilitar a inicialização automática do MySQL.
```
systemctl enable --now mysqld
```
```
systemctl status mysqld
```
4. Execute o seguinte comando para concluir as configurações de segurança e definir a senha do MySQL
```
mysql_secure_installation
```
Execute as seguintes etapas:
  1. Digite `y` e pressione **Enter** para iniciar as configurações.
  2. Escolha uma política de senha. Uma política de senha forte é recomendada. Digite `2` e pressione **Enter**.
    - 0: indica uma política flexível.
    - 1: indica uma política média.
    - 2: indica uma política rígida.
  3. Defina a senha para MySQL e pressione **Enter**. A senha que você digitou não será exibida por padrão.
  4. Digite novamente sua senha, pressione **Enter** e digite `y` para confirmar a senha.
  5. Digite `y` e pressione **Enter** para remover usuários anônimos.
  6. Configure se deseja desativar a conexão remota ao MySQL:
    - Sim: digite `y` e pressione **Enter**.
    - Não: digite `n` e pressione **Enter**.
  7. Digite `y` e pressione **Enter** para excluir a biblioteca de teste e acessar a permissão para ela.
  8. Digite `y` e pressione **Enter** para recarregar a tabela de autorização.

### Etapa 4: instalar e configurar o PHP
1. Execute os comandos a seguir em sequência para incluir e atualizar o repositório EPEL.
```
dnf -y install epel-release
```
```
dnf update epel-release
```
2. Execute os comandos a seguir em sequência para excluir o pacote de software desnecessário armazenado em cache e atualizar o repositório de software.
```
dnf clean all
```
```
dnf makecache
```
3. Execute o seguinte comando para instalar o repositório REMI.
>?Pule esta etapa se você instalar o PHP de uma versão diferente de 7.4.11.
>
```
dnf -y install https://rpms.remirepo.net/enterprise/remi-release-8.rpm
```
4. Execute o seguinte comando para iniciar o componente PHP 7.4.
```
dnf module install php:remi-7.4
```
5. Execute o seguinte comando para instalar os componentes PHP necessários.
```
dnf install php php-curl php-dom php-exif php-fileinfo php-fpm php-gd php-hash php-json php-mbstring php-mysqli php-openssl php-pcre php-xml libsodium
```
6. Execute o seguinte comando para visualizar a versão do PHP.
```
php -v
```
Se o seguinte resultado for retornado, isso indica que o PHP foi instalado com sucesso.
```
PHP 7.4.11 (cli) (built: Sep 29 2020 10:17:06) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies
    with Zend OPcache v7.4.11, Copyright (c), by Zend Technologies
```
7. Execute o seguinte comando para abrir o arquivo `www.conf`.
```
vi /etc/php-fpm.d/www.conf
```
8. Pressione **i** para mudar para o modo de edição e modifique o arquivo `www.conf`.
9. Altere `user = apache` para `user = nginx` e `group = apache` para `group = nginx`, como mostrado abaixo.
![](https://main.qcloudimg.com/raw/ceb9c202ebe56c9bd9265e86c0ad2333.png)
10. Pressione **Esc** e digite **:wq** para salvar e fechar o arquivo.
4. Execute os seguintes comandos em sequência para iniciar o PHP-FPM e habilitar a inicialização automática do PHP-FPM.
```
systemctl start php-fpm
```
```
systemctl enable php-fpm
```

## Verificação da configuração do ambiente.
1. Execute o seguinte comando para criar um arquivo de teste.
>? Este documento usa `/usr/share/nginx/html` que você configurou para o diretório raiz do seu site no Nginx como exemplo.
>
```
echo "<?php phpinfo(); ?>" >> /usr/share/nginx/html/index.php
```
2. Insira o seguinte URL em seu navegador e verifique se o ambiente foi configurado com sucesso. Para mais informações sobre como obter o endereço IP público, consulte [Obtenção de endereços IP públicos](https://intl.cloud.tencent.com/document/product/213/17940).
```
http://Public IP endereço da instância do CVM /index.php
```
Se aparecer o seguinte, o ambiente foi configurado com sucesso.
![](https://main.qcloudimg.com/raw/182c0f73df20d66216a9b73d571b2093.png)

## Operações relevantes
Depois que o ambiente LNMP for construído, você poderá [criar manualmente um site WordPress](https://intl.cloud.tencent.com/document/product/213/8044) para se familiarizar com o CVM e seus recursos.

## Perguntas frequentes

Se você encontrar um problema ao usar o CVM, consulte os seguintes documentos para solucioná-lo, conforme necessário:

- Para questões relacionadas ao login do CVM, consulte [Login de senha e login de chave SSH](https://intl.cloud.tencent.com/document/product/213/18120) e [Login e acesso remoto](https://intl.cloud.tencent.com/document/product/213/17278).
- Para questões relacionadas à rede CVM, consulte [Endereço IP](https://intl.cloud.tencent.com/document/product/213/17285) e [Porta](https://intl.cloud.tencent.com/document/product/213/2502).
- Para questões relacionadas aos discos CVM, consulte [Discos de sistema e dados](https://intl.cloud.tencent.com/document/product/213/17351).

