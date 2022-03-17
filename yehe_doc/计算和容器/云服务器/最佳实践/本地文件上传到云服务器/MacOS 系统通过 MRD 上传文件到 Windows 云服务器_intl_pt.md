## Visão geral
A Área de Trabalho Remota da Microsoft (MRD) é um software de área de trabalho remota desenvolvido pela Microsoft. Este documento descreve como usá-la no MacOS para fazer upload de arquivos para um CVM do Tencent Cloud com o Windows Server 2012 R2 instalado. 

## Pré-requisitos
- Você baixou e instalou a MRD em seu computador local. As seguintes operações usam a Área de Trabalho Remota da Microsoft para Mac como exemplo. A Microsoft parou de fornecer um link para baixar o cliente da Área de Trabalho Remota em 2017. Atualmente, sua subsidiária HockeyApp é responsável pelo lançamento do cliente beta. Acesse [Área de Trabalho Remota Beta da Microsoft](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/microsoft-remote-desktop-for-mac/distribution_groups/all-users-of-microsoft-remote-desktop-for-mac) para baixar uma versão beta.
- A MRD é compatível com o MacOS 10.10 e versões posteriores. Verifique se o seu sistema operacional é compatível.
- Você adquiriu um CVM do Windows.

## Instruções
### Obtenção de um IP público
Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index), navegue até a página **Instances (Instâncias)** e registre o IP público do CVM para o qual deseja fazer o upload dos arquivos, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/59ce52615c467ad80bc4220425bf2b80.png)

### Upload de arquivos
1. Inicie o MRD e clique em **Add Desktop (Adicionar área de trabalho)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
2. Na janela pop-up **Add Desktop (Adicionar área de trabalho)**, siga as etapas abaixo para selecionar a pasta a ser carregada e estabelecer uma conexão com seu CVM do Windows.
![](https://main.qcloudimg.com/raw/fc241ce8e4744bde57476ea823fcef72.png)
  1. No campo de texto **PC name (Nome do computador)**, insira o endereço IP público do seu CVM.
  2. Clique em **Folders (Pastas)** para redirecionar para a lista de pastas.
  3. Clique em <img src="https://main.qcloudimg.com/raw/89e7a3ff040849307cd1eb8bd878a2db.png" style="margin:-3px 0px"> no canto inferior esquerdo e selecione a pasta a ser carregada na janela pop-up.
  4. Verifique sua lista de pastas para fazer upload e clique em **Add (Adicionar)**.
  5. Mantenha as configurações padrão para as outras opções e estabeleça a conexão.
Sua entrada foi salva, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. Clique duas vezes na nova entrada. Insira seu nome de usuário e senha para o CVM e clique em **Continue (Continuar)**.
>?
>- A conta padrão para o CVM do Windows é `Administrator`.
- Se você usar uma senha padrão do sistema para fazer login na instância, vá primeiro para o [Centro de mensagens](https://console.cloud.tencent.com/message) para obtê-la.
>- Se você esqueceu sua senha, [redefina a senha da instância](http://intl.cloud.tencent.com/document/product/213/16566).
>
5. Na janela pop-up, clique em **Continue (Continuar)** para estabelecer a conexão, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
Se a conexão for bem-sucedida, a seguinte página aparecerá:
![](https://main.qcloudimg.com/raw/5a524210acd13624af7263b6de3aea54.png)
6. Clique em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px"> no canto inferior esquerdo e selecione **My Computer (Meu computador)** para exibir uma lista de pastas compartilhadas.
7. Clique duas vezes em uma pasta compartilhada para abri-la. Copie os arquivos locais desejados para outra unidade do CVM do Windows.
Por exemplo, copie o arquivo A da pasta para a unidade C do CVM do Windows.

### Download de arquivos
Para baixar arquivos do CVM do Windows para o seu computador, basta copiar os arquivos desejados do CVM para uma pasta compartilhada.


