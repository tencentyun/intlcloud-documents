

### Discos em nuvem elásticos

Um disco em nuvem elástico tem um ciclo de vida útil independente (ciclo de faturamento) e pode ser montado e desmontado entre instâncias diferentes do CVM na mesma região e zona de disponibilidade. Entretanto, ele não pode ser montado simultaneamente em vários CVMs.



### Discos em nuvem não elásticos

Um disco em nuvem não elástico é criado junto com um Cloud Virtual Machine (CVM) e tem o mesmo ciclo de vida útil que o CVM. Ele não é compatível com a montagem elástica.



### GPT

Consulte [GPT](https://www.tencentcloud.com/pt/document/product/362/18555#gpt2).



### Reversão

Uma reversão restaura um programa ou os dados de volta para o último status correto quando ocorre um erro de processamento. Há dois tipos: reversão de programa e reversão de dados.



### IOPS

Entrada/Saída por segundo (IOPS) se refere à quantidade de leituras (saídas) e gravações (entradas) em um segundo. É uma métrica importante para medir o desempenho do disco. O IOPS indica a quantidade de solicitações de E/S que o sistema pode processar em uma unidade de tempo (por segundo). As solicitações de E/S são geralmente solicitações de leitura ou gravação de dados.
Os discos tradicionais são basicamente dispositivos mecânicos, como discos FC, SAS e SATA, cujas taxas de rotação são geralmente de 5.400/7.200/10.000/15.000 rpm. O principal fator que afeta um disco é o tempo de serviço do disco, ou seja, o tempo que leva para o disco concluir uma solicitação de E/S. Ele é composto de tempo de busca, atraso rotacional e tempo de transferência de dados.
No geral, um único HDD com 7.200 rpm fornece 75 a 150 IOPS, e um único HDD com 15.000 rpm fornece 175 a 210 IOPS. O valor real depende de fatores como modo de acesso (sequencial ou aleatório) e tamanho da E/S.



### Cadeia de snapshots

A cadeia de snapshots é uma cadeia de relação composta por todos os snapshots do mesmo disco, em que cada nó representa um snapshot do disco.



### MBR

Consulte [MBR](https://www.tencentcloud.com/document/product/362/18555#mbr2)



### GPT

GUID Partition Table (GPT) é o layout de partição de um disco físico. É uma parte do padrão de Interface de Firmware Extensível (EFI, na sigla em inglês) e é um substituto da tabela de partição MBR usada pela maioria dos discos.

### Snapshot completo

Um snapshot completo é o primeiro snapshot criado para um disco que salva todos os dados do disco.



### E/S sequencial

E/S sequencial significa que blocos lógicos são lidos e gravados sequencialmente a partir de endereços adjacentes. No acesso de E/S sequencial, o tempo de busca de um disco é muito reduzido, porque os cabeçotes de leitura-gravação quase nem precisam se mover ao acessar o bloco seguinte. Serviços como backup de dados e login são E/S sequenciais.

### E/S aleatória

E/S aleatória significa que os endereços de acesso não são sequenciais, mas sim distribuídos de forma aleatória em várias partes do disco. Serviços como OLTP, SQL e mensagens instantâneas são E/S aleatória.



### Distribuição de dados

A distribuição de dados (striping) é um método de equilibrar automaticamente as cargas de E/S em vários discos físicos.

### Taxa de transferência

A taxa de transferência é a quantidade de dados transferidos com êxito em uma determinada unidade de tempo ao longo de uma rede, um dispositivo, uma porta, um circuito virtual ou outros dispositivos.



### Snapshots de disco em nuvem

Um snapshot é usado para salvar uma cópia do disco em nuvem em determinado ponto temporal. Você pode usá-lo para restaurar o disco em nuvem de volta ao ponto temporal quando o snapshot foi criado.



### Snapshot incremental

Um snapshot incremental é um backup de determinado ponto temporal composto apenas por todas as alterações realizadas desde o snapshot completo ou desde o snapshot incremental anterior.

### MBR

Master Boot Record (MBR) é o primeiro setor que o computador precisa ler ao acessar o disco após a inicialização. O MBR registra informações sobre o disco e o tamanho e a localização de cada partição do disco. Também é uma entrada importante de informações de dados.
