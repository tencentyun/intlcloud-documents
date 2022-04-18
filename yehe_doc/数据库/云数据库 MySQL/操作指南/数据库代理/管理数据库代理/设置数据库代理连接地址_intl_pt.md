
Este documento descreve como definir o endereço de acesso do proxy do banco de dados no console do TencentDB for MySQL.

O endereço de acesso do proxy do banco de dados é independente do endereço de acesso do banco de dados original. As solicitações com proxy efetuado no endereço de proxy são todas retransmitidas por meio do cluster de proxy para acessar os nós de origem e de réplica do banco de dados. A separação de leitura/gravação é implementada, para que as solicitações de leitura sejam encaminhadas para instâncias somente leitura, o que reduz a carga do banco de dados de origem.

## Pré-requisitos
Ter [ativado o proxy de banco de dados](https://intl.cloud.tencent.com/document/product/236/42052).

## Instruções
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, selecione a instância de origem para a qual deseja habilitar o proxy de banco de dados e clique no respectivo ID ou em **Manage (Gerenciar)**, na coluna **Operation (Operação)**, para entrar na página de gerenciamento de instância.
2. Na página de gerenciamento de instância, selecione a guia **Database Proxy (Proxy de banco de dados)** e clique no ícone <img src="https://main.qcloudimg.com/raw/be716b5360d5256a9d5e816e29872ec1.png"  style="margin:0;"> ao lado de **Connection Address (Endereço de conexão)**. 
![](https://main.qcloudimg.com/raw/63015c402bdd31e04e2597af84013a74.png)
<table>
<thead><tr><th width=15%>Descrição do</th><th>termo</th></tr></thead>
<tbody><tr>
<td>Endereço de proxy do banco de dados</td>
<td>É independente do endereço de acesso ao banco de dados original. As solicitações com proxy efetuado são todas retransmitidas por meio do cluster de proxy para acessar a origem e os nós de réplica do banco de dados. Pode ser editado.</td></tr>
<tr>
<td>Tipo de rede</td>
<td>Você pode alternar o tipo de rede da instância entre rede clássica e VPC de acordo com suas necessidades de negócios. <ul><li>Na rede clássica, as instâncias não podem ser isoladas pela rede, mas dependem de suas próprias políticas de lista de permissões para bloquear o acesso não autorizado. </li><li>Uma VPC é um ambiente de rede isolado e tem um nível de segurança mais alto.</li></ul></td></tr>
<tr>
<td>Observações</td>
<td>É uma breve descrição do endereço do proxy do banco de dados para facilitar o gerenciamento.</td></tr>
</tbody></table>
3. Na janela pop-up, modifique o endereço do proxy e clique em **OK**.
>!Modificar o endereço de proxy afeta os negócios do banco de dados que está sendo acessado. Recomendamos modificar o endereço fora do horário de pico. Certifique-se de que sua empresa tenha um mecanismo de reconexão.
>
![](https://main.qcloudimg.com/raw/982fd53d880ab1a6d4f8df0372a99613.png)
