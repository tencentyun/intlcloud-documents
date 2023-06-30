## Cenário
O WinSCP é um cliente do SFTP gráfico de software livre que usa SSH no ambiente Windows e aceita o protocolo SCP. Sua principal funcionalidade é a cópia de arquivos com segurança entre os computadores locais e remotos. Em comparação com os códigos de upload via FTP, você pode usar diretamente sua conta do CVM no WinSCP para acessar o CVM sem configuração adicional.

## Pré-requisitos
O WinSCP foi baixado e instalado no computador local (recomendamos que você baixe a versão mais recente do WinSCP no [site oficial](http://winscp.net/eng/docs/lang:chs).

## Instruções

### Login no WinSCP

1. Abra o WinSCP, e a caixa "WinSCP Login (Login do WinSCP)" será exibida.
2. Configure os seguintes parâmetros:
 - Protocol (Protocolo): SFTP ou SCP.
 - Host Name (Nome do host): IP público do CVM. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm) para exibir o IP público do CVM.
 - Port (Porta): 22, por padrão.
 - Password (Senha): senha correspondente ao nome de usuário do CVM.
 - Username (Nome de usuário): o nome de usuário do CVM.
	 - SUSE/CentOS/Debian: raiz
	 - Ubuntu：ubuntu
3. Clique em **Login** para acessar a interface de transferência de arquivos "WinSCP".

### Upload de arquivo
1. No painel direito da interface de transferência de arquivos "WinSCP", selecione o diretório onde os arquivos serão armazenados no servidor, como "/user".
2. No painel esquerdo da interface de transferência de arquivos "WinSCP", selecione o diretório onde os arquivos estão armazenados no computador local, como "F:\SSL certificate\ Nginx" e, depois, selecione os arquivos a serem transferidos.
3. Na barra de menus da interface de transferência de arquivos "WinSCP", clique em **Upload (Carregar)**.
4. Na caixa "Upload (Carregar)" exibida, confirme os arquivos a serem carregados e os diretórios remotos e clique em **OK** para fazer o upload dos arquivos do computador local para o CVM.

### Download de um arquivo
1. No painel esquerdo da interface de transferência de arquivos "WinSCP", selecione o diretório onde os arquivos serão armazenados no computador local, como "F:\SSL certificate \Nginx".
2. No painel direito da interface de transferência de arquivos "WinSCP", selecione o diretório onde os arquivos estão armazenados no servidor, como "/user" e, depois, selecione o arquivo a ser transferido.
3. Na barra de menus da interface de transferência de arquivos "WinSCP", clique em **Download (Baixar)**.
4. Na caixa "Download (Baixar)" exibida, confirme os arquivos a serem baixados e os diretórios remotos e clique em **OK** para baixar os arquivos do CVM para o computador local.
