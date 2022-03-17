## Cenário
Ghost é uma plataforma de blog de código aberto gratuita, escrita em JavaScript e distribuída sob a licença MIT, projetada para simplificar o processo de publicação online para blogueiros, bem como para publicações online. Este artigo descreve como configurar o Ghost em um CVM. 

Para configurar o Ghost, você deve estar familiarizado com o Linux e seus comandos comuns, como [Instalar software via Apt-get no ambiente Ubuntu](https://intl.cloud.tencent.com/document/product/213/2123).

## Software
Este artigo usa o seguinte software:
- Sistemas operacionais Linux. Este artigo usa o Ubuntu 18.04.
- Nginx 1.14.0 é usado para fornecer serviço da web.
- MySQL 5.7.27 é usado para banco de dados.
- Node.js 10.17.0 é nosso ambiente de tempo de execução.
- Ghost 3.0.2


##  Pré-requisitos
É preciso possuir um CVM Linux. Se você ainda não comprou um, consulte [Introdução aos CVMs Linux](http://intl.cloud.tencent.com/document/product/213/2936).
- Um nome de domínio que aponta para o seu CVM. Se o nome de domínio for usado para o serviço na China Continental, o preenchimento do ICP é necessário.



## Instruções

### Etapa 1 Login em uma instância do Linux
- [Faça login em uma instância do Linux usando WebShell (recomendado)](https://intl.cloud.tencent.com/document/product/213/5436). Você também pode usar outros métodos de login com os quais se sinta confortável:
- [Faça login em uma instância do Linux usando software de login remoto](https://intl.cloud.tencent.com/document/product/213/32502).
- [Faça login em uma instância do Linux usando SSH](https://intl.cloud.tencent.com/document/product/213/32501)

### Etapa 2 Criar um novo usuário
1. Após fazer o login, mude para `root`. Consulte [este artigo](https://intl.cloud.tencent.com/document/product/213/17278) para obter detalhes.
2. Execute o seguinte comando para criar um usuário chamado `user`.
>Não use `ghost` como nome de usuário. Isso causa conflitos com o Ghost-CLI. 
>
```
adduser user
```
 1. Insira e confirme a senha conforme solicitado. A senha não é mostrada por padrão. Pressione **Enter** para continuar.
 2. Insira as informações do usuário. Ou pressione **Enter** para ignorá-las e continuar.
 3. Insira **Y** para confirmar e pressione **Enter** para concluir o processo, conforme mostrado abaixo:
 ![](https://main.qcloudimg.com/raw/66ca399607b89f2653668eb4b0cb71f5.png)
3. Execute o seguinte comando para adicionar privilégios de usuário.
```
usermod -aG sudo user
```
4. Execute o seguinte comando para mudar para o usuário `user`.
```
su user
```

### Etapa 3 Atualizar os pacotes instalados
Execute os seguintes comandos para atualizar os pacotes instalados.
>Insira a senha para `user` conforme solicitado e pressione **Enter** para iniciar.
>
```
sudo apt-get update
```
```
sudo apt-get upgrade -y
```

### Etapa 4 Configurar o ambiente
#### Instalação do Nginx
Execute o seguinte comando para instalar o Nginx.
```
sudo apt-get install -y nginx 
```

#### Instalação e configuração do MySQL
1. Execute o seguinte comando para instalar o MySQL.
```
sudo apt-get install -y mysql-server 
```
2. Execute o seguinte comando para fazer login no MySQL.
```
sudo mysql
```
3. <span id="database"></span>Execute o seguinte comando para criar um banco de dados para o Ghost chamado `ghost_data`.
```
CREATE DATABASE ghost_data;
```
4. <span id="sercet"></span>Execute o seguinte comando para definir uma senha para o usuário do banco de dados `root`.
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your_password';
```
5. Execute o seguinte comando para sair do MySQL.
```
\q
```

#### Instalar o Node.js
1. Execute o seguinte comando para definir uma versão Node.js padrão a ser usada.
```
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash
```
2. Execute o seguinte comando para instalar o Node.js.
```
sudo apt-get install -y nodejs
```

#### Instalação do Ghost-CLI
Execute o seguinte comando para instalar o Ghost-CLI, o que ajuda a configurar o Ghost.
```
sudo npm install ghost-cli@latest -g
```

### Etapa 5 Instalar e configurar o Ghost
1. Execute os seguintes comandos.
```
sudo mkdir -p /var/www/ghost
```
```
sudo chown user:user /var/www/ghost
```
```
sudo chmod 775 /var/www/ghost
```
```
cd /var/www/ghost
```
2. Execute o seguinte comando para instalar o Ghost.
```
ghost install
```
3. Use a imagem a seguir para concluir o processo de instalação.
![](https://main.qcloudimg.com/raw/6c3a3b9d083dfb253285f47d81e928b5.png)
 1. **Enter your blog URL**: insira o seu nome de domínio no formato `http://your_domain_name`.
 2. **Enter your MySQL hostname**: insira o endereço do seu banco de dados. Use `localhost` neste caso e pressione **Enter**.
 3. **Enter your MySQL username**: insira o nome de usuário que você usa para se conectar ao MySQL. Use `root` neste caso e pressione **Enter**.
 4. **Enter your MySQL password**: insira a senha correspondente que você definiu [anteriormente](#secret) e pressione **Enter**.
 5. **Enter your database name**: insira o nome do banco de dados que você criou para o Ghost [na etapa anterior](#bancodedados). Use `ghost_data` e pressione **Enter**.
 6. Insira **Y** ou **N** para completar a configuração.
 O URL do administrador aparece na parte inferior da tela.
4. Abra uma janela do navegador em sua máquina local e visite o URL de administrador para começar a configurar seu blog.
Clique em para criar **Create account (Criar conta)**uma conta de administrador.
![](https://main.qcloudimg.com/raw/e2eeacd71eec4c27660eeb4797f83f2a.png)
5. Insira as informações desejadas e clique em **Last step (Última etapa)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/a7a81f16b811bdceeb429116ee23081c.png)
6. Você pode convidar outras pessoas para criarem blogs ou pode pular esta etapa.
7. Acesse a página de administração para gerenciar blogs, conforme mostrado abaixo: 
![](https://main.qcloudimg.com/raw/fd9071dba9748ce8125f8597be0d248a.png)
Quando terminar, use um navegador para visitar seu nome de domínio `www.xxxxxxxx.xx` para ver seu blog, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/055decab4524eb9f2f5602fbd0502c7c.png)

## Perguntas frequentes
Se você encontrar um problema ao usar o CVM, consulte os seguintes documentos para solucionar problemas com base em sua situação real.
- Para questões relacionadas ao login do CVM, consulte [Login de senha e login de chave SSH](https://intl.cloud.tencent.com/document/product/213/18120) e [Login e acesso remoto](https://intl.cloud.tencent.com/document/product/213/17278).
- Para questões relacionadas à rede CVM, consulte [Endereços IP](https://intl.cloud.tencent.com/document/product/213/17285) e [Portas e grupos de segurança](https://intl.cloud.tencent.com/document/product/213/2502).
- Para questões relacionadas aos discos CVM, consulte [Discos de sistema e dados](https://intl.cloud.tencent.com/document/product/213/17351).
