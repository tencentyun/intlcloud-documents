## Cenário

Este documento usa um CVM executando o Windows Server 2012 R2 como exemplo para descrever como configurar o PHP 5.3 e versões anteriores ou posteriores à 5.3 em um CVM Windows.


## Pré-requisitos

- Ter efetuado login no CVM do Windows e adicionado e instalado a função IIS no CVM. Para obter mais informações, consulte [Etapa 1: Instalação e configuração do IIS](https://intl.cloud.tencent.com/document/product/213/2755).
- Ter obtido o endereço IP público do Windows CVM. Para obter mais informações, consulte [Obtenção do endereço IP público de uma instância](https://intl.cloud.tencent.com/document/product/213/17940).

## Instruções

<span id="jump1"></span>
### Instalação do PHP 5.3 ou anterior

>! O [site oficial do PHP](http://windows.php.net/download/) não fornece mais os pacotes de instalação para versões anteriores ao PHP 5.2. Se você precisar de uma versão anterior à do PHP 5.2, pesquise e faça download no CVM. Como alternativa, faça download localmente e depois faça upload do pacote de instalação para o CVM. Para obter mais informações sobre como fazer upload de arquivos para um CVM Windows, consulte [Fazer upload de arquivos por meio de MSTSC para um CVM Windows](https://intl.cloud.tencent.com/document/product/213/2761). O procedimento a seguir usa PHP 5.2.13 como exemplo.
> 
1. Abra o pacote de instalação do PHP no CVM.
2. Clique em **Next (Avançar)**.
3. Na página "Web Server Setup (Configuração do servidor da web)", selecione **IIS FastCGI** e clique em **Next (Avançar)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/c5fc89547b020e6ec943732d16186a7b.png).
4. Conclua a instalação do PHP conforme solicitado.
5. Crie um arquivo PHP como `hello.php` em `C:/inetpub/wwwroot`.
6. No arquivo `hello.php` criado, adicione o seguinte código e salve o arquivo.
```
	<?php
	echo "<title>Test Page</title>";
	echo "hello world";
	?>
```
7. Na área de trabalho, abra o navegador e visite `http://<Public IP address of the Windows CVM>/hello.php` e verifique se o ambiente foi configurado com sucesso.
Se a página exibida abaixo aparecer, a configuração foi bem-sucedida.
![](https://main.qcloudimg.com/raw/0cdefc8707c4402e9ae5f9e6fa523ae1.png)

<span id="jump"></span>
### Instalação de uma versão posterior à PHP 5.3

Versões posteriores à PHP 5.3 não têm um pacote de instalação e são instaladas usando um arquivo zip ou pacote de depuração. O seguinte demonstra como instalar o PHP em um ambiente Windows Server 2012 R2 usando um arquivo zip.

#### Fazer download do software

1. No CVM, acesse o [site oficial do PHP](http://windows.php.net/download/) e baixe o pacote de instalação do PHP compactado, conforme mostrado na figura a seguir:
>! Para executar o PHP no IIS, você deve selecionar o pacote de instalação x86 para Non Thread Safe. Se o seu servidor estiver executando o Windows Server de 32 bits (x86), substitua o IIS pelo Apache e selecione o pacote de instalação x86 para Thread Safe.
>
![](https://main.qcloudimg.com/raw/b54dcb237ae24673cd592561ffc91bc0.png)
2. Com base no nome do pacote de instalação do PHP baixado, faça download e instale o pacote de instalação Visual C++ Redistributable.
A tabela a seguir lista os pacotes de instalação Visual C++ Redistributable que precisam ser baixados e instalados para o pacote de instalação do PHP.
<table>
<tr><th>Nome do Pacote de Instalação PHP</th><th>Download do endereço do pacote de instalação do Visual C++ Redistributable</th></tr>
<tr><td>php-x.x.x-nts-Win32-VC16-x86.zip</td><td><a href="https://visualstudio.microsoft.com/zh-hans/downloads/">Microsoft Visual C++ Redistributable for Visual Studio 2019</a>(x86)</td></tr>
<tr><td>php-x.x.x-nts-Win32-VC15-x86.zip</td><td><a href="https://visualstudio.microsoft.com/zh-hans/vs/older-downloads/">Microsoft Visual C++ Redistributable for Visual Studio 2017</a>(x86)</td></tr>
<tr><td>php-x.x.x-nts-Win32-VC14-x86.zip</td><td><a href="https://www.microsoft.com/zh-cn/download/details.aspx?id=48145">Microsoft Visual C++ Redistributable for Visual Studio 2015</a>(x86)</td></tr>
</table>
Por exemplo, se o nome do pacote de instalação do PHP baixado for <code>PHP-7.1.30-nts-Win32-VC14-x86.zip</code>, faça download e instale o pacote de instalação Microsoft Visual C++ Redistributable for Visual Studio 2015 (x86).

#### Instalação e configuração
1. Descompacte o pacote de instalação do PHP baixado, por exemplo, para `C:\PHP`.
2. Copie o arquivo `php.ini-production` em `C:\PHP` e altere a extensão do arquivo para `.ini`, ou seja, renomeie-o para `php.ini`, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/52d9a2098fe73c8ddb41366b9732a000.png)
3. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> para abrir o **Server Manager (Gerenciador do servidor)**, conforme mostrado na figura a seguir:
4. Na barra lateral esquerda, clique em **IIS**.
5. Na janela de gerenciamento do IIS à direita, clique com o botão direito do mouse no nome do servidor na coluna **Server (Servidor)** e escolha **Internet Information Services (IIS) Manager (Gerenciador de Serviços de Informações da Internet (IIS))**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/55e0b4c86de284050e5d810e92650337.png)
6. Na janela "Internet Information Service (IIS) Manager (Gerenciador de Serviços de Informações da Internet (IIS))", clique no nome do servidor na barra lateral esquerda para ir para a página inicial do servidor, conforme mostrado na figura a seguir:
Por exemplo, clique no nome do servidor 10_141_9_72 para ir para a página inicial 10_141_9_72.
![](https://main.qcloudimg.com/raw/ab0f2306624452d4a3ab9fd5389d5b1d.png)
7. Na **10_141_9_72 homepage (Página inicial 10_141_9_72)**, clique duas vezes em **Handler Mappings (Mapeamentos do manipulador)** para ir para a página "Handler Mappings (Mapeamentos do manipulador)", conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/916a9cc9ce1270dbbfe6ddbb58f937e7.png)
8. Na coluna **Actions (Ações)** à direita, clique em **Add Module Mapping (Adicionar mapeamento de módulo)** para abrir a janela "Add Module Mapping (Adicionar mapeamento de módulo)".
9. Na janela "Add Module Mapping (Adicionar mapeamento de módulo)", insira as seguintes informações e clique em **OK**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/a4d139682fc14204acd77ac3d1ea10eb.png)
Os principais parâmetros incluem:
 - Caminho da solicitação: digite `*.php`.
 - Módulo: selecione "FastCgiModule".
 Executável (opcional): selecione o arquivo php-cgi.exe no pacote de instalação do PHP, ou seja, `C:\PHP\php-cgi.exe`.
 - Nome: insira um nome personalizado, como FastCGI.
10. Na janela exibida, clique em **OK**. 
11. Clique no nome do servidor 10_141_9_72 na barra lateral esquerda para retornar à página inicial 10_141_9_72.
12. Na **10_141_9_72 homepage (Página incial 10_141_9_72)**, clique duas vezes em **Default Document (Documento padrão)** para ir para a página de gerenciamento de documentos padrão, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/6a896eeb929ae0104b1792e08bd895a6.png)
13. Na coluna **Actions (Ações)** à direita, clique em **Add (Adicionar)** para abrir a janela "Add Default Document (Adicionar documento padrão)".
14. Na janela "Add Default Document (Adicionar documento padrão)", defina **Name (Nome)** como `index.php` e clique em **OK**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/2d09af5d86755dd481b13efb0b3619a2.png)
15. Clique no nome do servidor 10_141_9_72 na barra lateral esquerda para retornar à página inicial 10_141_9_72.
16. Na **10_141_9_72 homepage (Página inicial 10_141_9_72)**, clique duas vezes em **FastCGI Settings (Configurações FastCGI)** para abrir a página de gerenciamento de configuração FastCGI, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/2a0693d3b837804b546fc690b4fb5cee.png)
17. Na página de gerenciamento de configuração FastCGI, selecione o aplicativo FastCGI e clique em **Edit (Editar)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/2038fa0df5c08820dc028fb3635fcda4.png)
18. Na janela "Edit FastCGI Application (Editar aplicativo FastCGI"), defina **Monitor changes to file (Monitorar alterações no arquivo)** para o caminho do arquivo `php.ini`, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/b1aa458607934a5331b51e22762d0dec.png)
19. Em `C:\inetpub\wwwroot`, crie um arquivo PHP, como`index.php`.
20. No arquivo `index.php` criado, adicione o seguinte código e salve o arquivo.
```
<?php
phpinfo();
?>
```
21. Na área de trabalho, abra o navegador e visite `http://localhost/index.php` para verificar se o ambiente foi configurado com êxito.
Se a página exibida abaixo aparecer, a configuração foi bem-sucedida.
![](https://main.qcloudimg.com/raw/ccd08fd9af6afe4ee2c3bf38f9e581b9.png)

