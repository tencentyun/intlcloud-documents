## Cenário de operação
Os grupos de segurança são usados para determinar se as solicitações de acesso da internet ou de redes privadas devem ser permitidas. Por questões de segurança, a negação de acesso é adotada na direção de entrada na maioria dos casos. Se você selecionar o modelo "Open all ports to the Internet (Abrir todas as portas para a internet)" ou "Open ports 22, 80, 443, and 3389 and the ICMP protocol to the Internet (Abrir as portas 22, 80, 443 e 3389 e o protocolo ICMP para a internet)" ao criar um grupo de segurança, o sistema adicionará automaticamente regras de grupo de segurança para algumas portas de comunicação com base no modelo selecionado. 

Este documento descreve como adicionar regras de grupo de segurança para permitir ou proibir CVMs em um grupo de segurança de acessar a internet ou instâncias do VPC.

## Observações

- As regras de grupo de segurança são divididas em IPv4 e IPv6.
- **Open all ports (Abrir todas as portas)** é aplicável às regras de grupo de segurança IPv4 e IPv6.

## Pré-requisitos
- Você criou um grupo de segurança. 
- Você sabe quais solicitações de acesso à internet ou rede privada precisam ser permitidas ou rejeitadas para sua instância do CVM. Para obter mais casos de uso de configurações de regras de grupo de segurança, consulte [Casos de uso de grupos de segurança](https://intl.cloud.tencent.com/document/product/215/35519).

## Etapas
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na barra lateral esquerda, clique em **[Security Group (Grupo de segurança)](https://console.cloud.tencent.com/cvm/securitygroup)** para ter acesso à pagina de gerenciamento de grupos de segurança.
3. Na página de gerenciamento de grupos de segurança, selecione **Region (Região)** e localize a linha do grupo para o qual deseja definir regras.
4. Na coluna de operação, clique em **Modify Rules (Modificar regras)**.
5. <span id="step05">Na página de regras do grupo de segurança, clique em **Inbound rules (Regras de entrada)** e selecione um dos seguintes modos com base em suas necessidades reais para concluir a operação.</span>
> Os exemplos de operação abaixo usam o modo 2 (adicionar regras).
>
 - Modo 1 (abrir todas as portas): é aplicável a cenários em que as regras do protocolo ICMP não precisam ser definidas e as operações podem ser feitas por meio das portas 22, 3389, 80, 443, 20 e 21, assim como do protocolo ICMP.
 - Modo 2 (adicionar regras): é aplicável a cenários em que vários protocolos de comunicação, como ICMP, precisam ser definidos.
6. Na janela **Add Inbound Rules (Adicionar regras de entrada)** que é exibida, defina as regras.
Os principais parâmetros necessários para adicionar uma regra são os seguintes:
 - Type (Tipo): o valor padrão é "Custom (Personalizado)". Você também pode selecionar outro modelo de regras de sistema, como "Windows login (Login no Windows)", "Linux login (Login no Linux)", "Ping", "HTTP (80)" ou "HTTPS (443)".
 - Source (Origem)/Destination (Destino): a origem (regras de entrada) ou o destino (regras de saída) do tráfego. Escolha uma das seguintes opções:
<table>
	<tr><th>Origem/destino especificados</th><th>Descrição</th></tr>
	<tr><td>Um endereço IPv4 ou intervalo de endereços IPv4</td><td>Especifique-o na notação CIDR (por exemplo, <code>203.0.113.0</code>, <code>203.0.113.0/24</code> ou <code>0.0.0.0/0</code>, em que <code>0.0.0.0/0</code> indica que todos os endereços IPv4 serão correspondidos).</td></tr>
	<tr><td>Um endereço IPv6 ou um intervalo de endereços IPv6</td><td>Especifique-o na notação CIDR (por exemplo, <code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code> ou <code>0::0/0</code>, em que <code>::/0</code> ou <code>0::0/0</code> indica que todos os endereços IPv6 serão correspondidos).</td></tr>
	<tr><td>Importar ID do grupo de segurança: você pode importar os seguintes IDs de grupos de segurança:<ul  style="margin: 0;"><li>ID do grupo de segurança</li><li>Outro grupo de segurança</li></ul>
</td><td><ul  style="margin: 0;"><li>O grupo de segurança atual se refere aos CVMs associados ao grupo de segurança.</li><li>Outro grupo de segurança se refere ao ID de outro grupo de segurança no mesmo projeto e na mesma região.</li></ul>
</td></tr>
	<tr><td>Importe o objeto de endereço IP ou o objeto de grupo de endereços IP no <a href="https://intl.cloud.tencent.com/document/product/215/31867">modelo de parâmetros</a>.</td><td>-</td></tr>
</table>
 - Protocol port (Porta de protocolo): insira o tipo de protocolo e intervalo de portas ou importe uma porta de protocolo ou grupo de portas de protocolo no [modelo de parâmetros](https://intl.cloud.tencent.com/document/product/215/31867).
 - Policy (Política): o valor padrão é "Permit (Permitir)".
    - Permit (Permitir): permite solicitações de acesso pela porta.
    - Reject (Rejeitar): descarta os pacotes de dados diretamente sem retornar nenhuma resposta.
 - Remarks (Observações): descreve resumidamente a regra para facilitar o gerenciamento futuro.
7. <span id="step07">Clique em **Finish (Finalizar)**. As regras de entrada são adicionadas ao grupo de segurança.</span>
8. Na página de regra do grupo de segurança, clique em **Outbound Rules (Regras de saída)** e adicione regras de saída ao grupo de segurança referindo-se a [Etapa 5](#step05) à [Etapa 7](#step07).
