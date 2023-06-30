## Visão geral
O documento usa CVMs com o CentOS 7.6 como exemplo para descrever como fazer upload e download de arquivos via SCP.


## Pré-requisitos
Você adquiriu um CVM do Linux.

## Instruções
### Obtenção de um IP público
Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index), navegue até a página **Instances (Instâncias)** e registre o IP público do CVM para o qual deseja fazer o upload dos arquivos, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/4ffafbd2f6ab65d55e56fe59b669363a.png)


### Upload de arquivos
1. Execute o comando a seguir para fazer upload de arquivos para um CVM do Linux.
```
scp [endereço de arquivo local] [conta do CVM]@[IP público/nome de domínio da instância do CVM]:[localização do arquivo CVM]
```
Suponha que você queira fazer o upload do arquivo local `/home/lnmp0.4.tar.gz` do CVM (IP: 129.20.0.2) no mesmo diretório, o comando deve ser o seguinte:
```
scp /home/Inmp0.4.tar.gz root@129.20.0.2:/home/Inmp0.4.tar.gz
```
2. Digite **yes** e pressione **Enter** para confirmar o upload e digite a senha de login para concluir o upload.
 - Se você usar uma senha padrão do sistema para fazer login na instância, vá primeiro para o [Centro de mensagens](https://console.cloud.tencent.com/message) para obtê-la.
 Se você esqueceu sua senha, você pode [redefinir a senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).

### Download de um arquivo
1. Execute o comando a seguir para baixar um arquivo de um CVM do Linux.
```
scp conta do CVM@IP público/nome de domínio da instância do CVM: Localização do arquivo CVM endereço de arquivo local 
```
Por exemplo, você pode executar o seguinte comando para baixar o arquivo `/home/lnmp0.4.tar.gz` do CVM cujo IP público é `129.20.0.2` para o mesmo diretório local:
```
scp root@129.20.0.2:/home/Inmp0.4.tar.gz /home/Inmp0.4.tar.gz
```


