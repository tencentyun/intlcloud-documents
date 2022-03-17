## Visão geral

Este documento descreve como adicionar e instalar funções IIS em uma instância CVM com Windows Server 2012 R2 ou Windows Server 2008.

## Instruções
### Windows Server 2012 R2 
1. Faça login no CVM do Windows.
2. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> e abra o **Server Manager (Gerenciador do servidor)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/cae0fe0bfebf5ad58b6e5d3451795230.png)
3. Clique em **Add roles and features (Adicionar funções e recursos)** e acesse a janela "Add Roles and Features Wizard (Assistente para adicionar funções e recursos)".
4. Na janela pop-up, clique em **Next (Avançar)** e acesse a página "Select installation type (Selecionar tipo de instalação)".
5. Selecione **Role-based or feature-based installation (Instalação baseada em função ou recurso)** e clique em **Next (Avançar)** duas vezes, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/9eaff4f125fb23a7180cba6f38f9f879.png)
6. Marque **Web Server (IIS) (Servidor Web (IIS))** na página "Select server roles (Selecionar funções de servidores)", conforme mostrado abaixo:
A caixa de diálogo "Add features that are required for Web Server (IIS) (Adicionar recursos necessários para servidor web (IIS))** será exibida.
![](https://main.qcloudimg.com/raw/d0aa5fa075275bfb2bd0c68da66616e4.png)
7. Clique em **Add Features (Adicionar recursos)** na caixa de diálogo pop-up, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/817d1f22107836c77af2fd963888824f.png)
8. Clique em **Next (Avançar)**.
9. Na página **Features (Recursos)**, marque **.NET Framework 3.5 Features (Recursos do .NET Framework 3.5)** e clique em **Next (Avançar)** duas vezes, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/4876efa4308912eb4bdbb6074d35fd20.png)
10. Na página **Role Services (Serviços de função)**, marque **CGI** e clique em **Next (Avançar)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/c571820b1a4290d9b04abbc65cf81fd9.png)
11. Revise suas seleções de instalação e clique em **Install (Instalar)**. Aguarde a conclusão do processo de instalação.
![](https://main.qcloudimg.com/raw/1e51aed773aad8eac28f88c401a1814e.png)
12. Quando a instalação for concluída, abra um navegador no CVM e visite`http://localhost/` para verificar se o IIS foi instalado com sucesso.
Se a página a seguir for exibida, isso indica que o IIS foi instalado com sucesso.
![](https://mc.qcloudimg.com/static/img/e064cc1f765d68edf3dcfb0051d5dbfa/image.png)

### Windows Server 2008

1. Faça login no CVM do Windows.
2. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/0e33f3dc1042244ab225ca32c5396296.png" style="margin: 0;"></img> e abra o **Server Manager (Gerenciador do servidor)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/36c9cf3d9fd246f0930a4be3516446b5.png)
3. Selecione **Roles (Funções)** na barra lateral esquerda e clique em **Add Roles (Adicionar funções)** no painel direito, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/b18a3c84aa193d3c64d1e25353154baf.png)
4. Clique em **Next (Avançar)** na janela "Add Roles Wizard (Assistente para adicionar funções)", conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/4ab72f46730ecf10f2fe2768b2cc24cc.png)
5. Na página "Server Roles (Funções do servidor)", marque **Web Server IIS (Servidor web (IIS))** e clique em **Next (Avançar)** duas vezes, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/7a41185e562a62ca586b6b677381b3a1.png)
6. Na página **Role Services (Serviços de função)**, marque **CGI** e clique em **Next (Avançar)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/7e7a96b106292e87d44807369db66842.png)
7. Revise suas seleções de instalação e clique em **Install (Instalar)**. Aguarde a conclusão do processo de instalação.
![](https://main.qcloudimg.com/raw/877b71930f11d9d2a6fecf946f0bebfe.png)
8. Quando a instalação for concluída, abra um navegador no CVM e visite`http://localhost/` para verificar se o IIS foi instalado com sucesso.
Se a página a seguir for exibida, isso indica que o IIS foi instalado com sucesso.
![](https://main.qcloudimg.com/raw/b11cd8170e7646daa3b9ca904b181cf4.png)

