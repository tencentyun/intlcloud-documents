O CLB roteia as solicitações para as instâncias do servidor de back-end que estão sendo executadas normalmente. Este documento descreve como adicionar ou excluir servidores de back-end conforme necessário ou quando você usar o CLB pela primeira vez.

## Pré-requisitos
Você criou uma instância do CLB e configurou um listener. Para obter mais informações, consulte [Introdução ao CLB](https://intl.cloud.tencent.com/document/product/214/8975).
## Instruções
### Adição do servidor de back-end à instância do CLB
>?
>- Se uma instância do CLB estiver associada a um grupo do Auto Scaling, as instâncias do CVM no grupo serão adicionadas automaticamente aos servidores de back-end da instância do CLB. Quando uma instância do CVM for removida do grupo do Auto Scaling, ela será automaticamente excluída dos servidores de back-end da instância do CLB.
>- Se você precisar usar uma API para adicionar servidores de back-end, consulte a API de [RegisterInstancesWithLoadBalancer](https://intl.cloud.tencent.com/document/api/214/1265).
>
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/loadbalance).
2. Na guia "Cloud Load Balancer" da página "Instance Management (Gerenciamento de instâncias)", clique em **Configure Listener (Configurar listener)** na coluna "Operation (Operação)" à direita da instância do CLB.
4. No módulo de configuração do listener, selecione o listener a ser vinculado a um servidor de back-end.
<span id="http"></span>
 - **Listener HTTP/HTTPS**
	 1. Na área de listener HTTP/HTTPS, clique em "+" à esquerda do listener em questão.
	 ![](https://main.qcloudimg.com/raw/561cc0f6ee3c0bce9e051fb20b4ec7bd.png)
	 2. Clique em "+" à esquerda do nome de domínio expandido.
	 ![](https://main.qcloudimg.com/raw/c4bb770736b9e185a3ecaddb9591331d.png)
	 3. Selecione o caminho do URL expandido e clique em **Bind (Vincular)**.
![](https://main.qcloudimg.com/raw/05f2041acaced53d2ae8bc24a2f0662b.png)
 -**Listener TCP/UDP/TCP SSL**
Na lista à esquerda do módulo de listener TCP/UDP/TCP SSL, selecione o listener a ser vinculado a um servidor de back-end e clique em **Bind (Vincular)**.
![](https://main.qcloudimg.com/raw/7dc44fc32104e533b512ab6c0b616e21.png)
<span id="CLB"></span>
5. Vincule um servidor de back-end à instância do CLB.
	- **Método 1**. Na janela pop-up "Bind Real Server (Vincular servidor de back-end)", clique em **CVM**, selecione uma ou várias instâncias do CVM a serem associadas, insira a porta e o peso e clique em **OK**. Para obter mais informações, consulte [Portas comuns do servidor](https://intl.cloud.tencent.com/document/product/213/12451).
>?
>- A janela pop-up "Bind Real Server (Vincular servidor de back-end)" exibe apenas as instâncias do CVM disponíveis na mesma região e mesmo ambiente de rede que não estão isoladas e não expiraram com pico de largura de banda maior que 0.
>- Quando vários servidores de back-end estiverem vinculados, o CLB encaminhará o tráfego de acordo com o algoritmo de hash para balancear a carga.
>- Quanto maior o peso de um servidor, mais solicitações serão encaminhadas a ele. O valor padrão é 10 e o intervalo de valores configuráveis é 0 a 100. Se o peso for definido como 0, o servidor não aceitará novas solicitações. Se a persistência de sessão estiver ativada, pode causar distribuição irregular de solicitações entre servidores de back-end. Para obter mais informações, consulte [Configuração de algoritmos e pesos](https://intl.cloud.tencent.com/document/product/214/5371).
>
 ![](https://main.qcloudimg.com/raw/a7f71557ff1812f777c9e989b916049f.png)
	- **Método 2**. Se você precisar vincular servidores em lotes com o mesmo valor de porta predefinido, pode clicar em **CVM** na janela pop-up "Bind Real Server (Vincular servidor de back-end)", inserir o valor de porta padrão (para obter mais informações sobre a escolha de portas, consulte [Portas comuns do servidor](https://intl.cloud.tencent.com/document/product/213/12451)), verifique os servidores de destino, defina o valor do peso e clique em **OK**.
![](https://main.qcloudimg.com/raw/118bfbab842d72e990d9ffe08c6379ff.png)

### Modificação do peso do servidor de back-end para a instância do CLB
O peso do servidor de back-end determina a quantidade de solicitações do CVM a serem encaminhadas. Ao vincular um servidor de back-end, é preciso predefinir o peso dele. Veja abaixo como modificar o peso do servidor de back-end com "listeners HTTP/HTTPS" como um exemplo (que pode ser modificado para listeners TCP/UDP/TCP SSL da mesma maneira).
>?
>- Se você precisar usar uma API para modificar os pesos do servidor de back-end, consulte a API de [ModifyLoadBalancerBackends](https://intl.cloud.tencent.com/document/api/214/1264).
>- Para obter mais informações sobre o peso do servidor de back-end do CLB, consulte [Método de sondagem do CLB](/doc/product/214/6153).
>
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/loadbalance).
2. Na guia "Cloud Load Balancer" da página "Instance Management (Gerenciamento de instâncias)", clique em **Configure Listener (Configurar listener)** na coluna "Operation (Operação)" à direita da instância do CLB.
4. Na lista à esquerda do módulo de listener HTTP/HTTPS, expanda as instâncias e as regras do listener e selecione um caminho de URL.
![](https://main.qcloudimg.com/raw/06d500104032de3edda51bdc368b0c4b.png)
5. Na lista de servidores à direita do módulo de listener HTTP/HTTPS, modifique o peso do servidor relevante.
>?Quanto maior o peso de um servidor, mais solicitações serão encaminhadas a ele. O valor padrão é 10 e o intervalo de valores configuráveis é 0 a 100. Se o peso for definido como 0, o servidor não aceitará novas solicitações. Se a persistência de sessão estiver ativada, pode causar distribuição irregular de solicitações entre servidores de back-end. Para obter mais informações, consulte [Configuração de algoritmos e pesos](https://intl.cloud.tencent.com/document/product/214/5371).
>
	- **Método 1**. Modifique o peso de um único servidor.
		1. Localize o servidor cujo peso precisa ser modificado, passe o cursor do mouse sobre o peso correspondente e clique em <img src="https://main.qcloudimg.com/raw/4aae0dbec227f8fc18b4a35acf560f62.png" style="margin:0;">.
		![](https://main.qcloudimg.com/raw/519a69a1fab550879e92cdfc159a8fa1.png)
		2. Na janela pop-up "Modify Weight (Modificar peso)", insira o novo valor de peso e clique em **Submit (Enviar)**.
	- **Método 2**. Modifique o peso de vários servidores em lotes.
	>?Após a modificação em lote, os servidores terão o mesmo peso.
		>
		1. Clique na caixa de seleção ao lado dos servidores, selecione vários servidores e clique em **Modify Weight (Modificar peso)** na parte superior da lista.
		![](https://main.qcloudimg.com/raw/09fdd5cb7a49f80bdc088632d7249f1e.png)
		2. Na janela pop-up "Modify Weight (Modificar peso)", insira o novo valor de peso e clique em **Submit (Enviar)**.



### Modificação da porta do servidor de back-end para a instância do CLB
Você pode modificar a porta do servidor de back-end no console do CLB. Veja abaixo como modificar o peso do servidor de back-end com "listeners HTTP/HTTPS" como um exemplo (que pode ser modificado para listeners TCP/UDP/TCP SSL da mesma maneira).
>?Se você precisar usar uma API para modificar as portas do servidor de back-end, consulte a API de [ModifyTargetPort](https://intl.cloud.tencent.com/document/product/214/33812).
>
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/loadbalance).
2. Na guia "Cloud Load Balancer" da página "Instance Management (Gerenciamento de instâncias)", clique em **Configure Listener (Configurar listener)** na coluna "Operation (Operação)" à direita da instância do CLB.
4. Na lista à esquerda do módulo de listener HTTP/HTTPS, expanda as instâncias e as regras do listener e selecione um caminho de URL.
![](https://main.qcloudimg.com/raw/06d500104032de3edda51bdc368b0c4b.png)
5. Na lista de servidores à direita do módulo de listener HTTP/HTTPS, modifique a porta do servidor relevante. Para obter mais informações sobre a escolha das portas, consulte [Portas comuns do servidor](https://intl.cloud.tencent.com/document/product/213/12451).
	- **Método 1**. Modifique a porta de um único servidor.
		1. Localize o servidor cuja porta precisa ser modificada, passe o cursor do mouse sobre a porta correspondente e clique em <img src="https://main.qcloudimg.com/raw/4aae0dbec227f8fc18b4a35acf560f62.png" style="margin:0;">.
		![](https://main.qcloudimg.com/raw/923c439bedc4af2e6129d8ada459a1c5.png)
		2. Na janela pop-up "Modify Port (Modificar porta)", insira o novo valor de porta e clique em **Submit (Enviar)**.
	- **Método 2**. Modifique a porta de vários servidores em lotes.
	>?Após a modificação em lote, os servidores terão a mesma porta.
		>
		1. Clique na caixa de seleção ao lado dos servidores, selecione vários servidores e clique em **Modify Port (Modificar porta)** na parte superior da lista.
		![](https://main.qcloudimg.com/raw/07d40e5fcf1111a9141be83e41f67797.png)
		2. Na janela pop-up "Modify Port (Modificar porta)", insira o novo valor de porta e clique em **Submit (Enviar)**.



### Desvinculação do servidor de back-end da instância do CLB
Você pode desvincular servidores de back-end vinculados no console do CLB. Veja abaixo como desvincular servidores de back-end vinculados a "listeners HTTP/HTTPS" como um exemplo (que pode ser desvinculado de listeners TCP/UDP/TCP SSL da mesma maneira).
>?
>- A desvinculação de um servidor de back-end desvinculará a instância do CLB da instância do CVM, e o CLB parará de encaminhar solicitações para ele imediatamente.
>- Desvincular um servidor de back-end não afetará o ciclo de vida da sua instância do CVM, que pode ser adicionada ao cluster de servidor de back-end novamente quando necessário.
>- Se você precisar usar uma API para desvincular servidores de back-end, consulte a API de [DeregisterTargets](https://intl.cloud.tencent.com/document/product/214/33832).
>
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/loadbalance).
2. Na guia "Cloud Load Balancer" da página "Instance Management (Gerenciamento de instâncias)", clique em **Configure Listener (Configurar listener)** na coluna "Operation (Operação)" à direita da instância do CLB.
4. Na lista à esquerda do módulo de listener HTTP/HTTPS, expanda as instâncias e as regras do listener e selecione um caminho de URL.
![](https://main.qcloudimg.com/raw/06d500104032de3edda51bdc368b0c4b.png)
5. Na lista de servidores à direita do módulo de listener HTTP/HTTPS, desvincule o servidor de back-end vinculado.
	- **Método 1**. Desvincule um único servidor.
		1. Localize o servidor que precisa ser desvinculado e clique em **Unbind (Desvincular)** na coluna **Operation (Operação)** à direita.
		![](https://main.qcloudimg.com/raw/c995daabbf0b6a710b21389b17b7760b.png)
		2. Na janela pop-up "Unbind (Desvincular)", confirme o servidor a ser desvinculado e clique em **Submit (Enviar)**.
	- **Método 2**. Desvincule vários servidores em lotes.
		1. Clique na caixa de seleção ao lado dos servidores, selecione vários servidores e clique em **Unbind (Desvincular)** na parte superior da lista.
		![](https://main.qcloudimg.com/raw/b397ef434ce42cfaa9a48b9f4f08f09f.png)
		2. Na janela pop-up "Unbind (Desvincular)", confirme os servidores a serem desvinculados e clique em **Submit (Enviar)**.

