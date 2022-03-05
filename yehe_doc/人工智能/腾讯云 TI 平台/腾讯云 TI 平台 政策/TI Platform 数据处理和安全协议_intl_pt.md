## 1.CONSIDERAÇÕES
Este Módulo se aplica se você usa TI Platform (“Recurso”). Este Módulo está incorporado ao contrato de privacidade e segurança de dados localizado em  (“[DPSA](https://intl.cloud.tencent.com/document/product/301/17347)”). Os termos utilizados, mas não definidos neste módulo, devem ter o significado dado a eles no DPSA. No caso de qualquer conflito entre o DPSA e este módulo, este módulo se aplicará conforme a inconsistência.

## 2.PROCESSAMENTO
Processaremos os seguintes dados em conexão com o recurso:

<table>
<thead>
<tr>
<th><b>Informações pessoais</b></th>
<th><b>Uso</b></th>
</tr>
</thead>
<tbody>
<tr>
<td><b>Dados de registro de treinamento</b> (Registros durante o treinamento de algoritmos).</td>
<td rowspan="2">Apenas processamos estes dados com a finalidade de fornecer o Recurso para você. 
Observe que esses dados estão integrados com nossos recursos de Cloud Block Storage (CBS), TDSQL para MySQL (TDSQL), Message Queue CKafka (CKafka) e Elasticsesarch Service (ES) para este fim. Esses dados também estão integrados com, armazenados e têm uma cópia de segurança em seu espaço de armazenamento comprado em nosso recurso COS (Cloud Object Storage, armazenamento de objetos em nuvem).    
</td>
</tr>
<tr>
<td><b>Dados de registro de inferência</b> (Registros no processo de execução após o algoritmo ficar on-line)</td>
</tr>
<tr>
<td><b>Dados de configuração de tarefas de treinamento</b> (Parâmetros para a tarefa de treinamento de algoritmos)</td>
<td rowspan="2">Apenas processamos estes dados com a finalidade de fornecer o Recurso para você. 
Observe que esses dados estão integrados com nossos recursos TDSQL, CKafka e ES para este fim. 
</td>
</tr>
<tr>
<td><b>Dados de configuração de serviços de inferência</b> (Parâmetros para a tarefa de treinamento de algoritmos on-line)</td>
</tr>
<tr>
<td><b>Dados de anotação do usuário</b> [Rótulos para dados anotados pelo usuário (a partir dos recursos da plataforma)]</td>
<td>Apenas processamos estes dados com a finalidade de fornecer o Recurso para você. 
Observe que esses dados estão integrados com nossos recursos TDSQL, CKafka e ES para este fim. Esses dados também estão integrados com, armazenados e têm uma cópia de segurança em nosso recurso COS. 
</td>
</tr>
<tr>
<td><b>Dados do modelo de treinamento</b> (Arquivo modelo gerado após o treinamento do algoritmo)</td>
<td>Apenas processamos estes dados com a finalidade de fornecer o Recurso para você. 
Observe que esses dados estão integrados com nossos recursos TDSQL, CKafka e ES para este fim. Esses dados também estão integrados com, armazenados e têm uma cópia de segurança em seu espaço de armazenamento comprado em nosso recurso COS.
</td>
</tbody></table>

## 3.REGIÃO DO SERVIÇO
Conforme especificado no DPSA.
## 4.SUBPROCESSADORES
Conforme especificado no DPSA.
## 5.RETENÇÃO DE DADOS
Armazenaremos dados pessoais processados em conexão com o Recurso da seguinte forma:

<table>
<thead>
<tr>
<th><b>Informações pessoais</b></th>
<th><b>Política de Retenção</b></th>
</tr>
</thead>
<tbody>
<tr>
<td><b>Dados de registro de treinamento </b></td>
<td>Retemos esses dados por 7 dias. Você também pode optar por aumentar o período de retenção fornecendo serviços do nosso recurso CLS (Cloud Log Service, serviço de registro de nuvem).</td>
</tr>
<tr>
<td><b>Dados de registro de inferência</b></td>
<td>Retemos esses dados por 7 dias. Você também pode optar por aumentar o período de retenção adquirindo serviços do nosso recurso CLS.</td>
</tr>
<tr>
<td><b>Dados de configuração de tarefas de treinamento</b></td>
<td>Retemos tais dados de acordo com o seu limite de tempo de retenção de dados escolhido ou até você excluir tais dados ou o notebook manualmente. Caso contrário, quando você excluir sua conta ou encerrar o seu uso do Recurso, nós vamos excluir esses dados após 7 dias.</td>
</tr>
<tr>
<td><b>Dados de configuração do serviço de inferência  </b></td>
<td>Retemos tais dados de acordo com o seu limite de tempo de retenção de dados escolhido ou até você excluir tais dados ou o notebook manualmente. Caso contrário, quando você excluir sua conta ou encerrar o seu uso do Recurso, nós vamos excluir esses dados após 7 dias.</td>
</tr>
<tr>
<td><b>Dados de anotação do usuário</b></td>
<td>Esses dados não são armazenados.</td>
</tr>
<tr>
<td><b>Dados do modelo de treinamento</b></td>
<td>Esses dados não são armazenados.</td>
</tbody></table>





Você pode solicitar a exclusão desses dados pessoais de acordo com o DPSA.
## 6.CONDIÇÕES ESPECIAIS
Você deve garantir que este recurso seja usado somente por usuários finais com a idade mínima exigida para que possam consentir com o processamento de seus dados pessoais. Pode haver diferenças dependendo da jurisdição em que o usuário final está localizado.
