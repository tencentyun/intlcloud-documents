Este documento descreve como obter o endereço IP privado da instância e configurar o DNS privado.

## Obtenção do endereço IP privado de uma instância
### Obtenção do endereço IP privado no console
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
2. Na página de gerenciamento da instância, selecione a instância e mova o mouse para a coluna **Primary IP (IP principal)** para visualizar seu IP privado e clique em <img src = "https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style = "margin: 0;"> para copiar o IP privado, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/f4849355a4890861e2d07b35de1099a4.png)

### Obtenção do endereço IP privado usando API
Consulte [API DescribeInstances](https://intl.cloud.tencent.com/document/product/213/33258).

### Obtenção do endereço IP privado usando metadados da instância

1. Faça login no CVM.
2. Acesse os metadados da instância usando a ferramenta cURL ou uma solicitação HTTP GET.
> As seguintes operações usam a ferramenta cURL como exemplo.
>
Execute o seguinte comando para obter o IP privado.
```
curl http://metadata.tencentyun.com/meta-data/local-ipv4
```
A informação retornada é o endereço IP privado, conforme mostrado abaixo:
![](https://mc.qcloudimg.com/static/img/14a13eccebc7eee6f83bc026adb30902/image.png)

Para obter mais informações sobre os metadados da instância, consulte [Metadados da instância](http://intl.cloud.tencent.com/document/product/213/4934).

## Configuração do DNS da rede privada 
Quando ocorre um erro de resolução de rede, você pode configurar manualmente o DNS da rede privada com base no sistema operacional do seu CVM.

### Para o sistema operacional Linux

1. Faça login no CVM do Linux.
2. Execute o seguinte comando para abrir o arquivo `/etc/resolv.conf`.
```
vi /etc/resolv.conf
```
3. Pressione **i** para alternar para o modo de edição e modifique o IP do DNS de acordo com a região correspondente na lista de [DNS da rede privada](https://intl.cloud.tencent.com/document/product/213/5225).
Por exemplo, para alterar o IP do DNS da rede privada para um servidor DNS da rede privada na região de Pequim.
```
nameserver 10.53.216.182
nameserver 10.53.216.198
options timeout:1 rotate
```
4. Pressione **Esc**, digite **:wq**, salve o arquivo e retorne.

### Para o sistema operacional Windows

1. Faça login no CVM do Windows.
2. Na interface do sistema operacional, abra o **Control Panel (Painel de controle)** > **Network and Sharing Center (Central de rede e compartilhamento)** > **Change adapter settings (Alterar configurações do adaptador)**.
3. Clique com o botão direito em **Ethernet** e selecione **Properties (Propriedades)** para abrir a janela “Ethernet Properties (Propriedades de Ethernet)”.
4. Na janela “Ethernet Properties (Propriedades de Ethernet)”, clique duas vezes em **IP version 4 (TCP/IPv4) (IP versão 4 (TCP/IPv4))**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/1eef10b5919ba4db272fa0fc21fb1702.png)
5. Selecione [Use the following DNS server address (Usar o seguinte endereço de servidor DNS)] e modifique o IP do DNS de acordo com a região correspondente na lista [DNS da rede privada](https://intl.cloud.tencent.com/document/product/213/5225).

6. Clique em **OK**.
