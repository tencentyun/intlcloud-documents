## Visão geral
Os grupos de segurança são usados para gerenciar o tráfego de e para redes públicas e privadas. Por motivos de segurança, a maior parte do tráfego de entrada é negada por padrão. Se você selecionou **Open all ports (Abrir todas as portas)** ou **Open ports 22, 80, 443, 3389 and ICMP protocol (Abrir as portas 22, 80, 443, 3389 e o protocolo ICMP)** como o modelo ao criar um grupo de segurança, as regras são criadas automaticamente e adicionadas ao grupo de segurança para permitir o tráfego nessas portas. Para obter mais informações, consulte [Grupos de segurança](https://intl.cloud.tencent.com/document/product/213/12452).

Este documento descreve como adicionar regras de grupos de segurança para permitir ou rejeitar o tráfego de e para redes públicas ou privadas.

## Observações

- As regras de grupos de segurança são compatíveis com as regras IPv4 e IPv6.
- **Open all ports (Abrir todas as portas)** permite o tráfego IPv4 e IPv6.

## Pré-requisitos
- É necessário ter um grupo de segurança existente. Se não tiver, consulte [Criação de um grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34271) para obter detalhes.
- É necessário saber qual tráfego é permitido ou rejeitado para sua instância do CVM. Para obter mais informações sobre as regras de grupos de segurança e seus casos de uso, consulte [Casos de uso de grupos de segurança](https://intl.cloud.tencent.com/document/product/213/32369).

### Direções
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Selecione [**Security Group (Grupo de segurança)**](https://console.cloud.tencent.com/cvm/securitygroup) na barra lateral esquerda para acessar a página de gerenciamento de grupos de segurança.
3. Selecione uma região e localize o grupo de segurança para o qual deseja definir as regras.
4. Clique em **Modify Rules (Modificar regras)** na coluna **Operation (Operação)**.
5. <span id="step05">Clique em **Inbound rules (Regras de entrada)** e escolha um dos métodos a seguir para adicionar as regras.</span>
![](https://main.qcloudimg.com/raw/e4c1f93fe75de51aa8de068da60a2206.png)
>? As instruções a seguir usam **Add a Rule (Adicionar uma regra)** como exemplo.
>
 - **Open all ports (Abrir todas as portas)**: este método é ideal se você não precisa de regras ICMP personalizadas e todo o tráfego passa pelas portas 20, 21, 22, 80, 443 e 3389 e pelo protocolo ICMP.
 - **Add a Rule (Adicionar uma regra)**: este método é ideal se você precisar usar vários protocolos e portas diferentes dos mencionados acima.
6. Na janela pop-up, defina as regras.
![](https://main.qcloudimg.com/raw/0114aa46ffabc46dd9d6921095f6e8fa.png)
Configure os seguintes parâmetros:
 - **Type (Tipo)**: **Custom (Personalizado)** fica selecionado por padrão. Também é possível escolher outro modelo de regras de sistema, incluindo **Login Windows CVMs (3389)**, **Login Linux CVMs (22)**, **Ping**, **HTTP (80)**, **HTTPS (443)**, **MySQL (3306)** e **SQL Server (1433)**.
 - **Source (Origem)** ou **Destination (Destino)**: origem (regras de entrada) ou destino (regras de saída) do tráfego. É necessário especificar uma das seguintes opções:
<table>
	<tr><th>Origem ou destino</th><th>Descrição</th></tr>
	<tr><td>Um único endereço IPv4 ou um intervalo IPv4</td><td>Na notação CIDR, como <code>203.0.113.0</code>, <code>203.0.113.0/24</code> ou <code>0.0.0.0/0</code>, em que <code>0.0.0.0/0</code> indica que todos os endereços IPv4 serão correspondidos.</td></tr>
	<tr><td>Um único endereço IPv6 ou um intervalo IPv6</td><td>Na notação CIDR, como <code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code> ou <code>0::0/0</code>, em que <code>::/0</code> ou <code>0::0/0</code> indica que todos os endereços IPv6 serão correspondidos.</td></tr>
	<tr><td>ID do grupo de segurança referenciado. Você pode fazer referência ao ID do:<ul  style="margin: 0;"><li>Grupo de segurança atual</li><li>Outro grupo de segurança</li></ul>
</td><td><ul  style="margin: 0;"><li>Para fazer referência ao grupo de segurança atual, digite o ID do grupo associado ao CVM.</li><li>Também é possível fazer referência a outro grupo de segurança na mesma região e que pertence ao mesmo projeto, inserindo o ID do grupo.</li></ul>
<blockquote class="d-mod-explain"><div class="d-mod-title d-explain-title"><i class="d-icon-explain"></i>Observações:</div>
<p></p><ul>
<li>O grupo de segurança referenciado fica disponível para você como uma funcionalidade avançada. As regras do grupo de segurança referenciado não são adicionadas ao grupo de segurança atual.</li>
<li>Se você inserir o ID do grupo de segurança em **Source (Origem)**/**Destination (Destino)** ao configurar as regras do grupo de segurança, os endereços IP privados das instâncias do CVM e os ENIs que estão associados a esse ID do grupo de segurança são usados como a origem/o destino. Isso não inclui os endereços IP públicos.</li>
</ul>
</blockquote>
</td></tr>
	<tr><td>Faça referência a um objeto de endereço IP ou objeto de grupo de endereço IP em um <a href="https://intl.cloud.tencent.com/document/product/215/31867">modelo de parâmetros</a>.</td><td>-</td></tr>
</table>
 - **Protocol port (Porta de protocolo)**: insira o tipo de protocolo e intervalo de portas ou faça referência a um protocolo/porta ou protocolo/grupo de portas em um [modelo de parâmetros](https://intl.cloud.tencent.com/document/product/215/31867). Os tipos de protocolos compatíveis incluem TCP, UDP, ICMP, ICMPv6 e GRE nos formatos a seguir.
    - Porta única: como `TCP: 80`.
    - Várias portas: como `TCP:80,443`.
    - Intervalo de portas: como `TCP:3306-20000`.
    - Todas as portas: como `TCP:ALL`.
 - **Policy (Política)**: **Allow (Permitir)** ou **Refuse (Recusar)**. **Allow (Permitir)** fica selecionado por padrão.
    - Permitir: o tráfego para esta porta é permitido.
    - Recusar: os pacotes de dados serão descartados sem nenhuma resposta.
 - **Notes (Observações)**: uma breve descrição da regra para facilitar o gerenciamento.
7. <span id="step07">Clique em **Complete (Concluir)** para terminar de adicionar a regra.</span>
8. Para adicionar uma regra de saída, clique em **Outbound rule (Regra de saída)** e consulte a [Etapa 5](#step05) à [Etapa 7](#step07).
