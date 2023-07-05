## Cenário

Para permitir que você nomeie as instâncias do CVM criadas em lote de acordo com uma regra durante a criação, as funcionalidades de Sufixos Numéricos Crescentes Automaticamente e Especificar as Strings de Padrão são fornecidas.

- Quando for necessário adquirir n instâncias e gerar nomes de instâncias em formatos específicos, como “CVM+número de sequência” (por exemplo, CVM 1, CVM 2 e CVM 3), é possível usar a funcionalidade de [Sufixos Numéricos Crescentes Automaticamente](#AutoAscending).
- Quando for necessário criar **n** instâncias e nomear instâncias específicas com números crescentes a partir de **x**, é possível usar a funcionalidade de [Especificar uma Única String de Padrão](#SpecifySingleString).
- Quando for necessário criar n instâncias com vários prefixos em seus nomes, cada um dos quais contém um número de série especificado, você pode usar a funcionalidade de [Especificar Várias Strings de Padrão](#SpecifyMultipleStrings).


## Etapas

<span id="AutoAscending"></span>
### Sufixos Numéricos Crescentes Automaticamente

Esta funcionalidade permite nomear instâncias adquiridas em lote com o mesmo prefixo e com números como sufixo de forma crescente e automática.
> As instâncias criadas são sufixadas com números começando em 1 por padrão. O número do sufixo inicial é fixo.
>
O exemplo a seguir considera que você adquiriu três instâncias e deseja nomeá-las no formato “CVM+número de sequência” (por exemplo, CVM 1, CVM 2 e CVM 3).

#### Operações na página de aquisição

1. Adquira três instâncias, consultando [Criação de uma instância](http://intl.cloud.tencent.com/document/product/213/4855). Na página da guia **2. Security Group and CVM (2. Grupo de segurança e CVM)**, insira o nome da instância no formato **Prefixo+número de sequência**. Nesse caso, insira `CVM` como o nome da instância.
![](https://main.qcloudimg.com/raw/820a52077080be5da4c1fb4715452e6b.png)
2. Siga as instruções na página e conclua o pagamento.
3. Retorne ao [Console do CVM](https://console.cloud.tencent.com/cvm/index) para visualizar as instâncias recém-adquiridas. Observe que essas instâncias adquiridas em lote são nomeadas com o mesmo prefixo e com sufixos numéricos crescentes.
![](https://main.qcloudimg.com/raw/27de624cd251910d47bea8e7732b284b.png)

#### Operações de API

Na API [RunInstances](https://intl.cloud.tencent.com/document/product/213/33237), defina o campo InstanceName como `CVM`.

### Especificar Strings de Padrão

Esta funcionalidade permite nomear instâncias adquiridas em lote de uma forma complexa com números de série especificados. É possível usar uma ou mais strings de padrão em nomes de instâncias, conforme necessário.

O nome da instância com uma string de padrão especificada fica no formato **{R:x}**, em que **x** indica o número inicial nos nomes das instâncias geradas.

<span id="SpecifySingleString"></span>
#### Especificar uma Única String de Padrão

O exemplo a seguir considera que você deseja criar três instâncias e nomeá-las com números crescentes começando em 3.

##### Operações na página de aquisição

1. Adquira três instâncias, consultando [Criação de uma instância](http://intl.cloud.tencent.com/document/product/213/4855). Na página da guia **2. Set the CVM (2. Definir o CVM)**, insira o nome da instância no formato **Prefixo+String de padrão especificada {R:x}**. Nesse caso, insira `CVM{R:3}` como o nome da instância.
![](https://main.qcloudimg.com/raw/4e09732d612222f619cf7a1e8da1ee06.png)
2. Siga as instruções na página e conclua o pagamento.
3. Retorne ao [Console do CVM](https://console.cloud.tencent.com/cvm/index) para visualizar as instâncias recém-adquiridas. Observe que essas instâncias adquiridas em lote são nomeadas com o mesmo prefixo e com sufixos numéricos crescentes, começando em 3.
![](https://main.qcloudimg.com/raw/78dc40cf4baa707573ad95a77bed4e1d.png)

##### Operações de API

Na API [RunInstances](https://intl.cloud.tencent.com/document/product/213/33237), defina o campo InstanceName como `CVM{R:3}`.

<span id="SpecifyMultipleStrings"></span>
#### Especificar Várias Strings de Padrão

O exemplo a seguir considera que você deseja criar três instâncias e nomeá-las com os prefixos **cvm**, **Big** e **test**, em que **cvm** e **Big** são seguidos por números crescentes a partir de 13 e 2, respectivamente. Por exemplo, seus nomes são cvm13-Big2-test, cvm14-Big3-test e cvm15-Big4-test, respectivamente.

##### Operações na página de aquisição

1. Adquira três instâncias, consultando [Criação de uma instância](http://intl.cloud.tencent.com/document/product/213/4855). Na página da guia **2. Set the CVM (2. Definir o CVM)**, insira o nome da instância no formato **Prefixo+String de padrão especificada {R:x}-Prefixo+String de padrão especificada {R:x}-Prefixo**. Nesse caso, insira `cvm{R:13}-Big{R:2}-test` como o nome da instância.
![](https://main.qcloudimg.com/raw/1042e86262bc7ce3939f1842a8025c23.png)
2. Siga as instruções na página e conclua o pagamento.
3. Retorne ao [Console do CVM](https://console.cloud.tencent.com/cvm/index) para visualizar as instâncias recém-adquiridas. Observe que essas instâncias adquiridas em lote são nomeadas com prefixos seguidos por números crescentes a partir dos números especificados.
![](https://main.qcloudimg.com/raw/a3c5e58daf07381ffde5abc019edad33.png)

##### Operações de API

Na API [RunInstances](https://intl.cloud.tencent.com/document/product/213/33237), defina o campo InstanceName como `cvm{R:13}-Big{R:2}-test`.

