## Cenários de operação
Este documento descreve como criar uma tabela no console do TcaplusDB.

## Pré-requisitos
- Você criou um [cluster](https://intl.cloud.tencent.com/document/product/1016/32714) e um [grupo de tabelas](https://intl.cloud.tencent.com/document/product/1016/32716) do TcaplusDB.
- Você preparou o arquivo da tabela de acordo com o [arquivo de descrição da tabela de exemplo](https://intl.cloud.tencent.com/document/product/1016/36560).

## Instruções
1. Faça login no [console do TcaplusDB](https://console.cloud.tencent.com/tcaplusdb/table), selecione **Table List (Lista de tabelas)** na barra lateral esquerda e clique em **Create Table (Criar tabela)**.
2. Configure a tabela na página de criação de tabelas.
 - **Cluster and Table Group (Cluster e grupo de tabelas)**: selecione o cluster e o grupo de tabelas em questão.
 - **Table File (Arquivo da tabela)**: você pode carregar um arquivo de definição de tabela de seu sistema de arquivos local, selecionar um previamente carregado ou misturar e combinar. No entanto, os nomes dos arquivos devem ser exclusivos. Para obter mais informações, consulte o arquivo de tabela do PB de exemplo [game_players.proto](
https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/game_players.proto).
 - **Remarks (Comentários)**: insira os comentários sobre a tabela.
   ![](https://main.qcloudimg.com/raw/5621a15042a9d73b4364fe19b9a9268b.png)
3. Clique em **Next (Avançar)** e o sistema verificará o arquivo de definição de tabela selecionado.
 - Se a verificação falhar, um erro será gerado e você deverá modificar o arquivo de acordo e carregá-lo novamente.
 - Se a verificação for bem-sucedida, os metadados da tabela definidos no arquivo serão exibidos e você poderá prosseguir para a próxima etapa.
4. Na página de configuração da tabela, selecione a tabela a ser criada e insira a capacidade e os parâmetros reservados de leitura e gravação. As taxas diárias da tabela serão calculadas automaticamente.
![](https://main.qcloudimg.com/raw/32aa5c8a292df17249a62e88b6fca4e6.png)
5. Após confirmar que as informações da tabela estão corretas, clique em **Create (Criar)** e o sistema avisará que a criação foi bem-sucedida.
![](https://main.qcloudimg.com/raw/7a39640da609a65df7040fc9c1d7be3d.png)
