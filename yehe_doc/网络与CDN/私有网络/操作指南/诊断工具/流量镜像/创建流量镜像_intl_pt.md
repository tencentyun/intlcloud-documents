O espelho de tráfego fornece um serviço de coleta de tráfego que permite filtrar o tráfego do ENI especificado usando 5 tuplas e outras regras. Depois, é possível copiar o tráfego filtrado para instâncias do CVM no mesmo VPC. Essa funcionalidade é aplicável a casos de uso, incluindo auditoria de segurança, monitoramento de risco, solução de problemas e análise empresarial. Este documento descreve como criar um espelho de tráfego.
>? Atualmente, a funcionalidade de espelho de tráfego está na versão beta. Se você quiser testá-la, [envie um tíquete](https://console.cloud.tencent.com/workorder/category). Salve o link do console do Espelho de tráfego para logins posteriores; caso contrário, pode ser necessário solicitar novamente.

## Pré-requisitos
Certifique-se de que o IP coletado e o IP de recebimento estejam no mesmo VPC, e que o IP coletado tenha uma tabela de rotas apontando para o IP de recebimento.
## Instruções
### Etapa 1: criar uma origem de espelho de tráfego
1. Abra o link que você recebeu depois de [enviar um tíquete](https://console.cloud.tencent.com/workorder/category) e faça login no console do Espelho de tráfego. No seletor **Region (Região)** superior, selecione a região na qual o espelho de tráfego será criado.
2. Clique em **+New (+Novo)**.
>? É possível criar até 5 espelhos de tráfego em um VPC.

3. Na janela pop-up, configure da seguinte maneira:
 - Digite um nome para o espelho de tráfego, que não pode exceder 60 caracteres.
 - Selecione **Network (Rede)**.
 - Selecione **Collection Range (Intervalo de coleta)**:
    - **Virtual Private Cloud**: todo o tráfego no VPC, exceto o tráfego espelhado de IPs de recebimento, será coletado; o que geralmente se aplica ao cenário de espelho completo.
    - **Subnet (Sub-rede)**: todo o tráfego na sub-rede do VPC, exceto o tráfego espelhado de IPs de recebimento, será coletado. Esta opção requer a seleção de sub-redes específicas.
    - **ENI**: todo o tráfego no VPC será coletado, mas o tráfego do ENI vinculado aos IPs de recebimento será excluído. Esta opção requer a seleção de ENIs específicos.
      ![](https://main.qcloudimg.com/raw/5a359241aabeccd7424324e8357d8251.png)
 - Selecione **Collection Type (Tipo de coleção)**: selecione a direção do tráfego conforme necessário. Existem três opções: All traffic (Todo o tráfego), Traffic out (Tráfego de saída) e Traffic in (Tráfego de entrada).
 - Selecione **Traffic filtering (Filtragem de tráfego)**: selecione um método para filtrar o tráfego desnecessário e manter o espelho pequeno e leve.
    - **N/A**: todo o tráfego configurado será coletado.
    - **Quintuple (Quíntuplo)**: o tráfego que atender às condições de 5 tuplas será coletado. Depois que essa opção for selecionada, especifique o **Protocol (Protocolo)**, o **Source IP range (Intervalo de IP de origem)**, o **Destination IP range (Intervalo de IP de destino)**, a **Source port (Porta de origem)** e a **Destination port (Porta de destino)**. Você pode clicar em **Add (Adicionar)** para criar outra condição de filtro. Apenas o tráfego que atender a todas as condições do filtro será coletado.
    ![](https://main.qcloudimg.com/raw/1b49eca6a1e7f736633ee2762f5d6620.png)
    - **The next hop is the NAT gateway (O próximo salto é o NAT Gateway)**: coleta o tráfego cujo endereço do próximo salto é o NAT Gateway. Depois que essa opção for selecionada, selecione o NAT Gateway correspondente ao lado de **Condition (Condição)**.
4. Quando concluir a configuração, clique em **Next (Avançar)**.

### Etapa 2: criar um destino de espelho de tráfego
1. Defina o tráfego de recebimento da seguinte maneira:
    + **Receiving IP (IP de recebimento)**: insira os endereços IP que recebem o tráfego espelhado.
       > ?
       > + Se este campo for deixado em branco, nenhum tráfego será espelhado. Portanto, insira pelo menos um IP de recebimento.
       > + Separe os IPs com quebras de linha ou vírgulas.
       > + O tráfego gerado pelo IP de recebimento em um VPC não será coletado.

    + **Balance method (Método de equilíbrio)**: selecione um dos seguintes:
        + **Evenly distribute traffic (Distribuir uniformemente o tráfego)**: todo o tráfego será copiado para esses IPs de recebimento uniformemente.
        + **HASH by ENI (HASH por ENI)**: tráfego do mesmo ENI será copiado para o mesmo IP de recebimento.
 ![](https://main.qcloudimg.com/raw/8bec0de6223c109daed7eefef1394959.png)
2. Ao concluir a configuração, clique em **OK**.

## Validação do resultado
>! Este documento usa como exemplo a criação de um espelho de tráfego que coleta o tráfego de saída do ENI 10.0.0.14, acessando o site www.qq.com.

1. Volte para a página **Traffic mirroring (Espelhamento de tráfego)**. Se o espelho de tráfego recém-criado for exibido com **Collect Traffic (Coletar tráfego)** habilitado, significa que ele foi criado com êxito.
![](https://main.qcloudimg.com/raw/fd6191f3c858d0f2dd799a467c0d1c40.png)
2. Execute as etapas a seguir para verificar se o tráfego coletado é espelhado para o IP de recebimento.
	1. Gere o tráfego de ENI. Por exemplo, você pode fazer login no CVM de origem e executar o comando `ping ***public IP***`.
    **Dados de origem:**
	 ![](https://main.qcloudimg.com/raw/74ad4cbd7a6f2179b441cafee5976bba.png)
	 <span id="buzhou2"></span>
	2. Faça login no CVM de destino e execute os seguintes comandos para capturar os dados e salvá-los como um arquivo “.cap” ou “.pcap”. Este documento usa o arquivo “.pcap” como exemplo.
	      ```plaintext
	   tcpdump -i eth0 -w capture-2020-10-27.pcap    #Insira o nome do arquivo real.
      ```
	**Pacotes de destino:** 
	    ![](https://main.qcloudimg.com/raw/404f6d2c612ae76b78aa63a624e98910.png)
	3. Use um simulador de terminal (como SecureCRT) para fazer login no CVM de destino e exportar o arquivo salvo na [Etapa ii](#buzhou2).
       ```plaintext
	    sz -bye capture-2020-10-27.pcap
       ```
	4. Use um analisador de pacotes (como o Wireshark) para obter dados do arquivo “capture-2020-10-27.pcap” baixado. Neste exemplo, 12 pacotes espelhados do CVM de origem são obtidos do CVM de destino.
	 **Verificação de pacotes:**
	 ![](https://main.qcloudimg.com/raw/8011aef82006411e35edd41bf5eae5c4.png)
3. Se um pacote excepcional for obtido, ou se não for possível obter pacotes, [envie um tíquete](https://console.cloud.tencent.com/workorder/category).

## Operações subsequentes
- [Ativação ou desativação do espelho de tráfego](https://intl.cloud.tencent.com/document/product/215/36393)
- [Modificação do espelho de tráfego](https://intl.cloud.tencent.com/document/product/215/36393)
- [Adição de uma tag](https://intl.cloud.tencent.com/document/product/215/36393)
- [Exclusão do espelho de tráfego](https://intl.cloud.tencent.com/document/product/215/36393)
