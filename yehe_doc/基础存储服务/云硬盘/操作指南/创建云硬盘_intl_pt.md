## Visão geral
O CBS permite criar um disco em nuvem e adicioná-lo a qualquer CVM na mesma zona de disponibilidade. O disco em nuvem é identificado e usado pelo CVM por meio do mapeamento do dispositivo de armazenamento em bloco. Depois de criado, o disco em nuvem pode atingir seu desempenho máximo sem pré-busca.
É possível criar diferentes tipos de discos em nuvem do CBS com base nas necessidades empresariais. Para obter mais informações sobre os tipos de discos do CBS, consulte [Tipos do CBS](https://intl.cloud.tencent.com/document/product/362/31636).

## Pré-requisitos
- Antes de criar um disco em nuvem, é preciso [criar uma conta no Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985) e concluir a [verificação de identidade](https://intl.cloud.tencent.com/document/product/378/3629).

## Instruções
<dx-tabs>
:::Criação\sde\sum\sdisco\sem\snuvem\spelo\sconsole

1. Faça login no [Console do CBS](https://console.cloud.tencent.com/cvm/cbs).
2. Selecione uma região e clique em **+ New (+ Novo)**.
3. Na caixa de diálogo **Purchase Data Disk (Adquirir disco de dados)**, configure os seguintes parâmetros:
<table>
     <tr>
         <th width="12%">Parâmetro</th>  
         <th>Descrição</th>  
     </tr>
	 <tr>
         <td>Zona de disponibilidade</td>
         <td>Obrigatório.</br>A zona de disponibilidade onde o seu disco em nuvem está localizado. Não pode ser modificada após a criação do disco em nuvem.</td>
     </tr> 
	 <tr>
         <td>Tipo de disco em nuvem</td>
         <td>Obrigatório.</br>O CBS oferece 3 tipos de discos em nuvem:<ul><li>Premium cloud storage</li><li>SSD</li><li>Enhanced SSD</li></ul></td>
     </tr>
		 <tr>
			 <td>Criação de disco rápida</td>
			 <td>Opcional. Para criar um disco em nuvem usando um snapshot, é necessário marcar **Create a cloud disk with a snapshot (Criar um disco em nuvem com um snapshot)** e selecionar o snapshot que deseja usar.
				 <ul><li>A capacidade de um disco em nuvem criado usando um snapshot é igual à do snapshot por padrão. É possível ajustar a capacidade do disco.</li>
         <li>Quando você cria um disco em nuvem usando um snapshot, o tipo de disco é o mesmo do disco de origem do snapshot. É possível ajustar o tipo do disco.</li></ul></td>
		 </tr>
	 <tr>
         <td>Capacidade</td>
         <td>Obrigatório.</br>O CBS fornece a seguinte capacidade e especificações de discos em nuvem:<ul><li>Premium Cloud Storage: 10 GB a 16.000 GB</li><li>SSD: 100 GB a 16.000 GB</li><li>Enhanced SSD: 100 GB a 16.000 GB</li></ul>Quando você cria um disco em nuvem usando um snapshot, a capacidade do disco não pode ser menor do que a do snapshot. Se você não especificar esse parâmetro, a capacidade do disco será igual à do snapshot por padrão.</td>
     </tr>
	 <tr>
	 <tr>
         <td>Snapshot programado</td>
         <td>Opcional.<br>É possível associar políticas de snapshots programados ao criar um disco em nuvem para gerenciar regularmente seus snapshots de discos em nuvem. Atualmente, o Tencent Cloud oferece um nível gratuito de 50 GB para cada região da China Continental. Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/362/32415">Visão geral do faturamento</a>.
         </td>
     </tr>
     <tr>
         <td>Nome do disco</td>
         <td>Opcional.</br>No máximo 20 caracteres, começando com uma letra ou caractere chinês e pode ser uma combinação de letras maiúsculas e minúsculas, caracteres chineses, números e caracteres especiais `.`, `_`, `:`. Esse parâmetro pode ser modificado após a criação do disco em nuvem.<ul><li>Criação de um único disco em nuvem: nome do disco é o nome do disco em nuvem que você cria.</li><li>Criação em lote de discos em nuvem: ao criar vários discos em nuvem ao mesmo tempo, o nome do disco é o prefixo dos nomes dos discos em nuvem, que são **nome do disco_número** variando de "nome do disco_0" a "nome do disco_49".</li></ul></td>
     </tr>
	 <tr>
         <td>Projeto</td>
         <td>Obrigatório.</br>Ao criar um disco em nuvem, é possível configurar o projeto ao qual ele pertence. Valor padrão: **DEFAULT PROJECT (PROJETO PADRÃO)**.</td>
     </tr>
	 <tr>
         <td>Tag</td>
         <td>Opcional.</br>Ao criar um disco em nuvem, é possível vincular uma tag a ele. A tag é usada para identificação, ajudando você a categorizar e pesquisar facilmente os recursos de nuvem. Para obter mais informações sobre as tags, consulte <a href="https://intl.cloud.tencent.com/document/product/651">Tag</a>.</td>
     </tr>
	 <tr>
         <td>Modo de faturamento</td>
         <td>Obrigatório.</br>O faturamento do CBS é com pagamento conforme o uso.</td>
     </tr>
	  <tr>
         <td>Quantidade</td>
         <td>Opcional.</br>O valor padrão é **1**, o que significa que apenas um disco em nuvem foi criado. Atualmente, até 50 discos em nuvem podem ser criados de uma vez.</td>
     </tr>
	 <tr>
         <td>Período</td>
         <td>Esse parâmetro não se aplica ao modo de faturamento **Pay-as-you-go (Pagamento conforme o uso)**.</td>
     </tr>
</table>
4. Clique em **OK**.
 - Se o **Billing Mode (Modo de faturamento)** for **Pay-as-you-go (Pagamento conforme o uso)**, a criação está concluída.
  <ol>
  1. Depois de confirmar sua configuração, selecione se deseja usar o voucher com base nas suas necessidades reais e clique em **Confirm (Confirmar)**.
  2. Conclua o pagamento.
 </ol>
5. É possível visualizar o(s) disco(s) em nuvem que você criou na página da lista do [Cloud Block Storage](https://console.cloud.tencent.com/cvm/cbs). O disco em nuvem elástico recém-adicionado tem o status **To be mounted (A ser montado)**. Para montá-lo em um CVM na mesma zona de disponibilidade, consulte [Montagem de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/32401).

:::
:::Criação\sde\sum\sdisco\sem\snuvem\susando\sum\ssnapshot
Se você deseja criar um disco em nuvem que contenha todos os dados após a criação, você pode [criar discos em nuvem usando snapshots](https://intl.cloud.tencent.com/document/product/362/5757).
:::
:::Criação\sde\sum\sdisco\sem\snuvem\susando\sAPI
É possível usar a API `CreateDisks` para criar um disco em nuvem. Para obter mais informações, consulte [CreateDisks](https://intl.cloud.tencent.com/document/product/362/16312).
:::
</dx-tabs>
