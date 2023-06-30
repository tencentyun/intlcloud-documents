## IP público

### Como uma CVM sem IP público pode acessar a rede pública?
Se você não comprou o IP público ao adquirir a CVM ou devolveu o IP público, é possível solicitar um EIP no [Console do EIP](https://console.cloud.tencent.com/cvm/eip) e vinculá-lo à CVM para permitir o acesso à rede pública.

### É possível alterar o IP público?

Você pode alterar o IP público da CVM. Para mais informações sobre as operações específicas, consulte [Alteração de endereços IP públicos](https://intl.cloud.tencent.com/document/product/213/16642).

### Como mantenho um IP público inalterado?

Se você precisar reter um IP público específico em sua conta, poderá convertê-lo em um EIP, que pode ser vinculado ao dispositivo e usado para acessar a rede pública. Esse EIP será retido na sua conta até que você o **libere**.
Para mais informações sobre as operações relacionadas, consulte [EIP](https://intl.cloud.tencent.com/document/product/213/16586).

### O que é um endereço IP público?
Um endereço IP público é um endereço IP não reservado na Internet. Uma CVM com um endereço IP público pode ser acessado por outros computadores na Internet.
Para mais informações, consulte [Acesso à Internet](https://intl.cloud.tencent.com/document/product/213/5224).

### Como obtenho o endereço IP público de uma instância?
Para mais detalhes, consulte [Obtenção de endereços IP públicos](https://intl.cloud.tencent.com/document/product/213/17940).

### Como altero o endereço IP público de uma instância?
Para mais detalhes, consulte [Alteração de endereços IP públicos](https://intl.cloud.tencent.com/document/product/213/16642).

### Quais são as diferenças entre gateways públicos e CVMs com endereços IP públicos?
Os gateways públicos habilitam a funcionalidade de encaminhamento de tráfego da rede pública na imagem. No entanto, as CVMs com endereços IP públicos não possuem essa funcionalidade por padrão. Portanto, as CVMs criados na imagem pública do Windows não podem funcionar como gateways públicos porque a imagem do Windows não tem funcionalidade de encaminhamento de tráfego.

### Por que não consigo alterar o IP público da CVM?
Os motivos possíveis incluem:
- A instância da CVM foi desligada e não incorre em cobranças ao ser desligada.
- O IP público da CVM foi alterado.


### Como obter o endereço IP público de uma instância que não teve um IP público (IPv4) atribuído durante a sua criação?
- Você pode obter o IP público de uma instância solicitando e vinculando um EIP a ela. Para acessar os procedimentos detalhados, consulte [EIP](https://intl.cloud.tencent.com/document/product/213/16586).

## IP privado

### O que é um endereço IP privado?
Não é possível acessar um endereço IP privado por meio da internet. É assim que a Tencent Cloud fornece serviços de rede privada.
Para mais informações, consulte [Acesso à rede privada](https://intl.cloud.tencent.com/document/product/213/5225).

### Como obter o endereço IP privado de uma instância?
Para mais detalhes, consulte [Obtenção de endereços IP privados e configuração do DNS](https://intl.cloud.tencent.com/document/product/213/17941).

### Posso alterar o endereço IP privado de uma instância além do endereço IP público?
Sim, você pode alterar o IP privado de uma instância. Para acessar os procedimentos, consulte [Modificação de endereços IP privados](https://intl.cloud.tencent.com/document/product/213/16561)

