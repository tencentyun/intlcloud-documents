## Relação entre um snapshot e o disco em nuvem de origem
Um snapshot é o backup de dados de um disco em nuvem em um determinado momento. A gravação e a modificação de dados no disco em nuvem não afetam os snapshots já criados. Com essa funcionalidade, os usuários podem usar snapshots para registrar dados do disco em nuvem em diferentes momentos, que podem ser usados para atender aos requisitos de recuperação do sistema, recuperação de desastres e replicação de discos em nuvem.
Conforme mostrado na figura a seguir, o Snapshot 1 retém as informações do bloco de dados do disco em nuvem às 10h (hora de criação do snapshot), independentemente de alterações no disco que ocorram após a criação desse snapshot.
![](https://main.qcloudimg.com/raw/1f7e576a6ea9e4f85273b0b147108c9b.png)

## Relação entre o tamanho do snapshot e o disco em nuvem de origem
O snapshot salva apenas blocos de dados no disco em nuvem que foram gravados ou modificados. Portanto, o tamanho do snapshot correspondente ao disco em nuvem será menor do que o tamanho do disco em nuvem.
A relação entre o tamanho do snapshot e o disco de dados é mostrada na figura a seguir:
![](https://main.qcloudimg.com/raw/00913478170abba28952aa9c8dc13c82.png)

## Processo de criação de snapshots incrementais 
Os snapshots do Tencent Cloud usam um mecanismo de snapshot incremental. Quando você cria continuamente vários snapshots do mesmo disco em nuvem, apenas o primeiro snapshot é um snapshot completo e os snapshots subsequentes contêm apenas os dados que foram modificados em relação ao snapshot anterior (snapshot incremental). Isso pode minimizar a capacidade total de armazenamento ocupada quando os usuários criam snapshots continuamente, reduzindo os custos para o usuário.
Por exemplo: Suponha que um disco em nuvem tenha três blocos de dados, A, B e C. Você cria snapshots às 10h, 11h e 12h, respectivamente. As alterações de blocos de dados no disco entre esses pontos no tempo são mostradas na figura a seguir, e cada snapshot deve salvar os seguintes dados:
- Snapshot 1 (snapshot inicial): contém backups de dados de todos os blocos de dados no disco em nuvem naquele momento.
- Snapshot 2: durante o período, o bloco de dados A no disco em nuvem muda. O Snapshot 2 contém apenas o backup dos dados mais recentes do bloco A (normalmente chamado de snapshot incremental).
- Snapshot 3: durante o período, o bloco de dados B no disco em nuvem muda. O Snapshot 3 contém apenas o backup dos dados mais recentes do bloco B (normalmente chamado de snapshot incremental).

![](https://main.qcloudimg.com/raw/bcdf30c658a08ef47196f8127608423b.png)

## Processo de reversão de snapshots incrementais 
Com base no exemplo anterior, quando você usa o Snapshot 3 para executar a reversão de dados, o sistema mesclará os dados no Snapshot 1, Snapshot 2 e Snapshot 3. Se houver um bloco de dados no mesmo local, os dados do snapshot mais recente serão obtidos. Durante a reversão final, os dados mesclados serão gravados no disco em nuvem para serem revertidos.
O processo de reversão de snapshot incremental é mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/745e412b2dfa84ea6ba5e8e0fc720fc8.png)

## Processos de exclusão e mesclagem de snapshots incrementais
- Ao excluir um snapshot completo (ou seja, o primeiro snapshot), o sistema mescla automaticamente o snapshot completo com o próximo snapshot incremental.
- Ao excluir um snapshot incremental, o sistema mescla automaticamente o snapshot incremental com o próximo snapshot incremental. Se não houver um próximo snapshot incremental, ele será excluído diretamente.

Com base no exemplo anterior, se você excluir o Snapshot 1, o sistema mesclará o Snapshot 1 e o Snapshot 2 e usará os dados do Snapshot 2 para substituir os dados do Snapshot 1 no mesmo local. Após a mesclagem, o Snapshot 2 é o novo snapshot completo.
O processo de exclusão de snapshot incremental é mostrado na figura a seguir:
![](https://qcloudimg.tencent-cloud.cn/raw/2f2bb2449450a52df265537da14768b5.png)
