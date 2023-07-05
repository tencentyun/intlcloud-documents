Os metadados da instância referem-se aos dados relevantes para uma instância. Eles podem ser usados para configurar ou gerenciar uma instância em execução.
>? Embora os metadados da instância só possam ser acessados após o login, os dados não foram criptografados. Qualquer pessoa que acessar a instância pode visualizar seus metadados. Portanto, você deve tomar as medidas adequadas para proteger os dados confidenciais.
>


## Visão geral
O Tencent Cloud fornece os seguintes metadados:

<table>
<thead>
<tr>
<th>Nome</th>
<th width="50%">Descrição</th>
<th width="15%">Versão</th>
</tr>
</thead>
<tbody><tr>
<td>instance-id</td>
<td>ID da instância</td>
<td>1,0</td>
</tr>
<tr>
<td>instance-name</td>
<td>Nome da instância</td>
<td>1,0</td>
</tr>
<tr>
<td>uuid</td>
<td>ID exclusiva da instância</td>
<td>1,0</td>
</tr>
<tr>
<td>local-ipv4</td>
<td>Endereço IP privado da instância</td>
<td>1,0</td>
</tr>
<tr>
<td>public-ipv4</td>
<td>Endereço IP público da instância</td>
<td>1,0</td>
</tr>
<tr>
<td>mac</td>
<td>Endereço MAC do dispositivo eth0 da instância</td>
<td>1,0</td>
</tr>
<tr>
<td>placement/region</td>
<td>Região da instância</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>placement/zone</td>
<td>Zona de disponibilidade da instância</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/mac</td>
<td>Endereço MAC da interface de rede da instância</td>
<td>1,0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/primary-local-ipv4</td>
<td>IP privado principal da interface de rede da instância</td>
<td>1,0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/public-ipv4s</td>
<td>Endereço IP público da interface de rede da instância</td>
<td>1,0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/vpc-id</td>
<td>ID do VPC da interface de rede da instância</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/subnet-id</td>
<td>ID da sub-rede da interface de rede da instância</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/gateway</td>
<td>Endereço de gateway da interface de rede da instância</td>
<td>1,0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/local-ipv4</td>
<td>Endereço IP privado da interface de rede da instância</td>
<td>1,0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/public-ipv4</td>
<td>Endereço IP público da interface de rede da instância</td>
<td>1,0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/public-ipv4-mode</td>
<td>Modo da rede pública da interface de rede da instância</td>
<td>1,0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/subnet-mask</td>
<td>Máscara da sub-rede da interface de rede da instância</td>
<td>1,0</td>
</tr>
<tr>
<td>payment/charge-type</td>
<td>Plano de faturamento da instância</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>payment/create-time</td>
<td>Hora de criação da instância</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>payment/termination-time</td>
<td>Hora de encerramento da instância</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>app-id</td>
<td>AppID do proprietário da instância</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>as-group-id</td>
<td>ID do grupo do Auto Scaling da instância</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>spot/termination-time</td>
<td>Horário de encerramento da instância spot</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>/meta-data/instance/instance-type</td>
<td>Tipo de instância</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>/instance/image-id</td>
<td>ID da imagem da instância</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>/instance/security-group</td>
<td>Informações do grupo de segurança vinculado à instância</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>/instance/bandwidth-limit-egress</td>
<td>Limite de largura de banda de saída da rede privada da instância, em Kbit/s</td>
<td>29/09/2019</td>
</tr>
<tr>
<td>/instance/bandwidth-limit-ingress</td>
<td>Limite de largura de banda de entrada da rede privada da instância, em Kbit/s</td>
<td>29/09/2019</td>
</tr>
<tr>
<td>/cam/security-credentials/${role-name}</td>
<td>Credencial temporária gerada pela política de funções do CAM, que pode ser obtida apenas quando a instância está associada à função do CAM. Mude `${role-name}` para o nome real da função do CAM; caso contrário, `404` será retornado</td>
<td>11/12/2019</td>
</tr>
</tbody></table>

>? 
> - Os campos `${mac}` e `${local-ipv4}` na tabela acima indicam o endereço MAC e o endereço IP privado da interface de rede especificada para a instância, respectivamente.
> - O endereço URL de destino da solicitação diferencia maiúsculas de minúsculas. Você deve criar o endereço URL de destino de uma nova solicitação de acordo com o resultado retornado da solicitação.
> - Os dados retornados de `placement` são alterados na nova versão. Para usar os dados na versão anterior, especifique o caminho dela ou deixe o caminho da versão vazio para acessar os dados da versão 1.0. Para obter mais informações sobre os dados retornados de `placement`, consulte as [Regiões e zonas de disponibilidade](https://intl.cloud.tencent.com/document/product/213/6091).

## Consulta de metadados da instância
Depois de fazer login em uma instância, você pode acessar os metadados, como seu endereço IP local e endereço IP público para gerenciar conexões com aplicativos externos.
Para visualizar todos os metadados da instância em uma instância em execução, use o seguinte URI:

```
http://metadata.tencentyun.com/latest/meta-data/
```
Você pode acessar os metadados usando a ferramenta cURL ou uma solicitação HTTP GET, por exemplo:

```
curl http://metadata.tencentyun.com/latest/meta-data/
```
* Para recursos que não existem, o código de erro HTTP "404 - Not Found (404 - Não encontrado)" será retornado.
* Para operar nos metadados da instância, primeiro faça login na instância. Para obter mais informações, consulte [Login em uma instância do Windows usando o RDP (recomendado)](https://intl.cloud.tencent.com/document/product/213/5435) e [Login em uma instância do Linux usando o método de login padrão](https://intl.cloud.tencent.com/document/product/213/5436).

### Exemplo de consulta de metadados

O exemplo a seguir mostra como obter a versão dos metadados.
>! Quando o Tencent Cloud modifica o caminho de acesso aos metadados ou os dados retornados, uma nova versão dos metadados é lançada. Se seu aplicativo ou script depender da estrutura ou dos dados retornados da versão anterior, você poderá acessar os metadados usando a versão anterior especificada. Se nenhuma versão for especificada, a versão 1.0 será acessada por padrão.
>

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/
1,0
2017-09-19
latest
meta-data
```

O exemplo a seguir mostra como visualizar o diretório raiz de metadados. As linhas que terminam com `/` representam os diretórios e as outras linhas representam os dados acessados. Para obter a descrição dos dados acessados, consulte a seção **Visão geral** descrita acima.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/
instance-id
instance-name
local-ipv4
mac
network/
placement/
public-ipv4
uuid
```

O exemplo a seguir mostra como obter as informações de localização física de uma instância. Para saber a relação entre os dados retornados e a localização física, consulte as [Regiões e zonas de disponibilidade](https://intl.cloud.tencent.com/document/product/213/6091).

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/placement/region
ap-guangzhou

[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/placement/zone
ap-guangzhou-3
```

O exemplo a seguir mostra como obter o endereço IP privado de uma instância. Se uma instância tiver vários ENIs, o endereço de rede do dispositivo eth0 será retornado.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/local-ipv4
10.104.13.59
```

O exemplo a seguir mostra como obter o endereço IP público de uma instância.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/public-ipv4
139.199.11.29
```

O exemplo a seguir mostra como obter o ID de uma instância. O ID da instância é usado para identificar exclusivamente uma instância.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/instance-id
ins-3g445roi
```

O exemplo a seguir mostra como consultar o UUID da instância. O UUID da instância também pode ser usado como o identificador exclusivo de uma instância, mas recomendamos que você use o ID da instância para identificá-las.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/uuid
cfac763a-7094-446b-a8a9-b995e638471a
```

O exemplo a seguir mostra como obter o endereço MAC do dispositivo eth0 de uma instância.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/mac
52:54:00:BF:B3:51
```

O exemplo a seguir mostra como obter as informações do ENI de uma instância. No caso de vários ENIs, várias linhas de dados são retornadas, com cada linha indicando o diretório de dados de um ENI.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/
52:54:00:BF:B3:51/
```

O exemplo a seguir mostra como obter as informações de um ENI especificado.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/
local-ipv4s/
mac
vpc-id
subnet-id
owner-id
primary-local-ipv4
public-ipv4s
local-ipv4s/
```

O exemplo a seguir mostra como obter as informações do VPC de um ENI especificado.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/vpc-id
vpc-ja82n9op

[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/subnet-id
subnet-ja82n9op
```

O exemplo a seguir mostra como obter a lista de endereços IP privados vinculados ao ENI especificado. Se o ENI estiver vinculado a vários endereços IP privados, várias linhas de dados serão retornadas.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/
10.104.13.59/
```

O exemplo a seguir mostra como obter as informações de um endereço IP privado.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59
gateway
local-ipv4
public-ipv4
public-ipv4-mode
subnet-mask
```

O exemplo a seguir mostra como obter o gateway de um endereço IP privado. Esses dados estão disponíveis apenas para os modelos do CVM baseados no VPC. Para obter mais informações, consulte [Virtual Private Cloud (VPC)](https://intl.cloud.tencent.com/document/product/215).

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/gateway
10.15.1.1
```

O exemplo a seguir mostra como obter o modo de acesso usado por um endereço IP privado para acessar a rede pública. Esses dados podem ser consultados apenas para os CVMs baseados no VPC. Um CVM baseado na rede clássica acessa a rede pública por meio do gateway público.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/public-ipv4-mode
NAT
```

O exemplo a seguir mostra como obter o endereço IP público vinculado a um endereço IP privado.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/public-ipv4
139.199.11.29
```

O exemplo a seguir mostra como obter a máscara da sub-rede de um endereço IP privado.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/subnet-mask
255.255.192.0
```

O exemplo a seguir mostra como obter o tipo de faturamento de uma instância.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/payment/charge-type
POSTPAID_BY_HOUR
```

O exemplo a seguir mostra como obter a hora de criação de uma instância.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/payment/create-time
18/09/2018 11:27:33
```


O exemplo a seguir mostra como obter a hora de encerramento para instâncias spot.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/spot/termination-time
18/08/2018 12:05:33
```

O exemplo a seguir mostra como obter o AppID da conta à qual o CVM pertence.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/app-id
123456789
```

O exemplo a seguir mostra como obter a credencial temporária gerada pela função do CAM à qual a instância pertence. Neste exemplo, o nome da função é `CVMas`.
```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/cam/security-credentials/CVMas
{
  "TmpSecretId": "AKIDoQMxF8OPg0gA7pyZIA6cW447p225cIt9NW8dhA1dwl5UvxxxxxxxxxUqRlEb5_",
  "TmpSecretKey": "Q9z24VucjF4xQQNV64qwF6uWY71PEsH3exxxxxxxxxgA=",
  "ExpiredTime": 1615590047,
  "Expiration": "2021-03-12T23:00:47Z",
  "Token": "xxxxxxxxxxx",
  "Code": "Success"
}
```

## Consulta dos dados do usuário da instância
Você pode especificar os dados do usuário da instância ao criar uma instância. As instâncias do CVM com o cloud-init configurado podem acessar os dados.

### Pesquisa de dados do usuário
Após o login, você pode acessar os dados do usuário usando o método a seguir.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/user-data
179, client, shanghai
```
