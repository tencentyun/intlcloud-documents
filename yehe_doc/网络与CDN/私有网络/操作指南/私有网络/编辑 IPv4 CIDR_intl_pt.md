Após criado, o bloco CIDR principal do seu VPC não pode ser modificado. Quando o bloco CIDR principal for insuficiente, é possível criar blocos CIDR secundários para adicionar intervalos de IP.

>?
>- Atualmente, a funcionalidade de bloqueio do CIDR secundário está em beta. Para testá-la, [envie um tíquete](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1).
>- Um bloco CIDR secundário pode se sobrepor ao intervalo de IP de destino de uma rota personalizada. Observe que o bloco CIDR secundário usa uma rota local, que tem uma prioridade mais alta do que as rotas de sub-rede personalizadas.
>- Os CVMs baseados na rede clássica não podem se interconectar com os recursos de nuvem no bloco CIDR secundário.
>- Atualmente, apenas o Cloud Connect Network (CCN) é compatível com os blocos CIDR secundários. Ou seja, os CVMs nos blocos CIDR secundários não podem se comunicar com outros VPCs ou IDCs por meio do Peering Connection ou do Direct Connect.

<span id="21"></span>
## Criação de blocos CIDR secundários
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione a região do VPC na parte superior da página **VPC**.
3. Na lista de VPCs, localize o VPC e selecione **More (Mais)** > **Edit IPv4 CIDR block (Editar bloco CIDR IPv4)** na coluna **Operation (Operação)**.

4. Na caixa de diálogo pop-up, clique em **Add (Adicionar)** para inserir um bloco CIDR secundário.

5. Clique em **OK**.

<span id="32"></span>
## Exclusão de blocos CIDR secundários
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione a região do VPC na parte superior da página **VPC**.
3. Na lista de VPCs, localize o VPC em questão e selecione **More (Mais)** > **Edit IPv4 CIDR block (Editar bloco CIDR IPv4)** na coluna **Operation (Operação)**.
4. Na caixa de diálogo pop-up, clique em **Delete (Excluir)** ao lado do bloco CIDR secundário.

5. Clique em **OK**.
