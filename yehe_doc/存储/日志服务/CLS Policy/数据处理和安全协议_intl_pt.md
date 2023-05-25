

## 1\. Considerações

Este Módulo se aplica se você usar o Cloud Log Service (“**Recurso**”). Este Módulo está incorporado ao Contrato de Processamento de Dados e Segurança localizado em [ (“**DPSA**”)](https://intl.cloud.tencent.com/document/product/301/17347). Os termos utilizados, mas não definidos nesse Módulo, devem ter o significado dado a eles no DPSA. No caso de qualquer conflito entre o DPSA e esse Módulo, esse Módulo será aplicado conforme a inconsistência.

## 2\. PROCESSAMENTO

Processaremos os seguintes dados em conexão com o Recurso:

| **Informações pessoais**                                     | **Uso**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Dados comerciais,** ou seja, seus registros de nuvem que você carrega para o Recurso por meio da ferramenta de coletor de registro dedicada “loglistener”. | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você.<br/>Observe que esses dados são salvos, armazenados em backup e gerenciados no Cloud Object Storage, Ckafka/ES e CK, que estão localizados na região de serviço do Recurso selecionado por você. |
| **Dados de configuração,** inclusive em relação a:<li>coleta de registros (ou seja, o endereço IP da máquina virtual na nuvem, o diretório de registro, a hora do registro e a política de filtro;</li><li>painel e índice: campos definidos pelo usuário que são usados para criar Índice e Painéis; e</li><li> alertas (nomeadamente a política de alerta e o período). </li> | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você.<br/>Observe que esses dados são armazenados e copiados em COS/Ckafka/ES, que estão localizados na região de serviço do Recurso selecionado por você. |



## 3\. região de serviço

Conforme especificado no DPSA.

## 4\. subprocessadores

Conforme especificado no DPSA.

## 5\. retenção de dados

Armazenaremos dados pessoais processados em conexão com o Recurso da seguinte forma:

| **Informações pessoais** | **Política de retenção**                                         |
| ------------------------ | ------------------------------------------------------------ |
| Dados comerciais            | Retemos esses dados até que você os exclua manualmente. Caso contrário, excluiremos esses dados dentro de 7 dias após você deixar de usar este Recurso ou excluir sua conta. |
| Dados de configuração       | Retemos esses dados após um período de retenção de dados definido pelo usuário (1 a 366 dias). Após o término do período definido, os dados serão excluídos automaticamente. |

Você pode solicitar a exclusão desses dados pessoais de acordo com o DPSA.