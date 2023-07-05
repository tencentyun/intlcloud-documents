## Introdução
O documento usa CVMs com o CentOS 7.6 como exemplo para descrever como fazer upload e download de arquivos via SCP.


## Pré-requisitos
Você adquiriu um CVM do Linux.

## Instruções
### Obtenção de um IP público
Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index), navegue até a página da lista de instâncias e registre o IP público do CVM para o qual deseja fazer o upload dos arquivos, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/59ce52615c467ad80bc4220425bf2b80.png)


### Upload de arquivo
1. Execute o comando a seguir em um computador com sistema operacional Linux para fazer upload de arquivos para o CVM do Linux.
```
scp endereço de arquivo local conta do CVM@IP público/nome de domínio da instância do CVM: Localização do arquivo CVM
```
Por exemplo, se você deseja fazer upload do arquivo local `/home/lnmp0.4.tar.gz` para o diretório correspondente do CVM cujo IP público é `129.20.0.2`, execute o seguinte comando:
```
scp /home/Inmp0.4.tar.gz root@129.20.0.2:/home/Inmp0.4.tar.gz
```
2. Digite **yes** e pressione **Enter** para confirmar o upload e digite a senha de login para concluir o upload.
 - Se você usar uma senha padrão do sistema para fazer login na instância, poderá consultar a senha no [Centro de mensagens](https://console.cloud.tencent.com/message).
 - Se esquecer sua senha, [redefina a senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).

### Download de um arquivo
1. Execute o comando a seguir em um computador com sistema operacional Linux para baixar os arquivos do CVM do Linux.
```
scp conta do CVM@IP público/nome de domínio da instância do CVM: Localização do arquivo CVM endereço de arquivo local   
```
Por exemplo, se você deseja baixar o arquivo `/home/lnmp0.4.tar.gz` do CVM cujo IP público é `129.20.0.2` para o diretório local correspondente, execute o seguinte comando:
```
scp root@129.20.0.2:/home/Inmp0.4.tar.gz /home/Inmp0.4.tar.gz
```
