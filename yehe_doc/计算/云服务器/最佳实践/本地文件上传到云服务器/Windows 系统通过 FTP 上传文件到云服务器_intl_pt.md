## Visão geral

Este documento descreve como usar o serviço FTP para fazer upload de arquivos de um computador Windows local para um CVM.

## Pré-requisitos

Você ativou o serviço FTP no CVM.
- Para usar o FTP para carregar arquivos em um CVM do Linux, consulte [Ativação do serviço FTP (Linux)](https://intl.cloud.tencent.com/document/product/213/10912)
- Para usar o FTP para carregar arquivos em um CVM do Windows, consulte [Ativação do serviço FTP (Windows)](https://intl.cloud.tencent.com/document/product/213/10414)


## Instruções

### Conexão ao CVM
1. Baixe e instale o software livre FileZilla localmente.
> Se você usar a versão 3.5.3 do FileZilla para fazer upload de arquivos via FTP, o upload pode falhar. Recomendamos que você baixe e use as versões 3.5.1 ou 3.5.2 do FileZilla do site oficial.
>
2. Abra o FileZilla.
3. Na janela do FileZilla, insira as informações como host, nome de usuário, senha e porta e clique em **Quickconnect (Conexão rápida)**.

**Descrição da configuração:**
 - Host: o IP público do CVM. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm) para exibir o IP público do CVM na página **Instances (Instâncias)**.
 - Username (Nome de usuário): a conta de usuário do FTP configurada quando você [criou o serviço FTP](https://intl.cloud.tencent.com/document/product/213/10912). A figura abaixo usa "ftpuser1" como exemplo.
 - Password (Senha): a senha correspondente à conta de usuário do FTP configurada quando você [criou o serviço FTP](https://intl.cloud.tencent.com/document/product/213/10912).
 - Port (Porta): a porta de escuta do FTP, que é **21** por padrão.
Após a conexão, você pode exibir os arquivos no site do CVM remoto.

### Upload de arquivo
Na janela inferior esquerda "Local site (Site local)", clique com o botão direito no arquivo local a ser carregado e selecione **Upload (Carregar)** para carregá-lo em um CVM do Linux, conforme mostrado abaixo:
> 
>- O caminho do FTP do CVM não permite a descompactação ou exclusão automática de arquivos .tar compactados carregados.
>- O caminho do site remoto é o caminho padrão para enviar arquivos para um CVM do Linux.
>

### Download de um arquivo
No canto inferior direito da janela "Remote site (Site remoto)", clique com o botão direito do mouse no arquivo do CVM a ser baixado e selecione **Download (Baixar)** para baixá-lo em um diretório local.


