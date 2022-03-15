## 1.CONSIDERAÇÕES
Esse módulo se aplica se você utiliza IoT Hub ("**Recurso**"). Este Módulo é incorporado ao contrato de segurança e privacidade de dados localizado no  (“**[DPSA](https://intl.cloud.tencent.com/document/product/301/17347)**"). Os termos utilizados, mas não definidos neste módulo, devem ter o significado dado a eles no DPSA. No caso de qualquer conflito entre o DPSA e este Módulo, este Módulo se aplicará conforme a inconsistência.

## 2.PROCESSAMENTO
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
<td><b>Dados de registro</b>: registro do dispositivo (se você habilitar a coleta desses dados) </td>
<td>Nós só processamos esses dados de acordo com sua configuração para facilitar a depuração ou solução de problemas por você.
Observe que estes dados são armazenados e têm uma cópia de segurança em nosso recurso Elasticsearch Service. Além disso, você também pode usar nosso recurso Cloud Log Dump para armazenar e analisar os dados.
</td>
</tr>
<tr>
<td><b>Dados de configuração</b>: configurações de produtos (nome do produto, ID do produto), dispositivos (nome do dispositivo, chave/certificado do dispositivo) e regras (instrução SQL)</td>
<td>Nós só processamos esses dados para facilitar a identificação e o gerenciamento de produtos e/ou dispositivos por você.
Note que esses dados estão armazenados e tem uma cópia de segurança em nosso recurso TencentDB for MySQL.
</td>
</tr>
<tr>
<td><b>Dados de monitoramento</b>: estatísticas de dispositivos on-line, mensagens de dispositivo, sombras de dispositivos, mecanismo de regras e firmware</td>
<td>Nós apenas processamos esses dados para fornecer-lhe estatísticas do seu uso do Recurso.
Observe que esses dados são armazenados e gerenciados pelo nosso recurso Cloud Monitor. Observe que esses dados têm uma cópia de segurança em nosso recurso TencentDB for MySQL.
</td>
</tr>
<tr>
<td><b>Dados de recursos</b>: recursos relacionados a plataformas e dispositivos carregados por você (se você incluir dados pessoais em tais recursos)</td>
<td>Nós apenas processamos esses dados para permitir que você forneça esses dados para seus usuários finais.
Observe que esses dados estão armazenados e têm uma cópia de segurança em nosso recurso Cloud Object Storage.
</td>
</tr>
<tr>
<td><b>Dados do dispositivo publicados</b>: tipo de dispositivo, estado do dispositivo, regras e comandos para controlar o dispositivo por instrução SQL</td>
<td>Nós só processamos esses dados para verificação de dispositivos e encaminhamento de mensagens conforme instruído por você.
Observe que não temos acesso a essas informações. Esses dados são transferidos para outro(s) serviço(s), conforme instruído por você.
</td>
</tr>
<tr>
<td><b>Dados do dispositivo do assinante</b>: mensagem de comando do dispositivo </td>
<td>Nós só processamos esses dados para facilitar o controle do(s) dispositivo(s) pelos seus usuários finais.
Observe que não temos acesso a essas informações. Esses dados são transferidos para outro(s) serviço(s), conforme instruído por você. 
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
<th><b>Informações Pessoais</b></th>
<th><b>Política de Retenção</b></th>
</tr>
</thead>
<tbody>
<tr>
<td><b>Dados de registro</b></td>
<td>Armazenado por 7 dias com nosso recurso Elasticsearch Service.
Além disso, você também pode armazenar os dados com o nosso recurso Cloud Log Dump por um período determinado por você.</td>
</tr>
<tr>
<td><b>Dados de configuração</b></td>
<td>Armazenado até que você solicite a exclusão, mediante a qual esses dados serão excluídos dentro de 30 dias. Quando você não solicitar a exclusão, esses dados serão excluídos no prazo de 30 dias a partir da data anterior da data em que os valores em atraso estarão disponíveis para pagamento em sua conta, rescisão do uso deste Recurso ou exclusão deste Recurso.</td>
</tr>
<tr>
<td><b>Dados de recursos</b></td>
<td>Armazenado até que você solicite a exclusão, mediante a qual esses dados serão excluídos dentro de 30 dias. Quando você não solicitar a exclusão, esses dados serão excluídos no prazo de 30 dias a partir da data anterior da data em que os valores em atraso estarão disponíveis para pagamento em sua conta, rescisão do uso deste Recurso, expiração da sua inscrição no Recurso ou exclusão deste Recurso.</td>
</tr>
<tr>
<td><b>Dados de monitoramento</b></td>
<td>Armazenados por 7 dias.</td>
</tr>
<tr>
<td><b>Dados do dispositivo publicados</b></td>
<td>Não armazenado.</td>
</tr>
<tr>
<td><b>Dados do dispositivo de assinante</b></td>
<td>Não armazenado.</td>
</tbody></table>

Você pode solicitar a exclusão desses dados pessoais de acordo com o DPSA.

## 6.CONDIÇÕES ESPECIAIS
Você deve garantir que este Recurso seja usado somente por usuários finais com a idade mínima exigida para que possam consentir com o processamento de seus dados pessoais. Pode haver diferenças dependendo da jurisdição em que o usuário final está localizado.
