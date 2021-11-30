1. **Criação de HAVIPs**
Faça login no [console do VPC](https://console.cloud.tencent.com/vpc/havip) e crie um HAVIP. Para obter instruções detalhadas, consulte [Criação de HAVIPs](https://intl.cloud.tencent.com/document/product/215/31820#.E5.88.9B.E5.BB.BA-havip).
2. **Vinculação e configuração**
A configuração é igual à do modo tradicional. O servidor de back-end declara e negocia no dispositivo que será vinculado ao HAVIP criado. Basta especificar o endereço IP virtual no arquivo de configuração como HAVIP.
No gerenciador de cluster, adicione o HAVIP que acabou de ser criado.
3. **Verificação**
Depois que a configuração for concluída, alterne diretamente os nós para teste.
Em situações normais, você verá que a rede se recupera após uma breve interrupção (nenhuma interrupção será notada se a alternação for rápida o suficiente), e os serviços online não serão afetados.

