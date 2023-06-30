Os serviços de rede privada são serviços de LAN, onde os serviços em nuvem conseguem comunicar-se entre si por meio de vínculos internos. Os serviços do Tencent Cloud conseguem comunicar-se entre si por meio do [acesso à internet](https://intl.cloud.tencent.com/document/product/213/5224) ou da rede privada do Tencent Cloud. Os data centers do Tencent Cloud estão interconectados com redes subjacentes de megabytes/gigabytes. Eles permitem comunicações por meio de redes privadas com grande largura de banda e baixa latência, que são gratuitas (se estiverem na mesma região) para ajudar você a criar uma arquitetura de rede de forma flexível.
## Endereço IP privado
### Visão geral
Os IPs privados são endereços que não podem ser acessados pela internet, dependendo de quais redes privadas do Tencent Cloud são criadas. Cada instância tem uma interface de rede padrão (ou seja, eth0) para atribuir IPs privados. Os IPs privados podem ser atribuídos automaticamente pelo Tencent Cloud ou você pode personalizá-los (somente com o [VPC](https://intl.cloud.tencent.com/document/product/215/535)).
> Caso você altere o IP privado dentro do sistema operacional, a rede privada poderá ser interrompida.
>

### Atributos
 - A rede privada é inerente ao usuário e os demais são isolados entre si. Por padrão, os serviços em nuvem de outro usuário não podem ser acessados por meio da rede privada.
 - A rede privada é inerente à região e as demais são isoladas umas das outras. Por padrão, os serviços em nuvem sob a mesma conta em uma região diferente não podem ser acessados por meio da rede privada.

### Cenários de aplicação
O IP privado pode ser usado para a comunicação entre CLBs e instâncias do CVM, e entre instâncias do CVM e outros serviços do Tencent Cloud (como o TencentDB).

### Atribuição de endereço
Cada instância do CVM receberá um endereço IP privado padrão ao iniciar. O IP privado varia de acordo com o [ambiente de rede](https://intl.cloud.tencent.com/document/product/213/5227):
 - Rede básica: o endereço IP privado é atribuído automaticamente pelo Tencent Cloud e não pode ser alterado.
 - VPC: atualmente, o Tencent Cloud VPC CIDR permite que você use um dos seguintes intervalos de IP e as máscaras máxima e mínima são /16 e /28:
  - **10.0**.0.0 - **10.255**.255.255
  - **172.16**.0.0 - **172.31**.255.255
  - **192.168**.0.0 - **192.168**.255.255

## DNS de rede privada 
### Endereço do servidor DNS
O serviço de DNS de rede privada é usado para a resolução de nomes de domínio. Se o DNS for configurado incorretamente, o nome de domínio não poderá ser acessado.
O Tencent Cloud fornece servidores DNS de rede privada confiáveis em diferentes regiões. Veja as configurações específicas abaixo:
<table><tbody>
<tr><th>Ambiente de rede</th><th>Região</th><th>Servidor DNS de rede privada</th></tr>
<tr><td rowspan="14">Rede básica</td><td rowspan="4">Guangzhou</td><td>Zona 1 de Guangzhou: <br>10.112.65.31<br>10.112.65.32</td></tr>
<tr><td>Zona 2 de Guangzhou: <br>10.112.65.31<br>10.112.65.32</td></tr>
<tr><td>Zona 3 de Guangzhou: <br>10.59.218.193<br>10.59.218.194</td></tr>
<tr><td>Zona 4 de Guangzhou: <br>100.121.190.140<br>100.121.190.141</td></tr>
<tr><td>Xangai</td><td>10.236.158.114<br>10.236.158.106</td></tr>
<tr><td>Pequim</td><td>10.53.216.182<br>10.53.216.198</td></tr>
<tr><td>América do Norte</td><td>10.116.19.188<br>10.116.19.185</td></tr>
<tr><td>Hong Kong, China</td><td>10.243.28.52<br>10.164.55.3</td></tr>
<tr><td>Singapura</td><td>100.78.90.19<br>100.78.90.8</td></tr>
<tr><td>Zona Livre de Guangzhou</td><td>10.59.218.18<br>10.112.65.51</td></tr>
<tr><td>Chengdu</td><td>100.88.222.14<br>100.88.222.16</td></tr>
<tr><td>Vale do Silício</td><td>100.102.22.21<br>100.102.22.30</td></tr>
<tr><td>Frankfurt</td><td>100.120.52.60<br>100.120.52.61</td></tr>
<tr><td>Seul</td><td>10.165.180.53<br>10.165.180.62</td></tr>
<tr><td>VPC</td><td>Todas as regiões</td><td>183.60.83.19<br>183.60.82.98</td></tr>
</tbody>
</table>

## Guia de operação
Você pode exibir ou modificar o endereço IP privado da instância. Para obter instruções detalhadas, consulte:
- [Obtenção do endereço IP privado de uma instância e configurações de DNS de rede privada](https://intl.cloud.tencent.com/document/product/213/17941)
- [Modificação de endereços IP privados](https://intl.cloud.tencent.com/document/product/213/16561)
