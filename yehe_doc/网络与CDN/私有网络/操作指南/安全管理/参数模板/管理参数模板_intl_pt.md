Um modelo de parâmetros consiste em um conjunto de parâmetros. Você pode salvar endereços IP e portas de protocolo como um modelo, para que possa importá-lo diretamente ao adicionar regras de grupo de segurança. Os modelos de parâmetros, se usados corretamente, podem aumentar sua eficiência no uso de grupos de segurança.
O Tencent Cloud aceita quatro tipos de modelos de parâmetros:
- Endereço IP (ipm): aceita um único endereço IP, bloco CIDR e intervalo de endereços IP.
- Grupo de endereços IP (ipmg): aceita um grupo de objetos de endereços IP.
- Porta de protocolo (ppm): aceita uma única porta, várias portas, portas consecutivas e todas as portas. Os protocolos aceitos são TCP, UDP, ICMP e GRE.
- Grupo de portas de protocolo (ppmg): aceita um grupo de objetos de portas de protocolo.

## Cenários
Os modelos de parâmetros se aplicam aos seguintes cenários:
- Gerenciar vários endereços IP ou grupos de portas de protocolo com os mesmos requisitos.
- Gerenciar vários endereços IP ou grupos de portas de protocolo com necessidades de edição frequentes.

## Etapa 1: Criar um modelo de parâmetros
### 1. Crie um modelo de parâmetros de endereços IP
Adicione endereços IP com os mesmos requisitos ou necessidades de edição frequentes ao objeto de endereço IP.
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Security (Segurança)** >**Parameter Template (Modelo de parâmetros)** na barra lateral esquerda para acessar a página de gerenciamento.
3. Na página da guia **IP Address (Endereço IP)**, clique em **+New (+Novo)**.
4. Na caixa pop-up, digite o nome e o endereço IP e clique em **Submit (Enviar)**.
Para adicionar vários endereços IP, separe-os com quebras de linha. Apenas endereços IPv4 nos seguintes formatos são aceitos:
 - Um único endereço IP, por exemplo, `10.0.0.1`;
 - Um intervalo de IP, por exemplo, `10.0.1.0/24`; 
 - Endereços IP consecutivos, por exemplo, `10.0.0.1` - `10.0.0.100`.
![](https://main.qcloudimg.com/raw/64ecfd48ffdc728506ef328a0ee19921.png)
5. (Opcional) Você pode adicionar vários endereços IP criados a um grupo, para criar um grupo de endereços IP.
	1. Clique na guia **IP Address Group (Grupo de endereços IP)** para acessar a página de gerenciamento. Nesta página, clique em **+New (+Novo)**.
	2. Na caixa pop-up, digite o nome, selecione os endereços IP que deseja adicionar e clique em **Submit (Enviar)**.
	![](https://main.qcloudimg.com/raw/5b40b996461455a77b723cdd828fd4f3.png)

### 2. Crie um modelo de parâmetros de portas de protocolo
Adicione portas de protocolo com os mesmos requisitos ou necessidades de edição frequentes ao objeto de portas de protocolo.
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Security (Segurança)** >**Parameter Template (Modelo de parâmetros)** na barra lateral esquerda para acessar a página de gerenciamento.
3. Clique na guia **Protocol Port (Porta de protocolo)** para acessar a sua página. Nesta página de guia, clique em **+New (+Novo)**.
4. Na caixa pop-up, digite o nome e a porta do protocolo e clique em **Submit (Enviar)**.
Para adicionar várias portas de protocolo, separe-as com quebras de linha. Os seguintes formatos de portas de protocolo são aceitos:
	- Uma única porta, por exemplo, `TCP:80`;
	- Várias portas discretas, por exemplo, `TCP:80,443`;
	- Portas consecutivas, por exemplo, `TCP:3306-20000`;
	- Todas as portas, por exemplo, `TCP:ALL`.
![](https://main.qcloudimg.com/raw/aae45c5c950f4e6b6cc75aaedebc48e3.png)
5. (Opcional) Você pode adicionar várias portas de protocolo criadas a um grupo, para criar um grupo de portas de protocolo.
	1. Clique na guia **Protocol Port Group (Grupo de portas de protocolo)** para acessar a página de gerenciamento. Nesta página, clique em **+New (+Novo)**.
	2. Na caixa pop-up, digite o nome, selecione as portas de protocolo que deseja adicionar e clique em **Submit (Enviar)**.
	![](https://main.qcloudimg.com/raw/91f6da2d037239206dcadbdf9a02570a.png)

## Etapa 2: Importar um modelo de parâmetros em um grupo de segurança
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Security (Segurança)** > **Security Group (Grupo de segurança)** na barra lateral esquerda para acessar a página de gerenciamento.
3. Na lista, localize o grupo de segurança para o qual um modelo de parâmetros precisa ser importado e clique em seu ID para acessar a página de detalhes.
4. Na página da guia **Inbound Rules or Outbound Rules (Regras de entrada ou Regras de saída)**, clique em **Add Rules (Adicionar regras)**.
5. Na caixa pop-up, escolha o modelo de parâmetros correspondente para porta de origem e de protocolo. Para obter instruções detalhadas sobre como adicionar regras de entrada e saída, consulte [Adição de regras de grupo de segurança](https://intl.cloud.tencent.com/document/product/215/35513).
>? Em seguida, se você precisar adicionar novos endereços IP ou portas de protocolo, basta adicioná-los ao grupo de endereços IP ou grupo de portas de protocolo correspondente, sem ter que modificar as regras do grupo de segurança, ou criar outro grupo.
>
![](https://main.qcloudimg.com/raw/3a06123b12ef4814c0c95e33418952cc.png)

