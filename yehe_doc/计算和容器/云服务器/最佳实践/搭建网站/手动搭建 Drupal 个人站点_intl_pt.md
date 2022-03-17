## Cenário
Drupal é uma estrutura de gerenciamento de conteúdo de código aberto, gratuita, escrita em PHP e distribuída sob a GNU General Public License. O Drupal fornece uma estrutura de back-end para pelo menos 2,3% de todos os sites do mundo - variando de blogs pessoais a sites corporativos. Este artigo descreve como configurar o Drupal manualmente em um CVM. 

Para configurar manualmente um site pessoal baseado em Drupal, você precisa estar familiarizado com os comandos do Linux, como [usar o YUM para instalar software no CentOS](https://intl.cloud.tencent.com/document/product/213/2046). Também é preciso estar familiarizado com o uso e a compatibilidade do software.

## Software
Este artigo descreve como instalar o seguinte software
- Sistemas operacionais Linux. Este artigo usa o CentOS 7.6.
- Apache é um software de servidor web. Este artigo usa o Apache 2.4.6.
- MariaDB é um sistema de gerenciamento de banco de dados. Este artigo usa MariaDB 10.4.8.
- PHP é uma linguagem de script. Este artigo usa PHP 7.0.33.
- Drupal é uma estrutura de gerenciamento de conteúdo Este artigo usa Drupal 8.1.1.


## Pré-requisitos
Você precisa de um CVM Linux. Se você ainda não comprou um, consulte [este artigo](http://intl.cloud.tencent.com/document/product/213/2936) para obter informações sobre como começar a usar um CVM Linux.


## Instruções
### Etapa 1 Login em uma instância do Linux
[Faça login em uma instância do Linux usando WebShell (recomendado)](https://intl.cloud.tencent.com/document/product/213/5436). Você também pode usar outros métodos de login com os quais se sinta confortável:
- [Faça login em uma instância do Linux usando software de login remoto](https://intl.cloud.tencent.com/document/product/213/32502).
- [Faça login em uma instância do Linux usando SSH](https://intl.cloud.tencent.com/document/product/213/32501)

### Etapa 2 Configuração de LAMP
Depois de fazer o login, configure o LAMP para que você possa executar o Drupal. Consulte [este artigo](https://intl.cloud.tencent.com/document/product/213/34813) para obter detalhes.

### Etapa 3 Fazer download e instalar o Drupal
1. Execute os comandos a seguir para baixar o pacote de instalação do Drupal para o diretório raiz do seu site.
```
cd /var/www/html/
```
```
wget wget http://ftp.drupal.org/files/projects/drupal-8.1.1.zip
```
2. Execute os comandos a seguir para descompactar o pacote de instalação e renomear o diretório.
```
unzip drupal-8.1.1.zip 
```
```
mv drupal-8.1.1/ drupal/
```

### Etapa 4 Configuração do Drupal 
1. Execute o seguinte comando para abrir o arquivo de configuração do Apache.
```
vi /etc/httpd/conf/httpd.conf
```
2. Pressione **i** para entrar no modo de edição. Encontre `AllowOverride None` em `Directory "/var/www/html"></Directory>` e substitua-o pelo seguinte:
```
AllowOverride All
```
O resultado é apresentado abaixo:
![](https://main.qcloudimg.com/raw/c68f918f22d9c29607d59fe1847eff69.png)
3. Pressione **Esc** para sair do modo de edição e digite **:wq** para salvar o arquivo e retornar.
4. Execute o seguinte comando para alterar a permissão de acesso do diretório raiz do site para o usuário `apache`.
```
chown -R apache:apache /var/www/html
```
5. Execute o seguinte comando para reinicializar o serviço Apache.
```
systemctl restart httpd
```

#### Configuração de uma base de dados para Drupal<span id="database"></span>
>As instruções para configurar as credenciais do usuário MariaDB podem variar dependendo das diferentes versões. Consulte [site oficial do MariaDB](https://downloads.mariadb.org/) para obter detalhes.
>
1. Execute o seguinte comando para entrar no MariaDB.
```
mysql
```
2. Execute o seguinte comando para criar um banco de dados chamado `drupal`.
```
CREATE DATABASE drupal;
```
3. Execute o seguinte comando para criar um novo usuário `user` e defina sua senha para `123456`.
```
CREATE USER 'user'@'localhost' IDENTIFIED BY '123456';
```
4. Execute o seguinte comando e atribua ao `user` todos os privilégios para` drupal`.
```
GRANT ALL PRIVILEGES ON drupal.* TO 'user'@'localhost' IDENTIFIED BY '123456';
```
5. Execute o seguinte comando para aplicar todas as configurações.
```
FLUSH PRIVILEGES;
```
6. Execute o seguinte comando para sair do MariaDB.
```
\q
```

#### Configuração `root`
1.  Execute o seguinte comando para entrar no MariaDB.
```
mysql
```
2. Execute o seguinte comando para definir uma senha para `root`.
>MariaDB 10.4 for CentOS agora permite que a conta `root` efetue login sem senha. Execute o seguinte comando para definir uma senha para `root` e registre-a em um local seguro.
>
```
ALTER USER root@localhost IDENTIFIED VIA mysql_native_password USING PASSWORD('your_pasword');
```
3. Execute o seguinte comando para sair do MariaDB.
```
\q
```

### Etapa 5 Instalação e configuração do Drupal
1. Abra uma janela do navegador em sua máquina local e visite o seguinte endereço para instalar o Drupal.
```
http://CVM_Public_IP/drupal
```
2. Selecione o idioma de sua preferência e clique em **Save and continue (Salvar e continuar)**
3. Selecione **Standard installation (Instalação padrão)** e clique em **Save and continue (Salvar e continuar)**
4. Insira informações relevantes do banco de dados configuradas em [Configuração de um banco de dados para Drupal](#database). Clique em **Save and continue (Salvar e continuar)**
>A instalação do Drupal agora verifica se todos os critérios de instalação foram atendidos. Nesse caso, a instalação é iniciada. Caso contrário, mensagens de erro serão exibidas. Resolva-os antes de continuar.
>

5. A página de configuração é carregada automaticamente após a conclusão da instalação. Insira as informações e clique em **Save and continue (Salvar e continuar)**
>Registre seu nome de usuário e senha de manutenção.
>

6. A página inicial do seu Drupal carrega automaticamente. Use o nome de usuário e senha de manutenção para fazer login
Agora você configurou com sucesso o seu site Drupal. Personalize sua experiência como achar melhor.

## Perguntas frequentes
Se você encontrar um problema ao usar o CVM, consulte os seguintes documentos para solucionar problemas com base em sua situação real.
- Para questões relacionadas ao login do CVM, consulte [Login de senha e login de chave SSH](https://intl.cloud.tencent.com/document/product/213/18120) e [Login e acesso remoto](https://intl.cloud.tencent.com/document/product/213/17278).
- Para questões relacionadas à rede CVM, consulte [Endereços IP](https://intl.cloud.tencent.com/document/product/213/17285) e [Portas e grupos de segurança](https://intl.cloud.tencent.com/document/product/213/2502).
- Para questões relacionadas aos discos CVM, consulte [Discos de sistema e dados](https://intl.cloud.tencent.com/document/product/213/17351).
