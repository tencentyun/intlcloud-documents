## Introdução
rdesktop é um cliente do RDP de software livre. Este artigo descreve como usá-lo para se conectar a um CVM executando o Windows Server 2012 R2 para carregar arquivos.

## Pré-requisitos
Adquiriu uma instância do CVM do Windows.

## Instruções
### Obtenção do IP público do CVM
Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index) e localize o endereço IP público do CVM do Windows, conforme mostrado na seguinte imagem:
![](https://main.qcloudimg.com/raw/59ce52615c467ad80bc4220425bf2b80.png)



###. Instalação do rdesktop.
1. Abra uma janela do terminal e execute o seguinte comando para baixar o rdesktop 1.8.3:
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
Se você deseja instalar uma versão nova, acesse [a página inicial do rdesktop no GitHub](https://github.com/rdesktop/rdesktop/releases) para localizá-la. Em seguida, substitua o caminho no comando pelo da versão nova.
2. Execute os comandos a seguir para descompactar o pacote de instalação e navegue até o seu diretório.
```
tar xvzf rdesktop-1.8.3.tar.gz
```
```
cd rdesktop-1.8.3
```
3. Execute os comandos a seguir para compilar e instalar o rdesktop.
```
./configure 
```
```
make
```
```
make install
```
4. Após a conclusão da instalação, execute o seguinte comando para verificar se o rdesktop foi instalado:
```
rdesktop
```

### Upload de arquivos
1. Execute o seguinte comando para especificar a pasta compartilhada:
```
rdesktop cvm_ip  -u cvm_username -p cvm_password -r disk:shared_folder_path=local_folder_path
```
>
>- O nome de usuário padrão do CVM é `Administrator`.
>- Se você optar por fazer o login com uma senha aleatória, verifique-a em [Centro de mensagens](https://console.cloud.tencent.com/message).
>- Se você esqueceu sua senha, [redefina a senha da instância](http://intl.cloud.tencent.com/document/product/213/16566).
>
Por exemplo, execute o comando a seguir para compartilhar a pasta `/home` na máquina local do Linux com o CVM especificado e renomeá-la como `share`.
```
rdesktop 118.xx.248.xxx  -u Administrator -p 12345678 -r disk:share=/home
```
Se a operação obtiver êxito, a área de trabalho do Windows será exibida.
Clique em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px"> e, em seguida, **My Computer (Meu computador)** para exibir as pastas compartilhadas.
2. Clique duas vezes na pasta compartilhada para abri-la. Copie um arquivo da pasta compartilhada para um diretório no disco do CVM do Windows para carregá-lo.
Por exemplo, copie **a.txt** em `share` para a unidade C do CVM do Windows.

### Download de arquivos
Para baixar arquivos de um CVM do Windows para o computador Linux, copie os arquivos desejados do CVM na pasta compartilhada.
