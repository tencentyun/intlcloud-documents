## Visão geral

O Remote Desktop Protocol (RDP) é um protocolo de vários canais desenvolvido pela Microsoft que permite que um computador local se conecte a um computador remoto. Recomendamos que você use o RDP para fazer login em seus CVMs do Windows. Este documento descreve como fazer login em instâncias do Windows usando arquivos RDP.

## Sistemas compatíveis
Você pode fazer login em seus CVMs do Windows, Linux e MacOS usando o RDP.

## Pré-requisitos

- É necessário ter a conta de administrador e a senha para fazer login em uma instância do Windows remotamente.
 - Se você usar uma senha padrão do sistema para fazer login na instância, poderá obter a senha no [Centro de mensagens](https://console.cloud.tencent.com/message).
 - Se você esqueceu sua senha, [redefina a senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).
- Você adquiriu IPs públicos para sua instância do CVM e a porta 3389 está aberta. (Essa porta fica aberta por padrão para um CVM adquirido com a configuração rápida.)

## Direções

### Login no seu CVM do Windows usando o RDP
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página **Instances (Instâncias)**, localize o CVM do Windows no qual deseja fazer login e clique em **Log In (Login)** conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/e7b1192332a116edca67425a301236be.png)
3. Na janela pop-up **Log into Windows instance (Login na instância do Windows)**, selecione **Log in with RDP file (Login com o arquivo RDP)** e clique em **Download RDP file (Baixar arquivo RDP)** para baixar o arquivo RDP em seu computador local.
>?Se você alterou a porta de login remoto, acrescente o endereço IP com `:port` no arquivo RDP.
>
![](https://main.qcloudimg.com/raw/0b0076390b95da3885c8967093683975.png)
4. Clique duas vezes no arquivo RDP baixado, digite a senha e clique em **OK** para conectar-se remotamente ao CVM do Windows.
 - Se você usar uma senha padrão do sistema para fazer login na instância, poderá obter a senha no [Centro de mensagens](https://console.cloud.tencent.com/message).
 - Se você esqueceu sua senha, [redefina a senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).

### Login no seu CVM do Linux usando o RDP

>? Recomendamos que você use o rdesktop como o cliente da área de trabalho remota. Para obter mais informações, consulte a [introdução oficial ao rdesktop](http://www.rdesktop.org/).
>
1. Execute o seguinte comando para verificar se o rdesktop foi instalado.
```
rdesktop
```
 - Se sim, realize a [etapa 4](#step04).
 - Se não, você será avisado com "command not found (comando não encontrado)". Nesse caso, realize a [etapa 2](#step02).
2. <span id="step02"></span>Abra uma janela do terminal e execute o seguinte comando para baixar o rdesktop. Essa etapa usa o rdesktop v1.8.3 como exemplo.
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
Se você deseja instalar a versão mais recente, acesse [a página do rdesktop no GitHub](https://github.com/rdesktop/rdesktop/releases) para localizá-la. Em seguida, substitua o caminho no comando pelo da versão mais recente.
3. No diretório onde o rdesktop será instalado, execute os seguintes comandos para descompactar e instalar o rdesktop.
```
tar xvzf rdesktop-<x.x.x>.tar.gz ## Replace x.x.x with the version number of the downloaded rdesktop. 
cd rdesktop-1.8.3
./configure 
make 
make install
```
4. <span id="step04">Execute o seguinte comando para se conectar à instância remota do Windows.</span>
>? Substitua os parâmetros do exemplo por seus próprios parâmetros.
>
```
rdesktop -u Administrator -p <your-password> <hostname or IP address>
```
 - `Administrator` refere-se à conta de administrador mencionada na seção de pré-requisitos.
 - `<your-password>` refere-se à senha de login que você definiu.
   Se você usar uma senha padrão do sistema para fazer login na instância, poderá obter a senha no [Centro de mensagens](https://console.cloud.tencent.com/message). Se você esqueceu sua senha, [redefina a senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).
 - `<hostname or IP address>` refere-se ao endereço IP público ou nome de domínio personalizado da sua instância do Windows.
 
### Login no seu CVM do MacOS usando o RDP

>?
>- As seguintes operações usam a Área de Trabalho Remota da Microsoft para Mac como exemplo. A Microsoft parou de fornecer um link para baixar o cliente da Área de Trabalho Remota em 2017. Atualmente, sua subsidiária HockeyApp é responsável pelo lançamento do cliente beta. Vá para [Área de Trabalho Remota Beta da Microsoft](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/microsoft-remote-desktop-for-mac/distribution_groups/all-users-of-microsoft-remote-desktop-for-mac) para baixar uma versão beta.
>- As seguintes operações usam um CVM no Windows Server 2012 R2 como exemplo.
>
1. Baixe e instale a Área de Trabalho Remota da Microsoft para Mac em seu computador local.
2. Inicie o MRD e clique em **Add Desktop (Adicionar área de trabalho)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
3. Na janela pop-up **Add Desktop (Adicionar área de trabalho)**, siga as etapas ilustradas na imagem a seguir para estabelecer uma conexão com o CVM do Windows.
![](https://main.qcloudimg.com/raw/d8e20278dd7c8aed487be2c43986f5e4.png)
    1. No campo de texto **PC name (Nome do computador)**, insira o endereço IP público do seu CVM.
    2. Clique em **Add (Adicionar)**.
    3. Mantenha as configurações padrão para as outras opções e estabeleça a conexão.
    Sua entrada foi salva, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. Clique duas vezes na nova entrada. Insira seu nome de usuário e senha para o CVM e clique em **Continue (Continuar)**.
 - Se você usar uma senha padrão do sistema para fazer login na instância, poderá obter a senha no [Centro de mensagens](https://console.cloud.tencent.com/message).
 - Se você esqueceu sua senha, [redefina a senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).
5. Na janela pop-up, clique em **Continue (Continuar)** para estabelecer a conexão, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
Se a conexão for bem-sucedida, a seguinte página aparecerá:
![](https://main.qcloudimg.com/raw/20db4a1d63384bc0575ded68a8fe912d.png)
