## Visão geral

Este documento descreve como usar o serviço FTP para carregar arquivos de um computador Linux local em um CVM.

## Pré-requisitos

Você ativou o serviço FTP no CVM.
- Para usar o FTP para carregar arquivos em um CVM do Linux, consulte [Ativação do serviço FTP (Linux)](https://intl.cloud.tencent.com/document/product/213/10912)
- Para usar o FTP para carregar arquivos em um CVM do Windows, consulte [Ativação do serviço FTP (Windows)](https://intl.cloud.tencent.com/document/product/213/10414)

## Instruções

### Conexão ao CVM
1. Execute o comando a seguir para instalar o serviço FTP.
> Se o serviço FTP já tiver sido instalado no computador Linux local, ignore essa etapa.
>
```
yum -y install ftp
```
2. Execute o comando a seguir para se conectar ao CVM e digite o nome de usuário e a senha do serviço FTP conforme solicitado.
```
ftp <CVM IP address>
```
Se a interface a seguir for exibida, a conexão foi estabelecida.
![](https://main.qcloudimg.com/raw/9d93f45167addf70e023a21543af59f8.png)

### Upload de arquivo
Execute o comando a seguir para carregar um arquivo local no CVM.
```
put local-file [remote-file]
```
Por exemplo, para carregar o arquivo `/home/1.txt` local no CVM, execute o comando a seguir.
```
put /home/1.txt 1.txt
```

### Download de um arquivo
Execute o comando a seguir para baixar um arquivo do CVM em um diretório local.
```
get [remote-file] [local-file]
```
Por exemplo, para baixar o arquivo `A.txt` do CVM no diretório local `/home`, execute o comando a seguir.
```
get A.txt /home/A.txt
```

