## Cenário
WordPress é uma plataforma de blog desenvolvida em PHP. Este documento descreve como construir manualmente um site WordPress privado em um Tencent Cloud CVM com CentOS 7.6.

Para construir um site WordPress, você deve estar familiarizado com os comandos comuns do Linux, como aqueles para [instalar software por meio do YUM no ambiente CentOS](https://intl.cloud.tencent.com/document/product/213/2046). Além disso, você precisa saber como usar os programas de software envolvidos e os detalhes de compatibilidade de versão.

## Software
Os seguintes programas de software são usados ​​para construir o site WordPress:
- Linux: Sistema operacional Linux. Este documento usa a versão CentOS 7.6 como exemplo.
- Nginx: web server. Este documento usa o Nginx 1.17.5 como exemplo.
- MariaDB: banco de dados. Este documento usa o MariaDB 10.4.8 como exemplo.
- PHP: linguagem de script. Este documento usa o PHP 7.2.22 como exemplo.
- WordPress: plataforma de blog. Este documento usa o WordPress 5.0.4 como exemplo.

## Instruções 
### Etapa 1: Faça login no CVM
[Faça login em uma instância do Linux usando WebShell (recomendado)](https://intl.cloud.tencent.com/document/product/213/5436). Também é possível usar qualquer um dos métodos de login a seguir, de acordo com sua preferência.
- [Faça login em uma instância do Linux usando ferramentas de login remoto](https://intl.cloud.tencent.com/document/product/213/32502)
- [Faça login em uma instância do Linux usando a chave SSH](https://intl.cloud.tencent.com/document/product/213/32501)



### Etapa 2: Construir manualmente um ambiente LNMP
LNMP é a sigla para Linux, Nginx, MariaDB e PHP. É um dos ambientes de tempo de execução mais comuns para servidores da web. Depois de criar e fazer login em uma instância do CVM, você pode construir um ambiente LNMP consultando [Construção manual de um ambiente LNMP (CentOS 7)](https://intl.cloud.tencent.com/document/product/213/32733).

<span id="database"></span>
### Etapa 3: Configurar o banco de dados WordPress
>O método de autenticação do usuário varia dependendo da versão do MariaDB. Para obter detalhes, visite o site oficial do MariaDB.
>
1. Execute o seguinte comando para acessar o MariaDB:
```
mysql
```
2. Execute o seguinte comando para criar um banco de dados MariaDB, como `wordpress` neste exemplo:
```
CREATE DATABASE wordpress;
```
3. Execute o seguinte comando para criar um usuário e especificar uma senha, como o usuário `user` com a senha `123456`, neste exemplo:
```
CREATE USER 'user'@'localhost' IDENTIFIED BY '123456';
```
4. Execute o seguinte comando para conceder ao `user` todas as permissões para o banco de dados` wordpress`:
```
GRANT ALL PRIVILEGES ON wordpress.* TO 'user'@'localhost' IDENTIFIED BY '123456';
```
5. Execute o seguinte comando para que todas as configurações tenham efeito:
```
FLUSH PRIVILEGES;
```
6. Execute o seguinte comando para sair do MariaDB:
```
\q
```

### Etapa 4: Configure uma conta `root`
1. Execute o seguinte comando para acessar o MariaDB:
```
mysql
```
2. Execute o seguinte comando para definir uma senha para `root`:
> O MariaDB 10.4 para CentOS permite que seja efetuado login na conta `root` sem uma senha. Execute o seguinte comando para definir uma senha para `root` e salve-a em um local seguro:
>
```
ALTER USER root@localhost IDENTIFIED VIA mysql_native_password USING PASSWORD('Insira sua senha');
```
3. Execute o seguinte comando para sair do MariaDB:
```
\q
```


### Etapa 5: Instalar e configurar o WordPress
#### Fazer dowload do WordPress
> É possível fazer download da versão mais recente no site oficial do WordPress.
>
1. Execute o seguinte comando para excluir o arquivo `index.php` que é usado para testar a configuração do PHP-Nginx do diretório raiz do site:
```
rm -rf /usr/share/nginx/html/index.php
```
2. Execute os seguintes comandos para navegar até o diretório `/usr/share/nginx/html/`, faça download e descompacte o pacote de instalação do WordPress:
```
cd /usr/share/nginx/html
wget https://cn.wordpress.org/wordpress-5.0.4-zh_CN.tar.gz
tar zxvf wordpress-5.0.4-zh_CN.tar.gz
```


#### Modificar o arquivo de configuração do WordPress
1. Execute os seguintes comandos para navegar até o diretório de instalação do WordPress, copie o conteúdo do arquivo `wp-config-sample.php` para o arquivo `wp-config.php` e salve o arquivo de configuração original para backup:
```
cd /usr/share/nginx/html/wordpress
cp wp-config-sample.php wp-config.php
```
2. Execute o seguinte comando para abrir e editar o novo arquivo de configuração:
```
vim wp-config.php
```
3. Pressione **i** para entrar no modo de edição. Encontre a seção MySQL no arquivo e modifique as configurações conforme descrito em [Configuração do banco de dados WordPress](#database).
```
	// ** Configurações MySQL - Você pode obter esta informação do seu host da web ** //
	/** O nome do banco de dadso para WordPress */
	define('DB_NAME', 'wordpress');
	
	/** Nome de usuário do banco de dados MySQL */
	define('DB_USER', 'user');
	
	/** Senha do banco de dados MySQL */
	define('DB_PASSWORD', '123456');
	
	/** Nome do host MySQL */
	define('DB_HOST', 'localhost');
```
4. Após terminar a modificação, pressione **Esc** e digite **:wq**. Em seguida, salve as alterações e feche o arquivo.

### Etapa 6: Verifique a instalação do WordPress
1. Na caixa de endereço do navegador, digite `http://<Domain name or public IP address of the CVM instance>/<WordPress folder>`, por exemplo:
```
http://192.xxx.xxx.xx/wordpress
```
Pressione **Enter** para ir para a página de instalação do WordPress e configurá-lo.

2. Preencha as seguintes informações de instalação conforme instruído no assistente de instalação do WordPress. Em seguida, clique em **Install WordPress (Instalar WordPress)**.
<table>
	<th style="width: 18%;">Informação necessária</th>
	<th style="width: 25%;">Descrição</th>
					<tr>
					<td>
							Título do site
					</td>
					<td>
							Nome do site WordPress
					</td>
			</tr>
				<tr>
					<td>
							Nome do usuário
					</td>
					<td>
							Nome do administrador do WordPress. Por motivos de segurança, use um nome diferente de admin, que pode ser crackeado.
					</td>
			</tr>
			<tr>
					<td>
							Senha
					</td>
					<td>
							Use a senha forte padrão ou uma senha personalizada. Não use senhas anteriores e salve a senha em um local seguro.
					</td>
			</tr>
				<tr>
					<td>
							Endereço de e-mail
					</td>
					<td>
							Endereço de e-mail para receber notificações
					</td>
			</tr>
	</table>
Agora, você pode fazer login no seu site WordPress e publicar blogs.

## Operações relevantes
É possível definir um nome de domínio para o seu site WordPress. Dessa forma, os usuários podem usar o nome de domínio em vez de um endereço IP complexo para visitar seu site. Se você estiver construindo o site para fins de aprendizado, poderá definir um endereço IP para o site. No entanto, essa prática não é recomendada para outros casos.

## Perguntas frequentes
Se você encontrar problemas ao usar um CVM, consulte os seguintes documentos para solucionar problemas com base em sua situação real.
- Para questões relacionadas ao login do CVM, consulte [Login de senha e login de chave SSH](https://intl.cloud.tencent.com/document/product/213/18120) e [Login e acesso remoto](https://intl.cloud.tencent.com/document/product/213/17278).
- Para questões relacionadas à rede CVM, consulte [Endereços IP](https://intl.cloud.tencent.com/document/product/213/17285) e [Portas e grupos de segurança](https://intl.cloud.tencent.com/document/product/213/2502).
- Para questões relacionadas aos discos CVM, consulte [Discos de sistema e dados](https://intl.cloud.tencent.com/document/product/213/17351).

