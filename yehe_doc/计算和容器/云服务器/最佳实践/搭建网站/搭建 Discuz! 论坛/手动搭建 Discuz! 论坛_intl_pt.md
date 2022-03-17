## Visão geral

Utilizado em mais de 2 milhões de sites, o Discuz! é o software de fórum mais sofisticado e predominante do mundo. Este documento descreve como criar um site usando o Discuz! na instância Tencent Cloud CVM e implementar o ambiente de tempo de execução LAMP (Linux, Apache, MariaDB e PHP) necessário.


Para configurar manualmente um site Discuz!, você deve estar familiarizado com os comandos comuns do Linux (consulte [Instalação do software via YUM no ambiente CentOS](https://intl.cloud.tencent.com/document/product/213/2046), e entender o uso e a compatibilidade da versão do software a ser instalado.
## Software
O seguinte software é usado para desenvolver um site Discuz!.
- Linux: Sistema operacional Linux. Este documento usa a versão CentOS 7.6 como exemplo.
- Apache: Software de servidor da web. Este documento usa o Apache 2.4.15 como exemplo.
- MariaDB: banco de dados. Este documento usa o MariaDB 5.5.60 como exemplo.
- PHP: linguagem de script. Este documento usa o PHP 5.4.16 como exemplo.
- Discuz!: software de fórum. Este documento usa o Discuz! X3.4 como um exemplo.


## Instruções
### Etapa 1: fazer login no CVM
Consulte [Fazer login na instância do Linux usando o método de login padrão](https://intl.cloud.tencent.com/document/product/213/5436). Você também pode usar outros métodos de login com os quais se sinta mais confortável:

- [Faça login em instâncias do Linux por meio de ferramentas de login remoto](https://intl.cloud.tencent.com/document/product/213/32502).
- [Faça login em instância do Linux via chave SSH](https://intl.cloud.tencent.com/document/product/213/32501)



### Etapa 2: configurar o ambiente LAMP 

O Tencent Cloud hospeda um repositório de software que contém lançamentos oficiais CentOS e fornece a versão mais recente e estável. Use o Yum para instalar rapidamente o CentOS.

<span id="InstallNecessarySoftware"></span>
#### Instalação e configuração do software necessário
1. Execute o seguinte comando para instalar o Apache, MariaDB, PHP e Git:
```
yum install httpd php php-fpm php-mysql mariadb mariadb-server git -y
```
2. Execute os seguintes comandos em sequência para iniciar os serviços.
```
systemctl start httpd
```
```
systemctl start mariadb
```
```
systemctl start php-fpm
```
3. <span id="step3"></span>Execute o seguinte comando para definir uma senha para o usuário `root` e concluir outras configurações básicas, para que o usuário raiz possa acessar o banco de dados.
>!
>- Execute o seguinte comando para definir a senha antes de seu primeiro login no MariaDB.
>- Ao visualizar a solicitação para digitar a senha raiz, pressione Enter para definir a senha. Sua senha não será exibida por padrão. Conclua outras configurações básicas conforme solicitado.
> 
```
mysql_secure_installation
```
4. Execute o seguinte comando para fazer login no MariaDB. Digite a senha que você definiu na [etapa 3](#step3) e pressione **Enter**.
```
mysql -u root -p
```
Um login bem-sucedido é mostrado abaixo:
![](https://main.qcloudimg.com/raw/18c54971e141db38c3f483161fefe251.png)

5. Execute o seguinte comando para sair do MariaDB.
```
\q
```

#### Verificação da configuração do ambiente

Verifique se o ambiente está configurado corretamente conforme as instruções abaixo:
1. Execute o seguinte comando para criar um arquivo de teste `test.php` no diretório raiz padrão `/var/www/html` do Apache:
```
vim /var/www/html/test.php
```
2. Pressione **i** para alternar para o modo de edição e insira o seguinte conteúdo:
```
<?php
echo "<title>Test Page</title>";
phpinfo()
?>
```
3. Pressione **Esc** e digite **:wq** para salvar e fechar o arquivo.
4. Insira o seguinte URL em um navegador para acessar `test.php` e verificar se o ambiente está configurado corretamente.
```
http://[endereço IP público do CVM]/test.php 
```
Se tudo correr bem, aparecerá o seguinte.
![](https://main.qcloudimg.com/raw/f511b15ac3016d710c2b1f833e69448d.png)



<span id="InstallDiscuz"></span>
### Etapa 3: instalação e configuração do Discuz!  

#### Fazer download do Discuz! 
Execute o seguinte comando para fazer download do pacote de instalação.
```
git clone https://gitee.com/Discuz/DiscuzX.git
```

#### Preparação para a instalação
1. Execute o seguinte comando para acessar o diretório de instalação.
```
cd DiscuzX
```
2. Execute o seguinte comando para copiar todos os arquivos em "upload" para "/var/www/html/".
```
cp -r upload/* /var/www/html/
```
3. Execute o seguinte comando para conceder aos usuários a permissão de gravação.
```
chmod -R 777 /var/www/html
```

#### Instalação do Discuz!
1. Digite o endereço IP do seu site Discuz! (o endereço IP público de sua instância CVM) na caixa de endereço, ou você pode [vincular um nome de domínio disponível](#ConfigureDomain) ao seu endereço IP.
2. Clique em **I agree (Concordo)** e vá para a página de verificação do ambiente.
3. Verifique os itens e clique em **Next Step (Próxima etapa)**.
4. Selecione **Clean Install (Limpar instalação)** e clique em **Next Step (Próxima etapa)**.
5. Insira as informações solicitadas para criar um novo banco de dados para Discuz!.
>!  
>- Use `root` e a senha definida em [Instalação e configuração do software necessário](#InstallNecessarySoftware) para se conectar ao banco de dados e configurar um endereço de e-mail do sistema e nome de usuário, senha e endereço de e-mail do administrador.
>- Lembre-se de seu nome de usuário e senha de administrador.
>
6. Clique em **Next Step (Próxima etapa)** para iniciar a instalação.
7. Após a instalação, clique em **Your forum has been installed successfully. Click here to access (Seu fórum foi instalado com sucesso. Clique aqui para acessar).** para acessar seu fórum.

<span id="ConfigureDomain"></span>
## Uso de um nome de domínio
Usar um nome de domínio em vez de um IP pode ajudar os usuários a se lembrarem de seu site com mais facilidade.

## Perguntas frequentes
Verifique a documentação a seguir para conferir problemas na utilização do CVM: 
- Login no CVM: [Login de senha e login de chave SSH](https://intl.cloud.tencent.com/document/product/213/18120) e [Login e acesso remoto](https://intl.cloud.tencent.com/document/product/213/17278)
- Rede CVM: [Endereço IP](https://intl.cloud.tencent.com/document/product/213/17285) e [Porta](https://intl.cloud.tencent.com/document/product/213/2502)
- Discos CVM: [Sistema e discos de dados](https://intl.cloud.tencent.com/document/product/213/17351)



