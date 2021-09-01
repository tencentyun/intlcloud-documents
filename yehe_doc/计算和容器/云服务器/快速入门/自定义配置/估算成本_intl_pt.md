Além do modelo do CVM e da configuração do VPC, esses fatores também influenciam os custos de serviço:
- Método de faturamento
- Recurso usado
- Quantidade

### Método de faturamento
- O **pagamento conforme o uso** é um método de faturamento flexível para as instâncias do CVM. É possível iniciar/encerrar um CVM a qualquer momento e você será faturado pelo uso real do CVM. Você paga por segundo e não é necessário pagamento adiantado. Uma fatura é gerada a cada hora cheia. Esse método de faturamento é adequado para casos de uso, como uma oferta relâmpago de comércio eletrônico, em que a demanda por recursos pode flutuar muito.
- A **instância spot** é uma nova forma de usar e pagar por instâncias do CVM. Semelhante ao pagamento conforme o uso, você paga pelas instâncias spot por segundo, a cada hora. O preço das instâncias spot flutua de acordo com a demanda do mercado. Você obtém um desconto considerável para elas quando a demanda é baixa (geralmente de 10 a 20%). No entanto, elas podem ser reavidas automaticamente pelo sistema à medida que a demanda aumenta.

### Recursos usados
- Região:
	- O preço é igual para o mesmo modelo de instância em diferentes regiões da China Continental.
	- O preço pode ser igual para o mesmo modelo de instância em diferentes regiões fora da China Continental.
- Imagem:
	- Imagens públicas: todas as imagens públicas na China Continental hospedadas pelo Tencent Cloud são gratuitas. As imagens do Windows fora da China continental requerem taxas de licenciamento.
	- Imagem personalizada: a criação, a importação e a cópia de imagens personalizadas entre regiões são gratuitas.
	- Imagens compartilhadas: as imagens compartilhadas de outros usuários do Tencent Cloud são gratuitas.
Rede:
	- O VPC, a sub-rede, a tabela de rotas, a ACL de rede, o grupo de segurança, o gateway do Direct Connect, o túnel VPN e o gateway do cliente são gratuitos.
	- Os custos de largura de banda não são aplicáveis à comunicação entre instâncias em sub-redes diferentes. As conexões de emparelhamento intrarregional também são gratuitas.
	- Consulte [este artigo](https://intl.cloud.tencent.com/document/product/213/10578) para mais detalhes sobre o método de faturamento da rede pública.
	- Para mais detalhes sobre as cobranças do NAT Gateway, do VPN Gateway e das conexões de emparelhamento intrarregional.
- Armazenamento:
	Para ter acesso aos preços de discos locais e discos em nuvem, consulte [este artigo](https://intl.cloud.tencent.com/document/product/362/2413)


### Quantidade

A quantidade de CVMs adquiridos também afeta o preço que você paga. Quanto mais CVMs, maior o preço.
