Para hospedar serviços destinados ao público na sua instância do CVM, que envolve a transmissão de dados pela internet, você precisa de um endereço IP público. O Tencent Cloud fornece acesso à internet por meio de redes conectadas de alta velocidade do IDC do Tencent Cloud. A rede doméstica multilinhas BGP abrange mais de 20 operadoras de rede, e a saída de rede pública consegue processar a mudança de região em questão de segundos. Isso garante que seus usuários possam desfrutar de uma rede segura e de alta velocidade, independentemente das redes que usarem.

## Endereço IP público
 - **Visão geral**: os endereços IP públicos são endereços não reservados na internet. Um CVM com endereço IP público pode acessar outros computadores na internet e ser acessado por outros computadores.
 - **Obtenção de um endereço IP público**: defina sua largura de banda para mais de 0 Mbps ao criar sua instância do CVM. O sistema seleciona automaticamente um endereço IP público do pool de endereços IP públicos e o atribui à sua instância. Esse endereço pode ser alterado mais tarde. Para obter mais detalhes, consulte [Alterar o endereço IP público da instância](https://intl.cloud.tencent.com/document/product/213/16642).
 - **Configuração da sua instância do CVM**: você pode fazer login na sua instância do CVM a partir de uma rede pública para configurá-la. Para obter mais informações, consulte [Login em instâncias do Linux](https://intl.cloud.tencent.com/document/product/213/5436) e [Login em instâncias do Windows](https://intl.cloud.tencent.com/document/product/213/5435). 
 - **Conversão do seu endereço IP público**: você pode mapear seu endereço IP público para [o endereço IP privado](https://intl.cloud.tencent.com/document/product/213/5225) da instância do CVM usando a conversão de endereços de rede (NAT, na sigla em inglês). 
 - **Recuperação de informações de endereço IP público**: todas as interfaces de rede pública do Tencent Cloud são gerenciadas pelo Tencent Gateway (TGW), o que significa que todas essas interfaces de todas as instâncias do CVM são mantidas pelo TGW. Esse processo é imperceptível às instâncias do CVM. Portanto, ao executar o comando `ifconfig` na instância do CVM do Linux ou `ipconfig` na instância do CVM do Windows, você obtém as informações de [endereço IP privado](https://intl.cloud.tencent.com/document/product/213/5225). Para obter mais informações a respeito dos endereços IP públicos, faça login no seu [console do CVM](https://console.cloud.tencent.com/cvm) e verifique as páginas de detalhes da instância.
 - **Faturamento**: o uso de endereços IP públicos para oferecer serviços pode incorrer em taxas. Para obter mais informações, consulte os [Métodos de faturamento de redes públicas](https://intl.cloud.tencent.com/document/product/213/10578).

## Liberação do endereço IP público
Você não pode associar ou liberar ativamente um endereço IP público que já esteja associado à uma instância.
Um endereço IP público associado à uma instância é liberado ou reatribuído nos seguintes casos:
- **Quando você encerra uma instância**. O Tencent Cloud libera um endereço IP público assim que você encerrar uma instância do CVM sob demanda.
- Quando você associa ou desassocia um [IP público elástico](https://intl.cloud.tencent.com/document/product/213/5733) à uma instância. Quando você associa um EIP à sua instância, o endereço IP público existente é liberado novamente no pool de IPs públicos. Quando você desassocia um EIP da sua instância, o Tencent Cloud atribui um novo endereço IP público a ela. Você não poderá usar seu endereço IP público antigo.

Caso precise de um endereço IP público estático, use um [IP público elástico (EIP)](https://intl.cloud.tencent.com/document/product/213/5733).

## Guia de operação
Para instruções detalhadas acerca de como obter e alterar seu endereço IP público, consulte:
- [Obtenção de um endereço IP público da instância](https://intl.cloud.tencent.com/document/product/213/17940)
- [Alteração do seu endereço IP público](https://intl.cloud.tencent.com/document/product/213/16642)
