## Visão geral
Uma consulta de instrução SQL que leva mais tempo do que o valor especificado é chamada de “consulta lenta”, e a instrução correspondente é chamada de “instrução de consulta lenta”. O processo em que um administrador de banco de dados (DBA, na sigla em inglês) analisa instruções de consulta lenta e descobre as razões pelas quais elas ocorrem é conhecido como “análise de consulta lenta”.

Você pode exibir os detalhes de logs lentos, detalhes de logs de erros e logs de reversão de uma instância, e baixar os logs lentos na página de log de operação no console. Você também pode exibir e baixar os logs de banco de dados por meio da interface de linha de comando (CLI, na sigla em inglês) ou das APIs do TencentDB. Para mais informações, consulte [DescribeSlowLogs](https://intl.cloud.tencent.com/document/product/236/15845) e [DescribeBinlogs](https://intl.cloud.tencent.com/document/product/236/15843).

>?As instâncias do TencentDB for MySQL (excluindo as instâncias de nó único básico) permitem o gerenciamento de log de operação.
>

#### Observações sobre consultas lentas no MySQL
- long_query_time: parâmetro de limite de consulta lenta com precisão de microssegundos. O valor padrão é 10 segundos. Quando uma instrução SQL leva mais tempo do que o limite para ser executada, ela será registrada em um log lento. 
Quando o parâmetro `long_query_time` for ajustado, os logs lentos existentes não serão afetados. Por exemplo, se o parâmetro de limite de log lento for 10 segundos, os registros de log lento que excederem 10 segundos serão relatados. Após esse valor for modificado para 1 segundo, os logs relatados anteriormente ainda serão mantidos.
- log_queries_not_using_indexes: se as consultas não indexadas devem ser registradas em log. O valor padrão é OFF (Desativado).


## Instruções
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, clique no ID de uma instância ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para acessar a sua página de gerenciamento.
2. Na guia **Operation Log (Log de operação)**, você pode exibir os detalhes dos logs lentos, os detalhes dos logs de erros e os logs de reversão da instância, e baixar os logs lentos.
<table>
<thead><tr><th>Funcionalidade</th><th>Descrição</th></tr></thead>
<tbody><tr>
<td>Detalhes dos logs lentos</td><td>Registra instruções SQL que levaram mais de 10 segundos para serem executadas no banco de dados no último mês</td></tr>
<tr>
<td>Download de logs lentos</td><td>Baixa logs lentos</td></tr>
<tr>
<td>Detalhes dos logs de erros</td><td>Registra as informações detalhadas de cada inicialização e desligamento, assim como todos os avisos e erros graves durante a operação</td></tr>
<tr>
<td>Reversão de logs</td><td>Registra o status e o progresso das tarefas de reversão</td></tr>
</tbody></table>
<img src="https://main.qcloudimg.com/raw/c229d0fe6a4869998d3472b0a35efa28.png"  style="margin:0;">
3. Para baixar o log lento, na guia **Download Slow Log (Baixar log lento)**, clique em **Download (Baixar)** na coluna **Operation (Operação)**.
4. Copie o endereço de download na caixa de diálogo pop-up, [faça login na CVM do Linux na mesma VPC que a instância do TencentDB](https://intl.cloud.tencent.com/document/product/213/10517) e execute `wget` para baixar o arquivo pela rede privada de alta velocidade.
>?
>- Os logs com tamanho de 0 KB não podem ser baixados.
>- Você também pode clicar em **Download (Baixar)** para baixá-lo diretamente. No entanto, isso pode levar mais tempo.
>- `wget` command format: wget -c 'log file download address' -O custom filename.log
>
Exemplo:
```
wget -c 'http://szx.dl.cdb.tencentyun.com:303/cfdee?appid=1210&time=1591&sign=aIGM%3D' -O test.log
```
