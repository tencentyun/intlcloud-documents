## Introdução
WordPress é uma plataforma de blog escrita em PHP. Este artigo descreve como instalar o WordPress no Windows Server 2012.

## Software
Embora o PHP, versão 5.6.20 e posterior, e o MySQL, versão 5.0 e posterior, sejam compatíveis com o WordPress, recomendamos o uso de PHP 7.3 e MySQL 5.6 ou versões posteriores por motivos de segurança.

Estes são os softwares envolvidos:
- Sistema operacional: Windows Server 2012
- Servidor da web: IIS 8.5
- Base de dados: MySQL 5.6.46
- Intérprete de hipertexto: PHP 7.3.12
- Plataforma de blog: WordPress 5.3


## Procedimento

### Etapa 1: Fazendo login no CVM do Windows
- [Entrar em um CVM do Windows usando um arquivo RDP (recomendado)](http://intl.cloud.tencent.com/document/product/213/5435)
- [Entrar em um CVM do Windows usando uma área de trabalho remota](https://intl.cloud.tencent.com/document/product/213/32498)

### Etapa 2: Configuração de WIMP
1. Instale o IIS.
2. Implemente o PHP 5.6.20 ou posterior.
3. Instale o MySQL 5.6 ou posterior.

### Etapa 3: Instalação e configuração de WordPress
> É possível fazer download da versão mais recente no site oficial do WordPress.
>

1. Baixe o WordPress e descompacte-o em um diretório do CVM.
Por exemplo, você pode descompactá-lo para `C:\wordpress`.
2. Clique com o botão direito do mouse em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;">. Digite **cmd** em **Run (Executar)** e pressione **Enter** para abrir uma janela de linha de comando.
3. Execute os seguintes comandos na janela de linha de comando para criar um banco de dados para WordPress.
Por exemplo, crie um banco de dados chamado `wordpress`.
```
create database wordpress;
```
4. Encontre `wp-config-sample.php` em `C:\wordpress` e renomeie-o como `wp-config.php`.
5. Use um editor de texto para abrir `wp-config.php` e editar as informações de configuração conforme detalhado na [Etapa 4: Instalação do MySQL](#Step04).
6. Salve `wp-config.php`.
7. Clique em <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> para abrir o **Server Manager (Gerenciador do servidor)**.
8. No painel de navegação à esquerda, selecione **IIS**. Clique com o botão direito do mouse no nome do servidor na coluna **Server (Servidor)** e selecione **Internet Information Services (IIS) Manager (Gerenciador de serviços de informação da Internet (IIS))** para abrir a janela **Internet Information Services (IIS) Manager (Gerenciador de serviços de informação da Internet (IIS))**.
9. Na janela **Internet Information Service (IIS) Manager (Gerenciador de serviços de informação da Internet (IIS))**, expanda seu servidor no painel de navegação esquerdo e selecione seu site. Isso abre a página de gerenciamento do site.
10. Exclua sites vinculados à porta 80.
Você pode alterar a porta para outra que não esteja sendo usada, como a 8080.
11. Clique em **Add Website (Adicionar site)**.
12. Insira as informações necessárias e clique em **OK**.
 - Website name (Nome do site): nome do site, como `wordpress`.
 - Application pool (Conjunto de aplicativos): selecione **DefaultAppPool**.
 - Physical path (Caminho físico): o diretório que contém o WordPress, como `C:\wordpress`.
13. Encontre `php.ini` no diretório que contém o PHP. Abra-o com um editor de texto e faça as seguintes alterações:
 1. As mudanças necessárias são diferentes a depender da versão do PHP.
     - Para PHP 5.x, encontre `extension = php_mysql.dll` e exclua o `;` no início.
     - Para PHP 7.x, encontre `extension = php_mysqli.dll` e exclua o `;` no início.
 2. Encontre `extension_dir= "ext"` e exclua o `;` no início.
14 Salve `php.ini`.

### Etapa 4: Verificação da configuração do WordPress

1. Abra uma janela do navegador em sua máquina local e acesse `http://localhost/wp-admin/install.php`. A página de instalação do WordPress é exibida.
2. Insira as informações conforme solicitado pelo assistente de instalação. Clique em **Install Wordpress (Instalar WordPress)** para concluir o processo.
<table>
	<tr><th>Informação </th><th>Descrição</th></tr>
	<tr><td>Website Name (Nome do site)</td><td>Nome do site do WordPress.</td></tr>
	<tr><td>User Name (Nome do usuário)</td><td>Nome da conta do administrador do WordPress. Por razões de segurança, use um nome diferente de `admin`.</td></tr>
	<tr><td>Password (Senha)</td><td>Use uma senha forte, diferente da senha atual. Guarde-a em um local seguro.</td></tr>
	<tr><td>Email</td><td>Endereço de e-mail usado para receber notificações</td></tr>
</table>
Agora, é possível fazer login no site do seu blog WordPress e publicar blogs.

## Uso de um nome de domínio

Use um nome de domínio que torne seu site mais fácil de lembrar. Recomendamos que você obtenha um nome de domínio e configure-o para apontar para seu site WordPress. Caso esteja instalando o WordPress apenas para aprender o processo, pode pular esta etapa.

## Perguntas frequentes
Se encontrar um problema ao usar o CVM, consulte os seguintes documentos de solução de problemas com base em sua situação real.
- Para questões relacionadas ao login do CVM, consulte [Login de senha e login de chave SSH](https://intl.cloud.tencent.com/document/product/213/18120) e [Login e acesso remoto](https://intl.cloud.tencent.com/document/product/213/17278).
- Para questões relacionadas à rede CVM, consulte [Endereços IP](https://intl.cloud.tencent.com/document/product/213/17285) e [Portas e grupos de segurança](https://intl.cloud.tencent.com/document/product/213/2502).
- Para questões relacionadas aos discos CVM, consulte [Discos de sistema e dados](https://intl.cloud.tencent.com/document/product/213/17351).

