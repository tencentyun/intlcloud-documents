Cada VPC pode ter um bloco CIDR principal, que não pode ser modificado após a criação da VPC. Quando os IPs no bloco CIDR principal não atendem às suas necessidades, é possível criar vários blocos CIDR secundários para adicionar intervalos de IP.
Você pode alocar a sub-rede com um intervalo de IP dos blocos CIDR principal ou secundário. Todas as sub-redes da mesma VPC são interconectadas por padrão, independentemente de pertencerem aos blocos CIDR principal ou secundário.

## Limites de uso
+ As CVMs baseadas na rede clássica não podem se interconectar com os recursos de nuvem no bloco CIDR secundário.
+ Um Peering Connection não aceita blocos CIDR secundários.
+ O Cloud Connect Network, o gateway do VPN e o gateway do Direct Connect padrão aceitam os blocos CIDR secundários. Atenção aos seguintes limites para um gateway do Direct Connect:
  - Essa funcionalidade está indisponível nas regiões de nuvem financeira.
  - Até 10 blocos CIDR secundários podem ser propagados.
  - Essa funcionalidade está indisponível para um NAT Gateway e gateway do Direct Connect.



## Criação de blocos CIDR secundários[](id:21)
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Selecione a região da VPC na parte superior da página **VPC**.
3. Na lista de VPCs, localize a VPC e selecione **More (Mais)** > **Edit IPv4 CIDR block (Editar bloco CIDR IPv4)** na coluna **Operation (Operação)**.
4. Na caixa de diálogo pop-up, clique em **Add (Adicionar)** para inserir um bloco CIDR secundário.
>!Um bloco CIDR secundário pode se sobrepor ao intervalo de IP de destino de uma rota personalizada. Observe que o bloco CIDR secundário usa uma rota local, que tem uma prioridade mais alta do que as rotas de sub-rede personalizadas.
>
5. Clique em **OK**.

## Exclusão de blocos CIDR secundários[](id:32)
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Selecione a região da VPC na parte superior da página **VPC**.
3. Na lista de VPCs, localize a VPC do qual os blocos CIDR secundários serão excluídos e selecione **More (Mais)** > **Edit IPv4 CIDR block (Editar o bloco CIDR IPv4)** na coluna **Operation (Operação)**.
4. Na caixa de diálogo pop-up, clique em **Delete (Excluir)** ao lado do bloco CIDR secundário.

5. Clique em **OK**.
