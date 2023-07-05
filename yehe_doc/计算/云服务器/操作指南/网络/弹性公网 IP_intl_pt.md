## Cenário
O IP elástico, ou EIP, é um IP estático projetado para computação em nuvem dinâmica e um IP público fixo em uma determinada região. Com o EIP, é possível remapear com rapidez um endereço para outra instância da sua conta ou instância do NAT Gateway para evitar a falha da instância. Este documento descreve como usar os EIPs.

## Pré-requisitos

Você fez login no [Console do CVM](https://console.cloud.tencent.com/cvm).

## Instruções

### Solicitar EIPs 

1. Na barra lateral esquerda, clique em **[EIP](https://console.cloud.tencent.com/cvm/eip)** para entrar na página de gerenciamento de EIPs.
2. Clique em **Apply (Solicitar)** na página de gerenciamento de EIPs.
3. Na janela pop-up “Apply for EIP (Solicitar EIP)”, selecione a região, tipo de endereço IP, método de faturamento e limite de largura de banda e insira a quantidade de EIPs que deseja solicitar.
4. Clique em **OK** para concluir a solicitação de EIPs.
Depois que a solicitação for concluída, é possível visualizar na lista o EIP que você solicitou, que está com o status não vinculado.

<span id = "jump2">  </span>
### Vinculação de EIPs a produtos em nuvem

1. Na barra lateral esquerda, clique em **[EIP](https://console.cloud.tencent.com/cvm/eip)** para entrar na página de gerenciamento de EIPs.
2. Na página de gerenciamento de EIPs, selecione o EIP que deseja vincular a um produto em nuvem e clique em **More (Mais)** > **Bind (Vincular)**.
> Se o EIP foi vinculado a uma instância, desvincule-o primeiro.
>
3. Na janela pop-up “Bind resources (Vincular recursos)”, selecione o recurso a ser vinculado ao EIP e clique em **OK**.
4. Na janela pop-up, clique em **OK** para concluir a vinculação do EIP ao produto em nuvem.


### Desvinculação de EIPs de produtos em nuvem

1. Na barra lateral esquerda, clique em **[EIP](https://console.cloud.tencent.com/cvm/eip)** para entrar na página de gerenciamento de EIPs.
2. Na página de gerenciamento de EIPs, selecione o EIP que deseja desvincular de um produto em nuvem e clique em **More (Mais)** > **Unbind (Desvincular)**.
3. Na janela pop-up “Unbind EIP (Desvincular EIP)”, confirme as informações de desvinculação e clique em **OK**.
4. Na janela pop-up, clique em **OK** para concluir a desvinculação do EIP do produto em nuvem.
> Após a desvinculação, a instância do produto em nuvem pode receber um novo IP público, que pode ser diferente do anterior à vinculação.
>

<span id = "jump">  </span>
### Liberação de EIPs

1. Na barra lateral esquerda, clique em **[EIP](https://console.cloud.tencent.com/cvm/eip)** para entrar na página de gerenciamento de EIPs.
2. Na página de gerenciamento de EIPs, selecione o EIP que deseja liberar de um produto em nuvem e clique em **More (Mais)** > **Release (Liberar)**.
3. Na janela pop-up “Are you sure you want to release the selected EIPs? (Tem certeza de que deseja liberar os EIPs selecionados?)”, selecione **Release the above EIPs (Liberar os EIPs acima)** e clique em **Release (Liberar)**.

### Ajuste da largura de banda
1. Na barra lateral esquerda, clique em **[EIP](https://console.cloud.tencent.com/cvm/eip)** para entrar na página de gerenciamento de EIPs.
2. Selecione o EIP cuja largura de banda precisa ser ajustada e clique em **Adjust Bandwidth (Ajustar largura de banda)**
3. Na janela pop-up “Adjust Bandwidth (Ajustar largura de banda)”, configure o valor da largura de banda e clique em **OK** para concluir o ajuste.

### Conversão de um IP público em um EIP
O IP público adquirido junto com a instância do CVM não é elástico e não pode ser montado ou desmontado. O Tencent Cloud permite que você converta o IP público em um EIP por meio das seguintes etapas:
1. Na barra lateral esquerda, clique em **[Instances (Instâncias)](https://console.cloud.tencent.com/cvm/index)** para entrar na página de gerenciamento de instâncias.
2. Selecione a instância cujo IP público precisa ser convertido em um EIP e clique em <img src="https://main.qcloudimg.com/raw/25e8c0e37b73c12da900301f03e57dbc.png" style="margin: 0;"></img>, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/53b608b2bb0840920703e7f50957611a.jpg)
3. Na janela pop-up “Convert to EIP (Converter para EIP)”, clique em **OK**.
![](https://main.qcloudimg.com/raw/3d20c058c66975f847e68e42ae944d6f.png)

## Solução de problemas de exceções
A inacessibilidade da rede pode ocorrer com um EIP devido aos seguintes motivos: 
- O EIP não está vinculado a nenhum produto em nuvem. Para obter mais informações sobre como vincular um EIP ao produto em nuvem, consulte [Vincular EIPs a produtos em nuvem](#jump2).
- A política de segurança é inválida. Verifique se há uma política de segurança válida (grupo de segurança ou ACL de rede). Se o produto em nuvem vinculado tiver uma política de grupo de segurança, como o acesso à porta 8080 negado, a porta 8080 do EIP também ficará inacessível.
