## Cenário

Este documento descreve como fazer login em uma instância do Windows pela área de trabalho remota em um computador local.

## Sistema operacional aplicável

Windows

## Pré-requisitos

- Você já deve ter a conta de administrador e a senha para fazer login em uma instância do Windows remotamente.
 - Se você usar uma senha padrão do sistema para fazer login na instância, obtenha-a visitando [Mensagem interna](https://console.cloud.tencent.com/message).
 Se você esqueceu sua senha, [redefina a senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).
- Um IP público foi adquirido para sua instância do CVM e a porta 3389 está aberta. (Se o CVM for adquirido com a “Configuração rápida”, essa porta fica aberta por padrão.)

## Etapas
>? As etapas a seguir consideram o sistema operacional Windows 7 como exemplo.
>
1. No computador Windows local, clique em <img src="https://main.qcloudimg.com/raw/370daffec54024ee262d1e5dbcd4bde2.png" style="margin: 0;width: 35px;"> e digite **mstsc** em **Search programs and files (Pesquisar programas e arquivos)** e pressione **Enter** para abrir a caixa de diálogo de conexão da área de trabalho remota, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/d8a4b0f70f876f6c0edc6e995a02c37d.png)
2. Digite o IP público do servidor Windows após **Computer (Computador)** e clique em **Connect (Conectar)**.
Para obter mais informações sobre como obter o IP público, consulte [Obtenção de endereços IP públicos](https://intl.cloud.tencent.com/document/product/213/17940).
3. Digite a conta/senha de administrador da instância na janela pop-up **Windows Security (Segurança do Windows)**, conforme mostrado abaixo:
> Se a caixa de diálogo **Do you trust this remote connection? (Você confia nesta conexão remota?)** for exibida, você pode marcar **Don’t ask me again for connections to this computer (Não me perguntar novamente sobre as conexões com este computador)** e clicar em **Connect (Conectar)**.

![](https://main.qcloudimg.com/raw/5d3d89e3ec4616a367b80ba377a3f541.png)
4. Clique em **OK** para fazer login na instância do CVM do Windows.

