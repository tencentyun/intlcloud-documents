## Visão geral
Criar um snapshot é um método importante para o compartilhamento e a migração de dados. Os discos em nuvem criados usando um snapshot possuem todos os dados no snapshot. É possível usar um snapshot para criar um disco em nuvem cuja capacidade seja maior ou igual à do snapshot.
- Quando você usa um snapshot para criar um disco de dados com a mesma capacidade do snapshot, o disco de dados não precisa ser inicializado. Para ler e gravar nele, basta [montá-lo](https://intl.cloud.tencent.com/document/product/362/32401) e selecionar **Server Management (Gerenciamento do servidor)** -> **Storage (Armazenamento)** -> **Disk Management (Gerenciamento do disco)** para associá-lo a um CVM.
- Quando você usa um snapshot para criar um disco de dados cuja capacidade é maior do que a do snapshot, o sistema apenas expande o bloco de armazenamento e não estende o sistema de arquivos ou converte o formato da partição. Depois que você [montar](https://intl.cloud.tencent.com/document/product/362/32401) o novo disco de dados, ele só pode usar o sistema de arquivos e os dados do snapshot de origem e não pode usar o novo espaço em disco. É preciso estender manualmente o sistema de arquivos e converter o formato da partição.
  Por exemplo, se você deseja um disco de dados de 3 TB usando um snapshot de disco de dados que usa o formato de partição MBR e tem uma capacidade de 1 TB, é necessário formatar o disco de dados no estilo de partição GPT porque o espaço máximo em disco suportado no estilo de partição MBR é 2 TB. Essa operação **excluirá os dados originais**.

Este documento descreve como usar um snapshot para criar um disco em nuvem na página [Lista de snapshots](https://console.cloud.tencent.com/cvm/snapshot). Ao [criar um disco em nuvem](https://intl.cloud.tencent.com/document/product/362/5744), é possível configurar o parâmetro **Snapshots** e especificar um snapshot para criar o disco em nuvem.


## Instruções
### Criação de um disco em nuvem com um snapshot no console
1. Faça login na página [Lista de snapshots](https://console.cloud.tencent.com/cvm/snapshot).
2. Na linha do snapshot de destino, clique em **More (Mais)** e selecione **Create Cloud Disk (Criar disco em nuvem)**.
3. Na caixa de diálogo **Purchase Data Disk (Adquirir disco de dados)**, configure os seguintes parâmetros:
<table>
     <tr>
         <th width="12%">Parâmetro</th>  
         <th>Descrição</th>  
     </tr>
	<tr>
         <td>Zona de disponibilidade</td>
         <td>Obrigatório.</br>A zona de disponibilidade onde o disco em nuvem criado está localizado. Não pode ser modificada após a criação do disco em nuvem.</td>
     </tr>
     <tr>
         <td>Tipo de disco em nuvem</td>
         <td>Obrigatório.</br>Os valores incluem:<ul><li>Premium Cloud Storage</li><li>SSD Cloud Storage</li></ul></td>
     </tr>
     <tr>
         <td>Capacidade</td>
         <td>Obrigatório.</br>O CBS fornece a seguinte capacidade e especificações de discos em nuvem:<ul><li>Premium Cloud Storage: 50 a 16.000 GB</li><li>SSD Cloud Storage: 100 a 16.000 GB</li></ul>Quando você cria um disco em nuvem usando um snapshot, a capacidade do disco não pode ser menor do que a do snapshot. Se você não especificar esse parâmetro, a capacidade do disco será igual à do snapshot por padrão.</td>
     </tr>
    <tr>
         <td>Snapshots</td>
    	 <td>Opcional. Para usar um snapshot para criar um disco em nuvem, selecione <b>Create a Cloud Disk with a Snapshot (Criar um disco em nuvem com um snapshot)</b> e o snapshot necessário. <ul><li>A capacidade do disco é a mesma do snapshot por padrão. É possível ajustar a capacidade para ser maior do que a do snapshot.</li><li>O tipo de disco é o mesmo do snapshot por padrão. É possível alterar o tipo de disco em nuvem.</li></ul></td>
     </tr>
     <tr>
         <td>Nome do disco</td>
         <td>Opcional.</br>São aceitos no máximo 20 caracteres. Deve começar com uma letra e pode ser uma combinação de letras, dígitos e caracteres especiais (`.`, `_`, `:` e `-`). Esse parâmetro pode ser modificado após a criação do disco em nuvem.<ul><li>Se você criar apenas um disco em nuvem, o nome do disco será o nome do disco em nuvem que você criar.</li><li>Se você criar vários discos em nuvem ao mesmo tempo, o nome do disco inserido será usado como o prefixo do nome do disco final, no formato de <b>nome do disco_número<b>, por exemplo, "nome do disco_0" a "nome do disco_49".</li></ul></td>
     </tr>
     <tr>
         <td>Projeto</td>
         <td>Obrigatório.</br>Ao criar um disco em nuvem, é possível configurar o projeto ao qual ele pertence. O valor padrão é <b>DEFAULT PROJECT (PROJETO PADRÃO)</b>.</td>
     </tr>
     <tr>
         <td>Tag</td>
         <td>Opcional.</br>Ao criar um disco em nuvem, é possível vincular uma tag a ele. As tags são usadas para identificar os recursos de nuvem, ajudando você a categorizar e pesquisá-los facilmente. Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/651">Tag</a>.</td>
     </tr>
     <tr>
         <td>Modo de faturamento</td>
         <td>Obrigatório.<li>O valor é <b>Pay as you go (Pagamento conforme o uso)</b>.</li></ul></td>
     </tr>
     <tr>
     	 <tr>
         <td>Snapshot programado</td>
         <td>Opcional.</br>Ao criar um disco em nuvem, é possível selecionar <b>Scheduled Snapshot (Snapshot programado)</b> para criar snapshots para o disco em nuvem periodicamente com base na política de snapshots programados criada. Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/362/35238">Snapshots programados</a>.
     </tr>
     <tr>
         <td>Quantidade</td>
         <td>Opcional.</br>O valor padrão é <b>1<b>, o que indica que apenas um disco em nuvem foi criado. Atualmente, até 50 discos em nuvem podem ser criados de uma vez.</td>
     </tr>
     <tr>
         <td>Período</td>
         <td></li><li>Se o <b>Billing Mode (Modo de faturamento)</b> for definido como <b>Pay as you go (Pagamento conforme o uso)</b>, esse parâmetro não é aplicável.</li></ul></td>
     </tr>
    	 		 <tr>
         <td>Renovação automática</td>
         <td> <li>Se o <b>Billing Mode (Modo de faturamento)</b> for definido como <b>Pay as you go (Pagamento conforme o uso)</b>, esse parâmetro não é aplicável.</li></ul></td>
     </tr>
</table>
4. Clique em <b>OK</b>.
 - Se o <b>Billing Mode (Modo de faturamento)</b> for <b>Pay as you go (Pagamento conforme o uso)</b>, a criação está concluída.
  <ol>
  1. Depois de confirmar sua configuração, selecione se deseja usar um voucher com base nas suas necessidades reais e clique em <b>OK</b>.
  2. Conclua o pagamento.
 </ol>



5. É possível visualizar o(s) disco(s) em nuvem que você criou na página da lista do [Cloud Block Storage](https://console.cloud.tencent.com/cvm/cbs). Os novos discos em nuvem elásticos estão no estado <b>To be mounted (A ser montado)</b>. Para obter mais informações sobre como montar um disco em nuvem elástico em um CVM na mesma zona de disponibilidade, consulte [Montagem de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/32401).

### Uso de uma API para criar um disco em nuvem a partir de um snapshot
É possível usar a API `CreateDisks` para criar um disco em nuvem. Para obter mais informações, consulte [CreateDisks](https://intl.cloud.tencent.com/document/product/362/16312).
