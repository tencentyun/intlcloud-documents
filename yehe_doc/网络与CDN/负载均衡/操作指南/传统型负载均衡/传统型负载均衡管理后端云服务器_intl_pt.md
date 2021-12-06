O CLB clássico roteia as solicitações para as instâncias do servidor de back-end que estão sendo executadas normalmente. Este documento descreve como adicionar ou excluir servidores de back-end conforme necessário ou quando você usar o CLB clássico pela primeira vez.
## Pré-requisitos
Você criou uma instância do CLB clássico e configurou um listener. Para obter mais informações, consulte [Introdução ao CLB clássico](https://intl.cloud.tencent.com/document/product/214/6574).
## Instruções
### Adição do servidor de back-end à instância do CLB clássico
>?
>- Se uma instância do CLB clássico estiver associada a um grupo do Auto Scaling, as instâncias do CVM no grupo serão adicionadas automaticamente aos servidores de back-end da instância do CLB clássico. Quando uma instância do CVM for removida do grupo do Auto Scaling, ela será automaticamente excluída dos servidores de back-end da instância do CLB clássico.
>- Se você precisar usar uma API para adicionar servidores de back-end, consulte a API de [RegisterTargetsWithClassicalLB](https://intl.cloud.tencent.com/document/product/214/33802).
>
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/loadbalance).
2. Na página "Instance Management (Gerenciamento de instâncias)", selecione a guia **Classic Cloud Load Balancer (Cloud Load Balancer clássico)**.
3. Clique em **Configure Listener (Configurar listener)** na coluna "Operation (Operação)" à direita da instância do CLB clássico em questão.
4. No módulo de configuração de listener, clique em **Create (Criar)**.
5. Na janela pop-up "Create Listener (Criar listener)", insira a "backend port (porta de back-end)" (para obter mais informações sobre a escolha da porta, consulte [Portas comuns do servidor](https://intl.cloud.tencent.com/document/product/213/12451)) e os outros campos relacionados e clique em **Next (Avançar)** para concluir a configuração. Para obter mais informações, consulte [Configuração do CLB clássico](https://intl.cloud.tencent.com/document/product/214/32462).
>?Você precisa especificar a porta do servidor de back-end para o CLB clássico durante a **criação do listener**.
>
![](https://main.qcloudimg.com/raw/b2d43b48851d5c021a95872613e359c3.png)
6. Após a criação do listener, clique em **Bind (Vincular)** no módulo de vinculação do servidor de back-end.
7. Na janela pop-up **Bind CVM (Vincular CVM)**, selecione a instância do CVM a ser vinculada, insira o peso e clique em **OK**.
>?
>- A janela pop-up exibe apenas as instâncias do CVM disponíveis na mesma região e mesmo ambiente de rede que não estão isoladas e não expiraram com pico de largura de banda maior que 0.
>- Quando vários servidores de back-end estiverem vinculados, o CLB encaminhará o tráfego de acordo com o algoritmo de hash para balancear a carga.
>- Quanto maior o peso de um servidor, mais solicitações serão encaminhadas a ele. O valor padrão é 10 e o intervalo de valores configuráveis é 0 a 100. Se o peso for definido como 0, o servidor não aceitará novas solicitações. Se a persistência de sessão estiver ativada, pode causar distribuição irregular de solicitações entre servidores de back-end. Para obter mais informações, consulte [Configuração de algoritmos e pesos](https://intl.cloud.tencent.com/document/product/214/5371).
>
 ![](https://main.qcloudimg.com/raw/d9d9becb83da5d34e913591b86132aa5.png)

### Modificação do peso do servidor de back-end para a instância do CLB clássico
>?Atualmente, o peso do servidor de back-end não pode ser modificado por meio de APIs para o CLB clássico.
>
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/loadbalance).
2. Na página "Instance Management (Gerenciamento de instâncias)", selecione a guia **Classic Cloud Load Balancer (Cloud Load Balancer clássico)**.
3. Clique em **Configure Listener (Configurar listener)** na coluna "Operation (Operação)" à direita da instância do CLB clássico em questão.
4. No módulo de vinculação do servidor de back-end, modifique o peso do servidor relevante.
>?Quanto maior o peso de um servidor, mais solicitações serão encaminhadas a ele. O valor padrão é 10 e o intervalo de valores configuráveis é 0 a 100. Se o peso for definido como 0, o servidor não aceitará novas solicitações. Se a persistência de sessão estiver ativada, pode causar distribuição irregular de solicitações entre servidores de back-end. Para obter mais informações, consulte [Configuração de algoritmos e pesos](https://intl.cloud.tencent.com/document/product/214/5371).
>
	- **Método 1**. Modifique o peso de um único servidor.
		1. Localize o servidor cujo peso precisa ser modificado, passe o cursor do mouse sobre o peso correspondente e clique em <img src="https://main.qcloudimg.com/raw/4aae0dbec227f8fc18b4a35acf560f62.png" style="margin:0;">.
		![](https://main.qcloudimg.com/raw/9230ac972fdd0f1b8c55c5188c0424fd.png)
		2. Na janela pop-up "Modify Weight (Modificar peso)", insira o novo valor de peso e clique em **Submit (Enviar)**.
	- **Método 2**. Modifique o peso de vários servidores em lotes.
	>?Após a modificação em lote, os servidores terão o mesmo peso.
		>
		1. Clique na caixa de seleção ao lado dos servidores, selecione vários servidores e clique em **Modify Weight (Modificar peso)** na parte superior da lista.
		![](https://main.qcloudimg.com/raw/6e58995f13d57fe0cd9ea0c92e32d931.png)
		2. Na janela pop-up "Modify Weight (Modificar peso)", insira o novo valor de peso e clique em **Submit (Enviar)**.

### Desvinculação do servidor de back-end da instância do CLB clássico
>?
>- A desvinculação de um servidor de back-end desvinculará a instância do CLB clássico da instância do CVM, e o CLB clássico parará de encaminhar solicitações para ele imediatamente.
>- Desvincular um servidor de back-end não afetará o ciclo de vida da sua instância do CVM, que pode ser adicionada ao cluster de servidor de back-end novamente quando necessário.
>- Se você precisar usar uma API para desvincular servidores de back-end, consulte a API de [DeregisterTargetsFromClassicalLB](https://intl.cloud.tencent.com/document/product/214/33807).
>
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/loadbalance).
2. Na página "Instance Management (Gerenciamento de instâncias)", selecione a guia **Classic Cloud Load Balancer (Cloud Load Balancer clássico)**.
3. Clique em **Configure Listener (Configurar listener)** na coluna "Operation (Operação)" à direita da instância do CLB clássico em questão.
4. No módulo de vinculação do servidor de back-end, desvincule o servidor vinculado.
	- **Método 1**. Desvincule um único servidor.
		1. Localize o servidor que precisa ser desvinculado e clique em **Unbind (Desvincular)** na coluna **Operation (Operação)** à direita.
		![](https://main.qcloudimg.com/raw/f398806fd564c8b0ff9ed1610b76ce4e.png)
		2. Na janela pop-up "Unbind Real Server (Desvincular servidor de back-end)", confirme o servidor a ser desvinculado e clique em **Submit (Enviar)**.
	- **Método 2**. Desvincule vários servidores em lotes.
		1. Clique na caixa de seleção ao lado dos servidores, selecione vários servidores e clique em **Unbind (Desvincular)** na parte superior da lista.
		![](https://main.qcloudimg.com/raw/088d33fd06d677741f58b91ea05ab1a2.png)
		2. Na janela pop-up "Unbind Real Server (Desvincular servidor de back-end)", confirme os servidores a serem desvinculados e clique em **Submit (Enviar)**.


