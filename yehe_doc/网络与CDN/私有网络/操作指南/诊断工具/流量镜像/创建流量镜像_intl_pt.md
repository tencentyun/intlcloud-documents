O Espelho de tráfego fornece um serviço de coleta de tráfego que permite filtrar o tráfego do ENI especificado usando 5 tuplas e outras regras. Depois, é possível copiar o tráfego filtrado para as instâncias da CVM no mesmo VPC. Essa funcionalidade é aplicável a casos de uso que incluem: auditoria de segurança, monitoramento de risco, solução de problemas e análise empresarial. Este documento descreve como criar um espelho de tráfego.
>? Atualmente, a funcionalidade Espelho de tráfego está na versão beta. Se você quiser testá-la, [envie um tíquete](https://console.cloud.tencent.com/workorder/category). Salve o link do console do Espelho de tráfego para logins posteriores; caso contrário, pode ser necessário solicitar novamente.

## Pré-requisitos
Confira se o IP de origem e a ENI de destino estão na mesma VPC, e se o IP de origem tem uma tabela de rotas apontando para a ENI de destino.
## Instruções
### Etapa 1: criar uma origem de espelho de tráfego
1. Abra o link que você recebeu após [enviar um tíquete](https://console.cloud.tencent.com/workorder/category) e faça login no console do Espelho de tráfego. No seletor **Region (Região)** superior, selecione a região na qual o espelho de tráfego será criado.
2. Clique em **+New (+Novo)**.
>? É possível criar até 5 espelhos de tráfego em uma VPC.
>
3. Na janela pop-up, configure da seguinte maneira:
   - Insira um nome para o espelho de tráfego (até 60 caracteres).
   - Selecione **Network (Rede)**.
   - Selecione **ENI** para **Collection Range (Intervalo de coleta)**. Ou seja, todo o tráfego na VPC será coletado, mas será excluído o tráfego da ENI que está vinculada aos IPs de recebimento. Esta opção requer a seleção de ENIs específicas.
![](https://qcloudimg.tencent-cloud.cn/raw/902cad1c6ecd774e67ffe72d3ce4ab64.png)
   - Selecione **Collection type (Tipo de coleta)**: selecione a direção do tráfego conforme necessário. Existem três opções: All traffic (Todo o tráfego), Traffic out (Tráfego de saída) e Traffic in (Tráfego de entrada).
   - Selecione **Traffic filtering (Filtragem de tráfego)**: selecione um método para filtrar o tráfego desnecessário e manter o espelho pequeno e leve.
      - **N/A**: todo o tráfego configurado será coletado.
      - **Quintuple (Quíntuplo)**: o tráfego que atender às condições de 5 tuplas será coletado. Depois que essa opção for selecionada, especifique o **Protocol (Protocolo)**, o **Source IP range (Intervalo de IP de origem)**, o **Destination IP range (Intervalo de IP de destino)**, a **Source port (Porta de origem)** e a **Destination port (Porta de destino)**. Você pode clicar em **Add (Adicionar)** para criar outra condição de filtro. Apenas o tráfego que atender a todas as condições de filtro será coletado.
    ![](https://qcloudimg.tencent-cloud.cn/raw/ab47286ffbc185a6287552ac44de0c6f.png)
   - **The next hop is the NAT gateway (O próximo salto é o NAT Gateway)**: coleta o tráfego cujo endereço do próximo salto é o NAT Gateway. Após selecionar essa opção, selecione o NAT Gateway correspondente ao lado de **Condition (Condição)**.
4. Quando concluir a configuração, clique em **Next (Avançar)**.

### Etapa 2: criar um destino de espelho de tráfego
1. Defina o tráfego de recebimento da seguinte maneira:
   + **Target type (Tipo de destino)**: selecione a ENI de destino para receber o tráfego.
> ?
> + Pelo menos uma ENI de destino precisa ser selecionada.
> + O tráfego para a ENI de destino de dentro da VPC não é coletado.
>
   + **Balance method (Método de equilíbrio)**: 
        + **Evenly distribution (Distribuição uniforme)**: todo o tráfego é distribuído uniformemente entre todas as ENIs de destino.
        + **HASH by ENI (HASH por ENI)**: o tráfego de uma ENI é sempre encaminhado para uma ENI de destino fixo.
![](https://qcloudimg.tencent-cloud.cn/raw/4b3e1c1c5bde43ed33d1724b072bb5e6.png)
2. Clique em **OK**.

## Validação do resultado
>! Este documento usa como exemplo a criação de um espelho de tráfego que coleta o tráfego de saída da ENI 10.0.0.14, acessando o site www.qq.com.
>
1. Volte para a página **Traffic mirroring (Espelhamento de tráfego)**. Se o espelho de tráfego recém-criado for exibido com **Collect Traffic (Coletar tráfego)** habilitado, significa que ele foi criado com êxito.
![](https://main.qcloudimg.com/raw/fd6191f3c858d0f2dd799a467c0d1c40.png)
2. Execute as etapas a seguir para verificar se o tráfego coletado é espelhado para o IP de recebimento.
	1. Gere o tráfego da ENI. Por exemplo, você pode fazer login na CVM de origem e executar o comando ping **public IP**.
    **Dados de origem:**
	 ![](https://main.qcloudimg.com/raw/74ad4cbd7a6f2179b441cafee5976bba.png)
	2. [](id:buzhou2) Faça login na CVM de destino, e execute os seguintes comandos para capturar os dados e salvá-los como um arquivo “.cap” ou “.pcap”. Este documento usa o arquivo “.pcap” como exemplo.
```plaintext
tcpdump -i eth0 -w capture-2020-10-27.pcap    #Insira o nome do arquivo real.
```
	**Pacotes de destino:** 
 ![](https://main.qcloudimg.com/raw/404f6d2c612ae76b78aa63a624e98910.png)
	3. Use um simulador de terminal (como SecureCRT) para fazer login na CVM de destino e exportar o arquivo salvo na [Etapa ii](#buzhou2).
 ```plaintext
sz -bye capture-2020-10-27.pcap
 ```
	4. Use um analisador de pacotes (como o Wireshark) para obter os dados do arquivo “capture-2020-10-27.pcap” baixado. Neste exemplo, 12 pacotes espelhados da CVM de origem são obtidos da CVM de destino.
	 **Verificação de pacotes:**
![](https://main.qcloudimg.com/raw/8011aef82006411e35edd41bf5eae5c4.png)
3. Se um pacote excepcional for obtido, ou se não for possível obter pacotes, [envie um tíquete](https://console.cloud.tencent.com/workorder/category).

## Operações posteriores
- [Ativação ou desativação do espelho de tráfego](https://intl.cloud.tencent.com/document/product/215/36393)
- [Modificação do espelho de tráfego](https://intl.cloud.tencent.com/document/product/215/36393)
- [Adição de uma tag](https://intl.cloud.tencent.com/document/product/215/36393)
- [Exclusão do espelho de tráfego](https://intl.cloud.tencent.com/document/product/215/36393)
