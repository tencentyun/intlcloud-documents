O TencentDB for MySQL permite o ajuste rápido da especificação da instância, além de operações de dimensionamento flexíveis no console. Você pode ajustar elasticamente as especificações das instâncias do MySQL de acordo com suas condições reais de operações (no estágio inicial, no estágio de desenvolvimento rápido, durante os horários de pico ou fora dos horários de pico), para atender melhor às suas necessidades, como a utilização total de recursos e a otimização de custos em tempo real. Para obter detalhes sobre as taxas de ajuste de instância, consulte [Taxa de ajuste de instância](https://intl.cloud.tencent.com/document/product/236/32345).

## Descrição do espaço em disco da instância
- Para garantir a continuidade das operações, faça o upgrade das especificações de sua instância ou adquira capacidade de disco adicional antes que a capacidade seja totalmente usada.
>?Você pode exibir o espaço em disco na página de detalhes da instância no [Console do MySQL](https://console.cloud.tencent.com/cdb) ou receber alarmes sobre o disco de acordo com as [Políticas de alarme (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457).
- Quando o tamanho dos dados armazenados em uma instância exceder seu limite de capacidade, ela será bloqueada e se tornará somente leitura. Você não poderá gravar dados nela. Será necessário expandir sua capacidade ou excluir algumas tabelas de banco de dados no console para desbloqueá-la.
- Para evitar que o banco de dados acione o status de bloqueio repetidamente, uma instância bloqueada será desbloqueada e permitida para leituras e gravações apenas quando sua capacidade livre disponível corresponder a mais de 20% de sua capacidade total ou mais de 50 GB.

## Detalhes do ajuste de configuração
Por padrão, a configuração da instância é ajustada no modo normal, o que requer uma migração de dados para que o ajuste seja concluído após você ajustar a configuração da instância no console. Mas se a máquina física em que a instância está localizada tiver recursos restantes suficientes (também conhecidos como recursos locais), você poderá escolher o modo QuickChange (Alteração rápida). O processo de ajuste é o seguinte:
![](https://qcloudimg.tencent-cloud.cn/raw/8e7702c81886573a459dbf73b2846701.png)

- **Normal mode (Modo normal)**: para ajustar a configuração da instância, os dados dela precisam ser migrados da máquina física original para uma nova. Como o ajuste nesse modo requer migração, comparação e verificação de dados, o processo geral de ajuste levará muito tempo em casos de uma grande quantidade de dados. Além disso, uma alternância de instância pode ocorrer após a conclusão do ajuste.
- **QuickChange mode (Modo de alteração rápida)**: a configuração da instância pode ser ajustada sem migrar dados ou alternar para outra máquina física. Como não é necessária nenhuma preparação para a migração, o processo geral de ajuste é muito mais rápido.
>!
>- Se os recursos locais forem suficientes e atenderem às condições do modo QuickChange (Alteração rápida), esse modo será usado por padrão. Se você não precisar usá-lo, poderá desativá-lo alternando-o na página de ajuste de configuração.
>- No modo QuickChange (Alteração rápida), a instância pode ser reiniciada e ficar indisponível por um curto período durante o ajuste da configuração.

## Observações
- Uma instância somente leitura com um VIP exclusivo ativado não aceita o QuickChange (Alteração rápida).
- Se um grupo de instâncias somente leitura (grupo RO) tiver a funcionalidade “Remove Delayed RO Instances (Remover instâncias RO atrasadas)” ativada, as instâncias somente leitura cujo atraso exceder o limite especificado serão removidas do grupo RO até que a quantidade de instâncias restantes atinja a quantidade mínima permitida. Se a quantidade de instâncias somente leitura disponíveis restantes em um grupo RO for menor ou igual à quantidade mínima permitida, nenhuma dessas instâncias aceitará o QuickChange (Alteração rápida).
- Se um grupo RO tiver apenas uma instância somente leitura, ela não aceitará o QuickChange (Alteração rápida).

## [Regras de ajuste de configuração](id:guize)
- Você pode ajustar a configuração de uma instância do TencentDB for MySQL e suas instâncias somente leitura e recuperação de desastres associadas somente quando estiverem com o status normal (em execução) e não estiverem executando nenhuma tarefa.
- Não é possível cancelar uma operação de ajuste de configuração em andamento.
- O nome, o IP de acesso e a porta de acesso da instância permanecem inalterados após o ajuste da configuração.
- Durante o ajuste de configuração, você deve evitar operações como modificar os parâmetros globais do MySQL e a senha do usuário.
- A migração de dados pode estar envolvida no ajuste de configuração. Durante a migração de dados, a instância do TencentDB for MySQL poderá ser acessada normalmente e as operações não serão afetadas.
- Pode ser necessária a alternância de instância após a conclusão do ajuste de configuração (ou seja, a instância do MySQL pode ser desconectada por segundos). Recomendamos que as aplicações sejam configuradas com a funcionalidade de reconexão automática e que a alternância de instância seja realizada durante o período de manutenção dela. Para mais informações, consulte [Configuração do período de manutenção da instância](https://intl.cloud.tencent.com/document/product/236/10929).
- As instâncias de nó único básico do TencentDB for MySQL ficam indisponíveis por cerca de 15 minutos no processo de ajuste de configuração. Recomendamos que você ajuste a configuração da instância fora dos horários de pico.

## Ajuste da configuração da instância no console
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), localize a instância desejada na lista de instâncias e selecione **More (Mais)** > **Adjust Configurations (Ajustar configurações)** na coluna **Operation (Operação)**.
2. Na janela pop-up, selecione a configuração desejada e clique em **Submit (Enviar)**.
>?
>- Quando os recursos locais forem suficientes, você poderá ativar o modo QuickChange (Alteração rápida) alternando o botão **QuickChange (Alteração rápida)** na página de ajuste de configuração no console.
>![](https://main.qcloudimg.com/raw/c37bb99f0a2db0a9108c7068ad72ba7c.png)
>- Em alguns casos, a reinicialização da instância não será necessária no modo QuickChange (Alteração rápida) e o ajuste de configuração entrará em vigor imediatamente após o envio da solicitação, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/6f5e9ab54f270c0833f5545cccbc8c6d.png)
>
![](https://main.qcloudimg.com/raw/ef2bf519dabe88cb23b9c73993602b9b.png)

## Ajuste da configuração da instância por meio de API
Você pode ajustar a configuração da instância usando a API `UpgradeDBInstance`. Para mais informações, consulte [UpgradeDBInstance](https://intl.cloud.tencent.com/document/product/236/15876).

## Perguntas frequentes
#### O ajuste de configuração da instância afetará as instâncias?
- No processo de ajuste de configuração do TencentDB for MySQL, pode ocorrer migração de dados, e as instâncias ainda podem ser acessadas durante o processo. Após a conclusão da migração, há uma alternância que causa uma desconexão rápida com duração de apenas alguns segundos, garanta que suas operações tenham um mecanismo de reconexão.
- As instâncias de nó único básico do TencentDB for MySQL ficam indisponíveis por cerca de 15 minutos no processo de ajuste de configuração. Recomendamos que você ajuste a configuração da instância fora dos horários de pico.

#### Por que não é possível fazer o downgrade da minha instância?
Pode ser porque a capacidade de armazenamento utilizada atingiu a capacidade máxima do disco rígido. Para fazer o downgrade de sua instância, primeiro 1você precisa limpar os dados e verificar se a capacidade restante disponível representa mais de 20% da capacidade total ou mais de 50 GB.

#### Por que minha instância está com o status “Waiting for switch (Aguardando a alternância)” por muito tempo após ajustar a configuração da instância no console?
Pode ser porque você selecionou **During maintenance time (Durante o tempo de manutenção)** como **Switch Time (Hora da alternância)** ao ajustar a configuração da instância no [console](https://console.cloud.tencent.com/cdb), de modo que a instância não será alternada imediatamente após o ajuste.
Para alternar imediatamente, você pode localizar a instância desejada na lista de instâncias e clicar em **Switch Now (Alternar agora)** na coluna **Operation (Operação)**. A alternância causa uma desconexão rápida que dura apenas alguns segundos. Certifique-se de que suas operações tenham um mecanismo de reconexão.

#### Quanto tempo leva para fazer upgrade da configuração da instância?
O tempo que leva depende do volume de dados da instância e das solicitações de leitura para replicar os dados.
As instâncias ainda podem ser acessadas durante o upgrade, mas uma alternância de VIP causa uma desconexão rápida que dura apenas alguns segundos após a conclusão do upgrade.

#### Como exibir o andamento do ajuste de configuração da instância?
Você pode exibir o andamento em [Lista de tarefas](https://console.cloud.tencent.com/mysql/task) no console.

#### O que devo fazer se o espaço em disco estiver acabando?
Se mais de 85% do espaço em disco for usado, recomendamos que você exclua os dados que não são mais usados ou expanda o espaço em disco no [console](https://console.cloud.tencent.com/cdb) selecionando **More (Mais)** > **Adjust Configurations (Ajustar configurações)** na coluna **Operation (Operação)** à direita da lista de instâncias.

#### Como posso saber se o modo QuickChange (Alteração rápida) é aceito ao ajustar a memória da instância ou a capacidade do disco?
Na página de ajuste de configuração, se o modo QuickChange (Alteração rápida) for aceito, a alternância **QuickChange (Alteração rápida)** pode ser ativada ou desativada conforme necessário; caso contrário, a alternância não poderá ser usada.
![](https://main.qcloudimg.com/raw/0ecdc6d86e3727e7a688a559ce217d7d.png)

#### A expansão da memória ou da capacidade do disco afeta a versão secundária do kernel da instância?
Se a versão secundária do kernel da instância não for a mais recente quando a memória ou a capacidade do disco for expandida, será feito o upgrade para a mais recente. Nesse caso, ativar o modo QuickChange (Alteração rápida) fará com que o banco de dados seja reiniciado.

#### A ativação do modo QuickChange (Alteração rápida) fará com que a instância reinicie?
Em alguns casos, a instância precisará ser reiniciada. Um prompt para reiniciar a instância será exibido na página de ajuste de configuração, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/d97d2daa7cb8e5aa0924355c59bc4fc8.png)

>?Se a versão secundária do kernel da instância for a mais recente, ajustar apenas a capacidade do disco no modo QuickChange (Alteração rápida) não fará com que a instância reinicie.

#### Como posso saber se o modo QuickChange (Alteração rápida) está ativado ao fazer o upgrade da configuração da instância no console?
Você pode verificar a alternância **QuickChange (Alteração rápida)** na página de ajuste de configuração: se o botão estiver ativado, o modo QuickChange (Alteração rápida) está ativado; caso contrário, o modo está desativado.
![](https://main.qcloudimg.com/raw/0ecdc6d86e3727e7a688a559ce217d7d.png)

#### Como posso saber se o modo QuickChange (Alteração rápida) está ativado quando uso APIs para ajustar a configuração da instância?
No momento, as APIs não aceitam o QuickChange (Alteração rápida), portanto, a configuração da instância poderá ser ajustada apenas migrando dados se você usar APIs. As APIs aceitarão o QuickChange (Alteração rápida) no futuro.

#### Os parâmetros do banco de dados serão modificados durante o ajuste de configuração do banco de dados?
O parâmetro `innodb_buffer_pool_size` será modificado de acordo com as alterações de configuração.

#### Os parâmetros do banco de dados serão modificados durante o ajuste de configuração do banco de dados no modo QuickChange (Alteração rápida)?
É o mesmo que o modo normal. No modo QuickChange (Alteração rápida), alguns parâmetros serão modificados de acordo com as alterações de configuração.

#### Qual é a diferença entre o modo QuickChange (Alteração rápida) e o modo normal?
O modo QuickChange (Alteração rápida) não requer migração de dados, portanto, leva menos tempo para ajustar a configuração da instância.
