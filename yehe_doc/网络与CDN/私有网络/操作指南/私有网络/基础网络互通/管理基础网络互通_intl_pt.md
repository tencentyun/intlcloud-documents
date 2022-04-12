## Criação de um Classiclink
Um Classiclink associa CVMs baseadas na rede clássica a uma VPC para permitir a interconexão entre a VPC e a rede clássica. Isso permite que as CVMs baseadas na rede clássica se comuniquem com os recursos da VPC.
>?
>- Os IPs privados das CVMs baseadas na rede clássica associados serão adicionados automaticamente à política local da tabela de rotas da VPC. Isso permite a interconexão, sem a necessidade de modificar manualmente a política de roteamento da VPC.
>- Depois que a CVM baseada na rede clássica for associada a uma VPC, suas configurações de firewall e ACL de rede permanecerão efetivas.


### Instruções
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Selecione a região, e clique no ID da VPC que precisa do Classiclink, para acessar a página de detalhes.
3. Clique na guia **Classiclink** e em **+Associate with CVM (+Associar à CVM)**. 
![](https://main.qcloudimg.com/raw/ad9b76faac017dbc093b3710f0d5070b.png)
4. Na janela pop-up, selecione a CVM na rede clássica a ser associada à VPC e clique em **OK**.
![](https://main.qcloudimg.com/raw/b99329129fc8de27dddfbe7897d59218.png)

## Exibição do Classiclink
É possível exibir a lista de CVMs baseadas na rede clássica que se interconectam com a VPC.
### Instruções
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Selecione a região, e clique no ID da VPC que precisa do Classiclink, para acessar a página de detalhes.
3. Clique na guia **Classiclink** para exibir a lista de CVMs baseadas na rede clássica associadas à VPC.
![](https://main.qcloudimg.com/raw/3b4e1ad2a860c35f89b42315e709d11f.png)
4. Digite um IP privado na caixa de pesquisa do canto superior direito para localizar a CVM de forma rápida.

## Exclusão de um Classiclink[](id:release)
Essa ação desassocia as CVMs baseadas na rede clássica da VPC e encerra sua interconexão.

### Instruções
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Clique no ID da VPC que precisa do Classiclink, para acessar a página de detalhes.
3. Clique na guia **Classiclink**, selecione a CVM a ser desassociada da lista de CVMs baseadas na rede clássica, e clique em **Disassociate (Desassociar)** na coluna **Operation (Operação)**.
![](https://main.qcloudimg.com/raw/156dd9a80b6923a96bb52e2d76b55993.png)
4. Verifique as observações e clique em **OK**.
5. Para desassociar várias CVMs, selecione as CVMs a serem desassociadas e clique em **Disassociate (Desassociar)** acima da lista.
