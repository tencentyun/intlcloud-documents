Este documento descreve como criar e manter modelos de parâmetros (endereços IP, grupo de endereços IP, portas de protocolo e grupo de portas de protocolo) no console, e como usá-los em grupos de segurança.


## Criação de modelo de parâmetros

### Criação de modelo de parâmetros de endereços IP
Adicione os IPs com as mesmas necessidades ou que são editados com frequência a este objeto de endereço IP.

#### Instruções
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Security (Segurança)** >**Parameter Template (Modelo de parâmetros)** na barra lateral esquerda, para acessar a página de gerenciamento.
3. Selecione a guia **IP Address (Endereço IP)** e clique em **+New (+Novo)**.
4. Na janela pop-up, insira o nome e os endereços IP, e clique em **Submit (Enviar)**.
 Você pode adicionar vários endereços IPv4 nos seguintes intervalos e separá-los por quebras de linha:
 - Endereço IP único: como `10.0.0.1`;
 - Bloco CIDR: como `10.0.1.0/24`; 
 - Intervalo de IP: como `10.0.0.1` - `10.0.0.100`.
![](https://main.qcloudimg.com/raw/64ecfd48ffdc728506ef328a0ee19921.png)

### Criação de modelo de parâmetros de grupo de endereços IP
Você pode adicionar vários objetos de endereço IP a um grupo de endereços IP para gerenciamento unificado.

#### Instruções
1. Selecione a guia **IP Address Group (Grupo de endereços IP)** e clique em **+New (+Novo)**.
	![](https://qcloudimg.tencent-cloud.cn/raw/333211f6e4bb94b7611cb6d4bb327c98.png)
2. Na janela pop-up, insira o nome, selecione os objetos de endereço IP a serem adicionados e clique em **Submit (Enviar)**.
	![](https://main.qcloudimg.com/raw/5b40b996461455a77b723cdd828fd4f3.png)

### Criação de um modelo de parâmetros de portas de protocolo
Você pode adicionar as portas de protocolo com as mesmas necessidades ou que são editadas com frequência a este objeto de porta de protocolo.

#### Instruções
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Security (Segurança)** >**Parameter Template (Modelo de parâmetros)** na barra lateral esquerda, para acessar a página de gerenciamento.
3. Selecione a guia **Protocol Port (Porta de protocolo)** e clique em **+New (+Novo)**.
4. Na janela pop-up, insira o nome e as portas de protocolo e clique em **Submit (Enviar)**.
   Você pode adicionar várias portas de protocolo nos seguintes intervalos e separá-las com quebras de linha:
	- Porta única: como `TCP:80`;
	- Várias portas: como `TCP:80,443`;
	- Intervalo de portas: como `TCP:3306-20000`;
	- Todas as portas: como `TCP:ALL`.
![](https://main.qcloudimg.com/raw/aae45c5c950f4e6b6cc75aaedebc48e3.png)

### Criação de um modelo de parâmetros de grupo de portas de protocolo
Você pode adicionar vários objetos de porta de protocolo criados a um grupo de portas de protocolo para gerenciamento unificado.
#### Instruções	
1. Selecione a guia **Protocol Port Group (Grupo de portas de protocolo)** e clique em **+New (+Novo)**.
	![](https://qcloudimg.tencent-cloud.cn/raw/5101e8b5139198a06f6d2a28036af32a.png)
2. Na janela pop-up, insira o nome, selecione o objeto de porta de protocolo a ser adicionado e clique em **Submit (Enviar)**.
	![](https://main.qcloudimg.com/raw/91f6da2d037239206dcadbdf9a02570a.png)

## Modificação de modelo de parâmetros
Se você precisar modificar um modelo de parâmetros criado, por exemplo, para adicionar/excluir endereços IP ou portas de protocolo, siga as etapas abaixo.

### Instruções
1. Clique no modelo de parâmetros de endereços IP, grupo de endereços IP, portas de protocolo ou grupo de portas de protocolo criado e clique em **Edit (Editar)** à direita. Por exemplo, a figura a seguir mostra como modificar os objetos de endereço IP.
    ![](https://qcloudimg.tencent-cloud.cn/raw/cbb3cb328b614baad17cd236fbe5cb61.png)
2. Na janela pop-up, modifique os parâmetros correspondentes e clique em **Submit (Enviar)**.
   
## Exclusão de modelo de parâmetros
Se você não usar mais um modelo de parâmetros, poderá excluí-lo. Quando esse modelo é excluído, todas as configurações de política que o contêm no grupo de segurança serão excluídas ao mesmo tempo. Avalie e prossiga com cautela.

### Instruções
1. Clique em **Delete (Excluir)** à direita do modelo de parâmetros criado.
   ![](https://qcloudimg.tencent-cloud.cn/raw/bc33be2141b5b267ba2d56cd40793258.png)
2. Quando esse modelo for excluído, todas as políticas que contenham o endereço IP ou a porta de protocolo correspondente também serão excluídas. Depois de confirmar que tudo está correto, clique em **Delete (Excluir)** na janela pop-up **Confirm Deletion (Confirmar exclusão)**.

## Importação do modelo de parâmetros para o grupo de segurança
Depois de criar um modelo de parâmetros, você pode importá-lo diretamente ao adicionar regras em um grupo de segurança para adicionar com rapidez origens de IP ou portas de protocolo, o que ajuda a melhorar sua eficiência ao adicionar regras de grupo de segurança.

### Instruções
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Security (Segurança)** >**Security Group (Grupo de segurança)** na barra lateral esquerda, para acessar a página de gerenciamento.
3. Na lista, localize o grupo de segurança que precisa importar o modelo de parâmetros e clique em seu ID para acessar a página de detalhes.
4. Na guia **Inbound/Outbound Rules (Regras de entrada/saída)**, clique em **Add Rule (Adicionar regra)**.
5. Na janela pop-up, selecione o tipo **Custom (Personalizada)**, selecione o modelo de parâmetros criado em **Source (Origem)** e **Protocol Port (Porta de protocolo)**, e clique em **Complete (Concluir)**. Para mais informações sobre como adicionar regras de entrada/saída, consulte [Adição de uma regra de grupo de segurança](https://intl.cloud.tencent.com/document/product/215/35513).
>?Se você precisar adicionar um novo endereço IP ou porta de protocolo no futuro, basta adicioná-lo ao grupo de endereços IP ou ao grupo de portas de protocolo correspondente, e não há necessidade de modificar as regras do grupo de segurança ou criar outro grupo de segurança.
>
 ![](https://main.qcloudimg.com/raw/3a06123b12ef4814c0c95e33418952cc.png)

## Exibição do grupo de segurança associado
Você pode exibir todas as instâncias dos grupos de segurança que importam um modelo de parâmetros nas etapas a seguir.
1. Clique em **View Association (Exibir associação)** à direita do modelo de parâmetros criado.
    ![](https://qcloudimg.tencent-cloud.cn/raw/1a56775ee22def20e25cb6d54548712d.png)
2. A lista de grupos de segurança associados exibida mostra todas as instâncias dos grupos de segurança associadas a esse modelo de parâmetros.
   ![](https://qcloudimg.tencent-cloud.cn/raw/128b47cf7b2c8e2e9bf0f6a3bbbd37cf.png)
