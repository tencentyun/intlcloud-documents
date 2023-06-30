### Não há conexão de rede após o login na CVM. Como resolvo esse problema?
Se não houver acesso à rede (por exemplo, a página da Web está inacessível) após o login na CVM, é necessário verificar a configuração do DNS. Configure a CVM para obter o endereço DNS automaticamente seguindo as instruções abaixo.
> As operações a seguir usam um Windows Server 2012 como exemplo.
> 
1. Faça login na CVM do Windows.
2. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;width: 22px;"> e selecione **Control panel (Painel de Controle)** -> **Network and Internet (Rede e Internet)** -> **View network status and tasks (Exibir o status e as tarefas da rede)** -> **Change adapter settings (Alterar as configurações do adaptador)**.
3. Clique com o botão direito em **Ethernet** e selecione **Properties (Propriedades)** para abrir a janela “Ethernet Properties (Propriedades de Ethernet)”.
4. Nessa janela, clique duas vezes e abra a janela **Internet Protocol Version 4 (TCP/IPv4) Properties (Propriedades do protocolo de Internet versão 4 (TCP/IPv4))**.
5. Nessa janela, selecione **Obtain an IP address automatically (Obter um endereço IP automaticamente)** e **Obtain DNS server address automatically (Obter o endereço dos servidores DNS automaticamente)** e clique em **OK**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/8a597efe05adc2f96d4b40b6cd633ca4.png)

### Uma instância do VPC pode se interconectar com a instância de rede clássica?

#### Sim, mas tem a seguinte restrição:
O intervalo de endereços IP do VPC (CIDR) deve ser 10.0.0.0/16 - 10.0.47.0/16 (incluindo os subconjuntos). Caso contrário, haverá conflitos.

#### Instruções
Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc/vpc?rid=1), clique no ID/nome do VPC para acessar sua página de detalhes, e clique na guia **Classiclink** para associar a CVM de rede clássica a ser interconectado. 

### Como exibo as CVMs da rede clássica que estão interconectados com as CVMs do VPC?
Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc/vpc?rid=1), clique no ID/nome do VPC para acessar sua página de detalhes, e exiba as CVMs da rede clássica interconectados com as CVMs do VPC no **Classiclink**.

### É possível migrar a CVM para uma rede no exterior?
Após a aquisição, a rede da CVM não pode ser alterada. Se precisar de uma rede no exterior, recomendamos que devolva a CVM e adquira um no exterior.

### Como configuro um DNS da rede privada?
Consulte [Acesso à rede privada](https://intl.cloud.tencent.com/document/product/213/5225).

### Dentro do mesmo intervalo de IP, o VPN consegue obter o endereço IP de um intervalo de IP, mas não consegue acessar a Internet. Como resolvo esse problema?

Verifique se estas configurações estão corretas:
1. O IP adicionado manualmente e o IP obtido automaticamente estão na mesma sub-rede de IP? As máscaras de sub-rede são as mesmas? O gateway padrão está configurado? O endereço de gateway padrão está correto?
2. O DNS está configurado e o endereço DNS está correto?
3. Se todas as configurações acima estiverem corretas, verifique se o endereço IP configurado estaticamente tem um conflito de IP.
  
Se nenhuma das opções acima funcionar, [envie um tíquete](https://console.cloud.tencent.com/workorder/category) para entrar em contato conosco.

### Como adiciono CVMs nas contas A e B à mesma sub-rede?

Por padrão, as contas não são interconectadas pela rede. Para interconectar contas, consulte [Criação de um Peering Connection entre contas](https://intl.cloud.tencent.com/document/product/553/35190) ou [Interconexão de instância de rede entre contas](https://intl.cloud.tencent.com/document/product/1003/31987).
