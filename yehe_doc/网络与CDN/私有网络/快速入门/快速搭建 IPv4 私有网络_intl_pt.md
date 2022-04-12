Este tutorial descreve como criar rapidamente uma Virtual Private Cloud (VPC) com blocos CIDR IPv4.
## Visão geral
Este documento orienta todo o processo de configuração de uma VPC baseado em IPv4. 
![](https://qcloudimg.tencent-cloud.cn/raw/926843feffd998e8dbf151b63178b366.png)

## Pré-requisitos
Certifique-se de ter [criado uma conta da Tencent Cloud](https://intl.cloud.tencent.com/register) e concluído a [verificação de identidade](https://intl.cloud.tencent.com/document/product/378/3629), se precisar adquirir recursos na China Continental.

## Instruções
### Etapa 1: criar uma VPC e uma sub-rede
>? Após criar uma VPC e uma sub-rede, você não pode modificar os blocos CIDR. Portanto, conclua o [planejamento de rede](https://intl.cloud.tencent.com/document/product/215/31795) com antecedência.
>
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Selecione a região da VPC na parte superior e clique em **+New (+Novo)**.
3. Na janela pop-up **Create VPC (Criar VPC)**, configure as informações da VPC e da sub-rede conforme as instruções abaixo.
![](https://qcloudimg.tencent-cloud.cn/raw/ba0387f51ed8112ab819d5cb9c5113b5.png)
 - **Informações da VPC*
    - Name (Nome): o nome da VPC.
    - IPV4 CIDR Block (Bloco CIDR IPV4): você pode escolher qualquer um desses intervalos de IP **10.0**.0.0 - **10.255**.255.255, **172.16**.0.0 - **172.31**.255.255 e 
    **192.168**.0.0 - **192.168**.255.255 como o intervalo de IP da VPC. O intervalo da máscara deve ser de 16 a 28, como `10.0.0.0/16`.
     - Advanced options (Opções avançadas): opcionalmente, é possível adicionar tags para ajudar você a melhorar o gerenciamento das permissões de recursos de subusuários e colaboradores.
  - **Informações da sub-rede**
    -  IPv4 CIDR Block (Bloco CIDR IPv4):
		- Você pode escolher um intervalo de IP dentro ou igual ao intervalo de IP da VPC. Por exemplo, se o intervalo de IP da VPC for 10.0.0.0/16, você poderá escolher um intervalo de IP entre 10.0.0.0/16 e 10.0.255.255/28 como o intervalo de IP da sub-rede.
		- Se a VPC em que as sub-redes estiverem localizadas precisar se comunicar com outras VPCs ou IDCs, certifique-se de que o intervalo de IP da sub-rede não se sobreponha ao intervalo de IP de par. Caso contrário, a interconexão por meio de uma rede privada pode falhar.
    - Availability Zone (Zona de disponibilidade): selecione uma zona de disponibilidade na qual a sub-rede está localizada. Uma VPC permite sub-redes em zonas de disponibilidade diferentes, e, por padrão, essas sub-redes podem se comunicar umas com as outras por meio de uma rede privada.
    - Advanced options (Opções avançadas): opcionalmente, é possível adicionar tags para ajudar você a melhorar o gerenciamento das permissões de recursos de subusuários e colaboradores.

### Etapa 2: adquirir uma instância da CVM
1. Faça login no [Console da CVM](https://console.cloud.tencent.com/cvm) para criar uma instância da CVM na VPC criado na etapa anterior.
2. Clique em **Create (Criar)** no canto superior esquerdo da página da lista para acessar a página de aquisição da CVM.
<img src="" width="80%">
3. Na página de configuração personalizada, configure a instância da CVM e clique em **Buy Now (Comprar agora)**. As configurações de rede da CVM são as seguintes:
 - Network (Rede): selecione a VPC e a sub-rede criados.
![](https://qcloudimg.tencent-cloud.cn/raw/7ec59dbff60a37870ef4f9cdaf2aff70.png)
 - Public network bandwidth (Largura de banda da rede pública): não marque <img src="https://main.qcloudimg.com/raw/50eef42428eb34dc35cf40995c9b7736.png" style="margin:-3px 0">.
![](https://qcloudimg.tencent-cloud.cn/raw/f59fd4da95bd18e3f8585a1541d7547b.png)
 - Security Group (Grupo de segurança): selecione **New security group (Novo grupo de segurança)** e configure-o conforme as instruções em [Configuração de grupos de segurança](https://intl.cloud.tencent.com/document/product/213/15377).
![](https://qcloudimg.tencent-cloud.cn/raw/72584971b62015e38c9ad22da7ddd3d4.png)

### Etapa 3: solicitar um EIP e vinculá-lo à instância da CVM
Um IP elástico (EIP) é um endereço IP público que pode ser solicitado e adquirido de forma independente. Você pode vinculá-lo a uma instância da CVM para habilitar o acesso à rede pública.
1. Faça login no [Console do EIP](https://console.cloud.tencent.com/cvm/eip).
2. Na página **EIP**, selecione a região onde está localizado a CVM. Clique em **Apply (Solicitar)** no canto superior esquerdo.
3. Na janela **Apply for EIP (Solicitar EIP)**, configure os parâmetros relevantes e clique em **OK**.
4. Na página **EIP**, localize o EIP solicitado e clique em **More (Mais)** > **Bind (Vincular)**, na coluna **Operation (Operação)**.
5. Na janela **Bind resources (Vincular recursos)**, selecione **CVM Instances (Instâncias da CVM)** como o tipo de recurso a ser vinculado, selecione a instância da CVM e clique em **OK**.
![]()
6. Na janela pop-up de confirmação, clique em **OK**.


### Etapa 4: testar a conectividade da rede pública
Conclua as operações a seguir para testar a conectividade da rede pública da instância da CVM.
>?Antes de realizar o teste, certifique-se de que o grupo de segurança permite o acesso ao endereço IP e à porta correspondentes. Por exemplo, o protocolo ICMP está aberto e o servidor pode receber ping da rede pública. Para mais informações, consulte [Exibição de uma regra de grupos de segurança](https://intl.cloud.tencent.com/document/product/215/35514).
>
1. Faça login na instância da CVM com um EIP vinculado. Para obter instruções detalhadas, consulte [Login e acesso remoto](https://intl.cloud.tencent.com/document/product/213/17278).
2. Execute o comando `ping <public IP address>`, como `ping www.qq.com` para testar a conectividade da rede pública.
![](https://main.qcloudimg.com/raw/e19b0921e6d0471ca0e9b78923ccdd06.png)

