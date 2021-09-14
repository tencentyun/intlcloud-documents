Quando você precisar criptografar os dados armazenados em um disco em nuvem devido à segurança da empresa ou motivos de conformidade, habilite a criptografia de disco em nuvem e use a infraestrutura fornecida pelo [Key Management Service (KMS) do Tencent Cloud](https://intl.cloud.tencent.com/product/kms) para proteger com eficácia a privacidade dos dados.
>Atualmente, essa funcionalidade está em teste beta. Para usá-la, é necessário [enviar um tíquete](https://console.cloud.tencent.com/workorder/category) para solicitar.
>

## Gerenciamento de chaves
O Tencent Cloud criptografa os dados em seus discos de nuvem usando uma chave de criptografia de dados baseada no algoritmo AES-256 padrão. Quando você usa a criptografia de disco em nuvem pela primeira vez, o sistema cria automaticamente uma chave mestra do cliente (CMK, do inglês "customer master key") que permite usar a funcionalidade de criptografia de disco em nuvem na região correspondente no KMS. Apenas uma CMK é criada e armazenada automaticamente no KMS, que é protegido por controles de segurança físicos e lógicos rígidos.
Em cada região, uma chave de dados (DK, do inglês "data key") de 256 bits exclusiva é usada para criptografar o disco em nuvem. Os snapshots criados por meio de discos em nuvem criptografados e discos em nuvem criptografados criados por meio de snapshots criptografados estão todos associados a essa DK. A DK é protegida pela infraestrutura de gerenciamento de chaves fornecida pelo KMS, que bloqueia efetivamente o acesso não autorizado. A DK de um disco em nuvem é usada apenas na memória do host onde a instância está localizada e não é armazenada em nenhuma mídia persistente (incluindo o próprio disco em nuvem) em formato de texto não criptografado.

## Princípios operacionais
Quando você configura seu disco em nuvem como criptografado, o KMS criptografa e descriptografa os dados automaticamente durante a operação de leitura. Os processos de criptografia e descriptografia são executados no host onde a instância do CVM está localizada, com impacto mínimo no desempenho de leitura e gravação do disco em nuvem. Para testar o desempenho dos discos em nuvem, consulte [Medição de desempenho do disco em nuvem](https://intl.cloud.tencent.com/document/product/362/6741).

Depois que o disco em nuvem criptografado é criado e montado na instância, o sistema criptografa os dados abaixo:
- Dados estáticos no disco em nuvem;
- Dados transmitidos entre o disco em nuvem e a instância (os dados do sistema operacional da instância não são criptografados);
- Todos os snapshots criados por meio de discos em nuvem criptografados;

## Limites de uso
A funcionalidade de criptografia de disco em nuvem está sujeita a estas limitações:

<table>
	<tr>
	<th width="20%">Limitação</th>
	<th>Descrição</th>
	</tr>
	<tr>
	<td>Limitações do disco em nuvem</td>
	<td><ul class="params">
	<li>A criptografia de disco em nuvem é compatível com todos os tipos de discos em nuvem e tipos de instâncias.</li>
	<li>Só é possível criptografar os discos em nuvem, não os discos locais.</li>
	<li>Só é possível criptografar os discos de dados, não os discos do sistema.</li>
	<li>Não é possível converter diretamente um disco não criptografado existente em um disco criptografado.</li>
	<li>Não é possível converter um disco em nuvem criptografado em um disco em nuvem não criptografado.</li>
	</ul></td>
	</tr>
	<tr>
	<td>Limitações de snapshots e imagens</td>
	<td><ul class="params">
	<li>Não é possível converter diretamente um snapshot gerado por um disco não criptografado existente em um snapshot criptografado.</li>
  <li>Não é possível converter um snapshot criptografado em um snapshot não criptografado.</li>
	<li>Não é possível compartilhar uma imagem com um snapshot criptografado.</li>
	<li>Não é possível replicar o snapshot criptografado e as imagens criadas por ele entre regiões.</li>
	</ul></td>
	</tr>
	<tr>
	<td>Outras limitações</td>
	<td><ul class="params">
	<li>A funcionalidade de criptografia de disco em nuvem depende do KMS da mesma região. Se você não tiver outras solicitações de operação, não precisa realizar operações adicionais no console do KMS.</li>
	<li>Ao usar a funcionalidade de criptografia de disco em nuvem pela primeira vez, é preciso ativar o KMS conforme as instruções da página. Caso contrário, não será possível adquirir o disco em nuvem criptografado.</li>
	<li>É possível consultar a CMK criada especificamente pelo sistema para criptografia de disco em nuvem no console do KMS, mas não é possível especificar, excluir ou alterar a CMK.</li>
	</ul></td>
	</tr>
</table>







## Faturamento
A criptografia de disco em nuvem, a CMK e as leituras/gravações de dados de discos em nuvem não incorrem em custos adicionais. No entanto, quando você gerencia o disco em nuvem criptografado no console ou por uma API, o KMS é usado como uma API e sua operação de gerenciamento será contada como uma chamada do KMS nessa região. Você será faturado com base na quantidade de chamadas do KMS. Para obter detalhes, consulte a [Visão geral do faturamento do KMS](https://cloud.tencent.com/document/product/573/34388).

As operações de gerenciamento de um disco em nuvem criptografado incluem:
- Criar um disco em nuvem criptografado
- Montar um disco em nuvem
- Desmontar um disco em nuvem
- Criar um snapshot
- Reverter um snapshot
>Certifique-se de ter saldo suficiente na conta, caso contrário, a operação falhará.
>


## Criação de um disco em nuvem criptografado
É possível criar um disco em nuvem criptografado por meio destes três métodos:

### Criação de um disco em nuvem criptografado pelo console
1. Faça login no [Console do CBS](https://console.cloud.tencent.com/cvm/cbs), selecione uma região e clique em **Create (Criar)**.
2. Na caixa de diálogo **Purchase Data Disk (Adquirir disco de dados)**, selecione **Enable disk encryption (Habilitar a criptografia de disco)**.
>Se você estiver usando a criptografia de disco em nuvem nessa região pela primeira vez, primeiro autorize o Key Management Service.
>
3. Selecione a configuração do disco em nuvem com base em suas necessidades reais e clique em **Submit (Enviar)**.
4. Depois de adquirir o disco em nuvem, é possível visualizar os discos em nuvem criptografados que já foram criados na página [Lista de discos em nuvem](https://console.cloud.tencent.com/cvm/cbs).
O novo disco em nuvem criptografado está com o status **to be mounted (para ser montado)**. Consulte a [Montagem de discos de nuvem](https://intl.cloud.tencent.com/document/product/362/5745) para montar o disco em nuvem em uma instância do CVM na mesma zona de disponibilidade.

### Criação de um disco em nuvem criptografado de um snapshot
Consulte [Criação de discos em nuvem usando snapshots](https://cloud.tencent.com/document/product/362/5757). Ao selecionar um snapshot criptografado para criar um disco em nuvem, é possível criar um disco em nuvem que contenha dados relevantes e seja criptografado.

### Criação de um disco em nuvem criptografado por uma API
É possível criar um disco em nuvem criptografado usando a [API CreateDisks](https://cloud.tencent.com/document/product/362/16312) por estes dois métodos:
- Configure `Encrypt` como `true`.
- Especifique um `SnapshotId` para o snapshot criptografado.

## Alteração do status da criptografia de dados
Para alterar o status dos dados existentes no disco em nuvem de "não criptografado" para "criptografado", recomendamos que você execute o comando `rsync` no sistema Linux ou o comando `robocopy` no sistema Windows para copiar os dados do disco não criptografado para o novo disco criptografado.
Se for preciso alterar o status dos dados existentes no disco em nuvem de "criptografado" para "não criptografado", recomendamos que você execute os mesmos comandos para copiar os dados do disco criptografado para o novo disco não criptografado.


<style>
	.params{margin-bottom:0px !important;}
</style>





