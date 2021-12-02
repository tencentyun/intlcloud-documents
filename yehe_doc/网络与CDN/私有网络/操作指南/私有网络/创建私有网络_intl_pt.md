Os Virtual Private Clouds (VPCs) são a base para o uso dos serviços do Tencent Cloud. Ao adquirir uma instância como CVM, CLB ou TencentDB em uma região que não tem VPCs existentes, um VPC e uma sub-rede padrão serão criados automaticamente. 
![](https://main.qcloudimg.com/raw/98878feb887075f6535eca50a76d3d0c.png)
O VPC e a sub-rede padrão são criados junto com a sua instância, e não são contabilizados em sua cota na região. Eles funcionam da mesma forma que os criados manualmente. Só pode haver um VPC e uma sub-rede padrão em cada região. É possível excluir o VPC e a sub-rede padrão se não precisar mais deles.
![](https://main.qcloudimg.com/raw/a67ac7a3ac09b41905e11925f11bfa51.png)
![](https://main.qcloudimg.com/raw/907d836a6fe2e41ec2dc6a9b2796ad3a.png)
Você pode consultar este documento para criar uma instância do VPC no console se a instância padrão ou existente não for adequada.

## Instruções
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione uma região na parte superior da página **VPC**, e clique em **+ Novo (+New)**.
3. Insira as informações do VPC e da sub-rede no pop-up **Create VPC (Criar VPC)**.
>?Os blocos CIDR do VPC e da sub-rede não podem ser modificados após a criação.
>
 - O bloco CIDR do VPC pode ser qualquer um dos seguintes intervalos de IP. Para que os VPCs se comuniquem entre si por meio de uma rede privada, seus blocos CIDR não devem se sobrepor.
    - `10.0.0.0` - `10.255.255.255` (intervalo de máscara entre 16 e 28)
    - `172.16.0.0` - `172.31.255.255` (intervalo de máscara entre 16 e 28)
    - `192.168.0.0` - `192.168.255.255` (intervalo de máscara entre 16 e 28)
 - O bloco CIDR da sub-rede deve estar dentro ou ser igual ao bloco CIDR do VPC.
   Por exemplo, se o intervalo de IP do VPC for `10.0.0.0/16`, então seu intervalo de IP da sub-rede pode ser `10.0.0.0/16`, `10.0.0.0/24`, etc.
 - Availability zone (Zona de disponibilidade): uma sub-rede é específica da zona de disponibilidade. Selecione uma zona de disponibilidade na qual a sub-rede está localizada. Um VPC permite sub-redes em diferentes zonas de disponibilidade e essas sub-redes podem se comunicar umas com as outras por meio de uma rede privada por padrão.
 - Associated route table (Tabela de rotas associada): a sub-rede deve ser associada a uma tabela de rotas para encaminhamento de tráfego. Uma tabela de rotas padrão será associada para garantir a interconexão da rede privada no VPC.
 - Advanced options (Opções avançadas): é possível adicionar tags para melhorar o gerencimento das permissões de recursos de subusuários e colaboradores.
4. Ao concluir a configuração, clique em **OK**. Um VPC criado será exibido na lista, conforme mostrado abaixo. Um novo VPC tem uma sub-rede e uma tabela de rotas padrão.
![](https://main.qcloudimg.com/raw/269317b3b2b8220fde33fd01e77be65e.png)

## Operação posterior
Depois que o VPC e a sub-rede forem criados, é possível implantar recursos, incluindo o CVM e o CLB no VPC.
Clique no ícone conforme mostrado abaixo para adquirir diretamente um CVM na página de aquisição do CVM. Para obter mais informações, consulte [Criação de um VPC IPv4](https://intl.cloud.tencent.com/document/product/215/31891).
![](https://main.qcloudimg.com/raw/8374f8704f9ac1731ba84eb9d3570254.png)
