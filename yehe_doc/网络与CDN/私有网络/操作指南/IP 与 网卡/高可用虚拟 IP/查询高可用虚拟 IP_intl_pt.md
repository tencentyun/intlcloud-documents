É possível exibir todos os detalhes do HAVIP em uma região específica no console dele.

## Instruções
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc/).
2. Selecione **IP and Interface (IP e interface)** > **HAVIP** na barra lateral esquerda para acessar a página de gerenciamento do HAVIP.
3. Selecione uma região de destino para exibir os detalhes de todos os HAVIPs que você solicitou.
	A descrição do campo é a seguinte:
	+ ID/Name (ID/Nome): ID refere-se ao ID gerado do HAVIP automaticamente depois de ser criado. Você pode clicar nela para exibir as informações básicas do HAVIP. O nome é definido pelo usuário quando o HAVIP é criado.
	+ Status: indica se o HAVIP está especificado como um endereço IP flutuante no arquivo de configuração do software de HA no CVM. Um HAVIP configurado com êxito estará com o status **Bound with CVM (Vinculado ao CVM)**; caso contrário, estará com o status **Not bound with CVM yet (Ainda não vinculado ao CVM)**.
	+ Address (Endereço): endereço HAVIP.
	+ Backend ENI (ENI de back-end): refere-se ao ID do ENI do CVM vinculado. Caso o HAVIP ainda não esteja vinculado ao CVM, este campo será exibido como **-**.
	+ Server (Servidor): refere-se ao ID do CVM vinculado. Caso o HAVIP ainda não esteja vinculado ao CVM, este campo será exibido como **-**.
	+ EIP: refere-se ao EIP vinculado. Caso o HAVIP não esteja vinculado a um EIP, este campo será exibido como **-**.
	+ Virtual Private Cloud: refere-se ao VPC do HAVIP.
	+ Subnet (Sub-rede): refere-se à sub-rede do HAVIP.
	+ Application Time (Hora da solicitação): refere-se à hora em que este HAVIP foi solicitado.
	+ Operation (Operação): refere-se às operações compatíveis, incluindo **Bind (Vincular)**, **Unbind (Desvincular)** e **Release (Liberar)**.
	   +  Bind (Vincular): vincula um EIP
	   +  Unbind (Desvincular): desvincula um EIP
	   +  Release (Liberar): libera o HAVIP
3. Insira o ID, o nome ou o endereço na caixa de pesquisa à direita para pesquisar rapidamente por HAVIPs.
4. Clique no ícone ao lado da caixa de pesquisa para atualizar a página.
