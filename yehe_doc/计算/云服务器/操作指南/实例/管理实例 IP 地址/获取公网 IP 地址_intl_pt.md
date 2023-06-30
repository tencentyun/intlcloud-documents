## Cenário
Este documento descreve como obter o endereço IP público pelo console, por API ou pelos metadados da instância.


## Direções

### Obtenção do endereço IP público no console
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
2. Na página de gerenciamento da instância, mova o mouse para a coluna IP principal e <img src = "https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style = "margin: 0;"></ img> é exibido, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/952664b0a70077ba49a031b98a57c782.png)
3. Clique em <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: 0;"> para copiar o endereço IP.	
>! O endereço IP público é mapeado para o endereço IP privado por meio do NAT. Se você visualizar os atributos da interface de rede pela instância (por exemplo, usando comandos como `ifconfig (Linux)` ou `ipconfig (Windows)`), o endereço IP público não será exibido. Para obter o IP público pela instância, consulte [Obtenção de um endereço IP público da instância usando metadados da instância](#jump).
>

### Obtenção do endereço IP público usando API
Consulte [DescribeInstances](https://intl.cloud.tencent.com/document/product/213/33258).

<span id = "jump">  </span>
### Obtenção do endereço IP público usando metadados da instância
1. Faça login na instância do CVM.
Para obter mais informações, consulte [Login em instâncias do Linux](https://intl.cloud.tencent.com/document/product/213/5436) e [Login em instâncias do Windows](https://intl.cloud.tencent.com/document/product/213/5435).
2. Para obter o endereço IP público, você pode acessar os metadados usando a ferramenta cURL ou uma solicitação HTTP GET.
```
curl http://metadata.tencentyun.com/meta-data/public-ipv4
```
Se o valor retornado estiver na seguinte estrutura, é possível visualizar o endereço IP público:
![](https://main.qcloudimg.com/raw/03f603e433b7a5da09e33a8b09d731b4.png)
Para obter mais informações, consulte os [Metadados da instância](http://intl.cloud.tencent.com/document/product/213/4934).
