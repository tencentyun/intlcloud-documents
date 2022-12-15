## 1\. CONSIDERAÇÕES INICIAIS
Este Módulo se aplica se você usar o Data Lake Compute (“Recurso”). Esse Módulo está incorporado ao Contrato de Segurança e Processamento de Dados localizado em:  (“[DPSA](https://intl.cloud.tencent.com/document/product/301/17347)”). Os termos utilizados, mas não definidos nesse Módulo, devem ter o significado dado a eles no DPSA. No caso de qualquer conflito entre o DPSA e esse Módulo, esse Módulo será aplicado conforme a inconsistência. 

## 2\. PROCESSAMENTO
Processaremos os seguintes dados em conexão com o Recurso:
<table>
<thead>
<tr>
<th><b>Informações Pessoais</b></th>
<th><b>Uso</b></th>
</tr>
</thead>
<tbody>
<tr>
<td><b>Dados de origem</b>: arquivos de dados (dados estruturados ou semiestruturados, como CVS, Avro, Parquet, ORC e json) que você carrega para este Recurso (se seus arquivos contiverem dados pessoais)</td>
<td>Apenas processamos esses dados com a finalidade de fornecer o Recurso a você.<br>Observe que esses dados estão integrados, armazenados e têm uma cópia de segurança em nosso recurso Cloud Object Storage.
<br>Note que não temos controle sobre os dados pessoais (caso existam) armazenados no banco de dados.</td>
</tr>
<tr>
<td><b>Dados de agendamento de tarefas</b>: número de identificação único, ID da tarefa e horário de funcionamento</td>
<td>Apenas processamos esses dados com o fim de fornecer o Recurso a você de acordo com a sua configuração, inclusive para permitir que você gerencie suas tarefas e execute tarefas recorrentes.</td>
</tr>
<tr>
<td><b>Dados de gerenciamento de acesso</b>: número de identificação único, ID da aplicação, informações do grupo de trabalho e informações de acesso</td>	
<td>Apenas processamos esses dados com o fim de fornecer-lhe o Recurso, inclusive para possibilitar que você gerencie autorizações de usuários.</td>
</tr>
<tr>
<td><b>Dados de registros de operações</b>: número de identificação único, ID da aplicação, ID da tarefa, horário de funcionamento e suas instruções (SQL, spark)</td>
<td>Apenas processamos esses dados com o fim de fornecer-lhe o Recurso, inclusive para registrar suas execuções de tarefas e as dos usuários autorizados, bem como registrar o status de execução das tarefas.</td>
</tr>
</tbody></table>

## 3\. REGIÃO DO SERVIÇO
Conforme especificado no DPSA.

## 4\. SUBPROCESSADORES
Como especificado no DPSA, incluindo Aceville Pte. Ltd.

## 5\. RETENÇÃO DE DADOS
Armazenaremos dados pessoais processados em conexão com o Recurso da seguinte forma:
<table>
<thead>
<tr>
<th><b>Informações Pessoais</b></th>
<th><b>Política de Retenção</b></th>
</tr>
</thead>
<tbody>
<tr>
<td>Dados de origem</td>
<td>Retemos esses dados até que você os exclua manualmente (a menos que você tenha uma taxa de serviço pendente de pagamento relacionado ao Recurso. Neste caso, excluiremos esses dados 120 dias após o vencimento, caso a taxa ainda não tenha sido paga). De outro modo, excluiremos esses dados no momento em que você  excluir sua conta.</td>
</tr>
<tr>
<td>Dados de agendamento de tarefas<br>Dados de registros de operações</td>
<td>Retemos esses dados por 45 dias (a menos que você solicite sua exclusão. Neste caso, realizaremos a exclusão em até 30 dias). </td>
</tr>
<tr>
<td>Dados de gerenciamento de acessos</td>	
<td>Retemos esses dados até que você os exclua manualmente. Caso contrário, ao excluir sua conta, excluiremos esses dados em até 30 dias.</td>
</tr>
</tbody></table>
Você pode solicitar a exclusão desses dados pessoais de acordo com o DPSA.

## 6\. CONDIÇÕES ESPECIAIS
Você deve garantir que esse Recurso seja usado somente por usuários finais com a idade mínima exigida para que possam consentir com o processamento de seus dados pessoais. Pode haver diferenças dependendo da jurisdição em que o usuário final está localizado.

Este Recurso não se destina ao processamento de dados confidenciais. Você deve assegurar que esse Recurso não seja utilizado para transferir ou processar quaisquer dados sensíveis por você ou seus usuários finais, incluindo (mas não limitado a) opiniões políticas, crenças religiosas ou filosóficas relacionadas a seus usuários finais, em que tal processamento poderia resultar em riscos de reputação para nossos negócios dentro e fora da jurisdição em que seus usuários finais estão localizados.

Você declara, garante e assume que deve obter e manter todos os consentimentos necessários dos envolvidos em relação aos respectivos processamentos dos dados pessoais (se aplicável), no que diz respeito ao Recurso (inclusive para os fins de fornecimento do Recurso), de acordo com as leis aplicáveis e de modo a nos permitir cumpri-las. Você concorda que indenizará e isentará de responsabilidade a Tencent sobre e contra todas as reclamações, responsabilidades, custos, despesas, perda ou danos (incluindo perdas consequenciais, perda de lucro e perda de reputação e todos os juros, multas e outros custos e despesas jurídicos e profissionais) incorridos à Tencent, decorrentes direta ou indiretamente de uma violação deste requerimento.
