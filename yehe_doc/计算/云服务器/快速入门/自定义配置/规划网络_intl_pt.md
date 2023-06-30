Uma instância do Tencent Cloud Virtual Private Cloud (VPC) é um espaço de rede isolado logicamente e definido pelo usuário do Tencent Cloud. Nessa instância, os usuários podem personalizar os intervalos de IP, os endereços de IP e as políticas de roteamento. Portanto, recomendamos que você use uma instância do VPC para suas empresas.

Para ajudá-lo a usar melhor as instâncias do Tencent Cloud VPC, fornecemos as seguintes recomendações de planejamento de rede.

### Determinação da quantidade de instâncias do VPC

- Funcionalidades:
	- As instâncias do VPC são específicas da região. Por padrão, os CVMs em regiões diferentes não podem se comunicar uns com os outros. Se a comunicação entre regiões for necessária, estabeleça uma [conexão de emparelhamento](https://intl.cloud.tencent.com/document/product/553).
	- Por padrão, as instâncias diferentes do VPC na mesma região não podem se comunicar entre si. Se a comunicação entre VPCs for necessária, estabeleça uma [conexão de emparelhamento](https://intl.cloud.tencent.com/document/product/553).
	- Por padrão, as zonas de disponibilidade diferentes na mesma instância do VPC podem se comunicar entre si.
- Recomendações:
	- Se sua empresa requer a implantação de sistemas entre regiões, são necessárias várias instâncias do VPC. Nesse caso, é possível criar uma instância do VPC próxima à região onde seus clientes estão localizados, para reduzir a latência de acesso e melhorar a velocidade de acesso.
	- Se você implantou várias empresas na região atual e deseja implementar o isolamento de rede entre empresas diferentes, é possível criar uma instância do VPC para cada empresa na região atual.
	- Se a implantação de empresas entre regiões ou o isolamento de rede entre as empresas não for necessário, é possível usar somente uma instância do VPC.

### Determinação da divisão de sub-rede
- Funcionalidades:
	- Sub-redes são blocos de endereços IP em uma instância do VPC. Todos os recursos de nuvem em uma instância do VPC devem ser implantados em sub-redes.
	- Na mesma instância do VPC, os intervalos de IP das sub-redes não devem se sobrepor.
	- O Tencent Cloud atribui automaticamente endereços IP privados iniciais de intervalos de IP do VPC. O bloco CIDR do Tencent Cloud VPC pode ser qualquer um dos seguintes intervalos de IP do VPC. Para um endereço IP dentro desses intervalos, sua máscara varia de 16 a 28, e a máscara real é determinada pela rede privada onde reside a instância.
	 - **10.0**.0.0-**10.255**.255.255
	 - **172.16**.0.0-**172.31**.255.255
	 - **192.168**.0.0-**192.168**.255.255
	- Depois que uma instância do VPC é criada, seu intervalo de IP não pode ser modificado.
- Recomendações:
	- Se apenas as sub-redes do VPC precisarem ser divididas e a comunicação com a rede básica ou o IDC não estiver envolvida, escolha qualquer um dos intervalos de IP anteriores para criar uma sub-rede.
	- Se a comunicação com a rede básica for necessária, estabeleça uma instância do VPC com o intervalo de IP de 10.[0-47].0.0/16 e seus subconjuntos, conforme necessário.
	- Se for necessário um VPN, o intervalo de IP local (da instância do VPC) e o intervalo de IP de par (do seu IDC) não podem se sobrepor. Portanto, não use o intervalo de IP de par ao criar uma sub-rede.
	- Durante a divisão da sub-rede, também é necessário considerar a quantidade de endereços IP disponíveis em um intervalo de IP.
	- Recomendamos que as sub-redes sejam divididas de acordo com os módulos da empresa para as empresas na mesma instância do VPC. Por exemplo, a sub-rede A é usada para a camada da web, a sub-rede B é usada para a camada lógica e a sub-rede C é usada para a camada de banco de dados. Isso facilita o controle de acesso e a filtragem usando a ACL de rede.

### Determinação de políticas de rotas

- Funcionalidades:
	- Uma tabela de rotas consiste em uma série de regras de roteamento que controlam o fluxo de tráfego de sub-redes em uma instância do VPC.
	- Cada sub-rede deve ser associada a apenas uma tabela de rotas.
	- Uma única tabela de rotas pode ser associada a várias sub-redes.
	- Quando uma instância do VPC é criada, o sistema gera automaticamente uma tabela de rotas padrão para a instância, que define que as instâncias do VPC podem se comunicar entre si por meio da rede privada.
- Recomendações:
	- Se você não precisa controlar o fluxo de tráfego de sub-redes e as instâncias do VPC são interconectadas por meio da rede privada por padrão, é possível usar a tabela de rotas padrão sem precisar configurar uma política de roteamento personalizada.
	- Se for necessário controlar o fluxo de tráfego de sub-redes, consulte a [Visão geral](https://intl.cloud.tencent.com/document/product/215/31810) no site oficial.


Para obter mais informações sobre as instâncias do VPC, consulte [VPC](https://intl.cloud.tencent.com/document/product/215).



