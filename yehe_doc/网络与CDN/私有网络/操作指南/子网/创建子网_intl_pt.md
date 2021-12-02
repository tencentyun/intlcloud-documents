Uma sub-rede é um espaço de rede em um VPC, que carrega todas as implantações de recursos em nuvem. Um VPC possui pelo menos uma sub-rede. Uma sub-rede será criada junto com o VPC. Também é possível criar mais sub-redes em um VPC de acordo com suas necessidades empresariais.
Uma sub-rede é específica de uma zona de disponibilidade. Um VPC permite sub-redes em diferentes zonas de disponibilidade, e, por padrão, essas sub-redes podem se comunicar umas com as outras por meio de uma rede privada. Este documento lhe orientará sobre como criar uma sub-rede em um VPC.

## Instruções
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Subnet (Sub-rede)** na barra lateral esquerda para acessar a página de gerenciamento.
3. Selecione a região e o VPC em que a sub-rede será criada e clique em **+New (+Novo)**[](id:step3).
4. Configure os parâmetros da sub-rede na caixa de diálogo pop-up.
    ![](https://main.qcloudimg.com/raw/fefbd7d65e21194d342728770f964a6b.png)
   + Network (Rede): o VPC onde a sub-rede está localizada. O VPC selecionado na [Etapa 3](#step3) será exibido automaticamente. Como alternativa, você pode selecionar um VPC na lista suspensa.
   + Subnet Name (Nome da sub-rede): insira um nome de sub-rede personalizado com 60 caracteres.
   + VPC IP Range (Intervalo de IP do VPC): o bloco CIDR do VPC selecionado será exibido automaticamente.
   + CIDR: defina o bloco CIDR da sub-rede, que deve fazer parte do bloco CIDR do VPC e não pode se sobrepor ao bloco CIDR de outras sub-redes existentes no VPC.
>? Planeje intervalos de IP de sub-rede adequados à escala da sua empresa. Um endereço IP privado dentro da sub-rede especificada será atribuído automaticamente à instância do CVM que você está criando. O IP privado principal de um CVM pode ser modificado.
   + Availability Zone (Zona de disponibilidade): selecione uma zona de disponibilidade na qual a sub-rede está localizada.
   + Associated route table (Tabela de rotas associada): selecione uma tabela de rotas a ser associada. A sub-rede deve ser associada a uma tabela de rotas para controlar o tráfego de saída. Por padrão, a tabela de rotas padrão do VPC será associada para garantir a interconexão da rede privada no VPC. Você também pode selecionar outra tabela de rotas no VPC.
   + Add a line (Adicionar uma linha): clique em **Add a line (Adicionar uma linha)** para criar várias sub-redes de uma vez. Clique em ![](https://main.qcloudimg.com/raw/ae1ede733a45968e89f58c56aee3099f.png) para excluir as configurações de sub-rede selecionadas.
   + Advanced Options (Opções avançadas): você pode opcionalmente definir tags para a sub-rede para gerenciar melhor os recursos da sub-rede. Clique em **Add (Adicionar)** para definir várias tags de uma vez. Você pode clicar no ícone na coluna **Operation (Operação)** para excluir as configurações de tag selecionadas.
5. Ao concluir a configuração, clique em **Create (Criar)**. Em seguida, as sub-redes criadas serão exibidas na lista, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/fe8df992288fce35a67b0bac6861c58b.png)

## Operação posterior
Após criar uma sub-rede, você pode implantar recursos, incluindo o CVM e o CLB nela.
Clique no ícone conforme mostrado abaixo para adquirir diretamente um CVM na página de aquisição do CVM. Para obter mais informações, consulte [Criação de um VPC IPv4](https://intl.cloud.tencent.com/document/product/215/31891).
![](https://main.qcloudimg.com/raw/8fae00dfa94664159b9e98e283a2316f.png)
