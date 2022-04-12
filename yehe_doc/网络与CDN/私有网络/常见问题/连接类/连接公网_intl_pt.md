### Como solicito um IP público se não tiver sido atribuído na aquisição da CVM?
Se um IP público não foi atribuído quando você adquiriu a CVM, não há como solicitar novamente um IP público comum para essa CVM. No entanto, a mesma função pode ser realizada usando [EIPs](https://intl.cloud.tencent.com/document/product/213/5733). Para mais informações sobre como usá-los, consulte [Solicitação de EIPs](https://intl.cloud.tencent.com/document/product/213/16586).
- Um EIP é um tipo de IP público que é fixado em um endereço IP público específico em uma determinada região. Ao contrário de um IP público comum, ele é vinculado à sua conta. Em outras palavras, você pode vincular e desvincular um EIP a CVMs diferentes conforme necessário (apenas um pode ser vinculado por vez).
- Devido à natureza especial de um EIP, se você solicitar um EIP, mas não o vincular a uma instância, serão cobradas taxas de recursos de IP. Para mais detalhes, consulte [Faturamento de EIP](https://intl.cloud.tencent.com/document/product/213/17156).

### Como uma instância (da CVM ou banco de dados) pode acessar a rede pública sem um endereço IP público?
Uma instância sem um IP público pode solicitar um EIP (confira a pergunta anterior) ou pode acessar a rede pública por meio do NAT Gateway.
O [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015) pode fornecer funcionalidades SNAT e DNAT para instâncias da CVM em VPCs. Se você tiver várias instâncias e quiser que elas acessem a rede pública por meio do mesmo IP público, poderá usar um NAT Gateway.

### É possível alterar o IP público de uma CVM?
Sim.
- Se a instância da CVM usa o IP público atribuído no momento da aquisição, consulte [Alteração de endereços IP públicos](https://intl.cloud.tencent.com/document/product/213/16642).
- Se a instância da CVM estiver vinculada a um EIP, primeiro você precisará [desvincular o EIP](https://intl.intl.cloud.tencent.com/document/product/213/16586) e depois [solicitar outro EIP](https://intl.intl.cloud.tencent.com/document/product/213/16586) ou vincular um EIP existente.
> ! Recomendamos que você libere o EIP imediatamente após ele ser convertido de um IP público. Caso contrário, o EIP que não estiver vinculado a uma instância incorrerá em [taxas de recursos de IP](https://intl.cloud.tencent.com/document/product/213/17156). 

### É possível recuperar um IP público usado anteriormente? Posso solicitar um EIP específico?
Você pode recuperar os IPs públicos que usou anteriormente e que não estão atribuídos a outros usuários. Os IPs públicos recuperados são todos EIPs. Para mais informações, consulte [Recuperar o endereço IP da rede pública](https://intl.cloud.tencent.com/document/product/213/32719).

### Uma cota maior pode ser solicitada depois que a quantidade de EIPs atingir o limite máximo?
Devido aos recursos limitados de EIP, você pode solicitar apenas 20 por conta por região, e não pode solicitar um aumento de cota. As instâncias da CVM sem IPs públicos podem usar NAT Gateways e outros métodos para acessar a rede pública.

### Como uma CVM acessa a rede pública se possui um IP público ou EIP e sua sub-rede também está associada a um NAT Gateway?

Se uma CVM tiver um IP público ou EIP e sua sub-rede também estiver associada a um NAT Gateway (ou seja, a tabela de rotas especifica que o próximo salto do tráfego dessa sub-rede para acessar a rede pública é um NAT Gateway), então a configuração padrão é para que todo o tráfego dessa CVM acesse a rede pública por meio do NAT Gateway.

Se você precisar modificar a prioridade para que o tráfego da instância da CVM para a rede pública passe pelo IP público, consulte [Ajuste das prioridades dos NAT Gateways e EIPs](https://intl.cloud.tencent.com/document/product/1015/32734).

### Quando uma instância da CVM acessa a rede pública por meio de um gateway público ou NAT Gateway, a taxa de rede será cobrada duas vezes?

Não, a taxa de rede será cobrada apenas uma vez. Ao acessar a rede pública por meio de um gateway público ou NAT Gateway, será cobrada apenas a taxa de rede do gateway público correspondente ou a taxa de rede do NAT Gateway. 

