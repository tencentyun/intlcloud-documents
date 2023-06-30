Um grupo de posicionamento é uma política para a distribuição de instâncias no hardware. As instâncias criadas no grupo de posicionamento apresentam recuperação de desastre e alta disponibilidade quando iniciadas. O Tencent Cloud CVM fornece uma política de posicionamento de instância, que pode forçar as instâncias a serem dispersas com uma determinada política e reduzir o impacto da falha de hardware/software nos serviços do CVM. Você pode usar o grupo de posicionamento para implementar instâncias do CVM em diferentes servidores físicos e garantir a alta disponibilidade do serviço e a respectiva capacidade de recuperação de desastre. Quando você criar instâncias em um grupo de posicionamento, nós as iniciaremos em uma região especificada de acordo com a política de implantação que você configurou previamente. Se você não configurou um grupo de posicionamento para as instâncias, tentaremos iniciá-las em diferentes servidores físicos para garantir a disponibilidade do serviço.

## Grupo de posicionamento disperso

Atualmente, os grupos de posicionamento disperso são compatíveis. Um grupo de posicionamento disperso é um grupo de instâncias que são colocadas em diferentes hardwares e têm alta disponibilidade. Recomendamos que você use um grupo de posicionamento disperso para aplicativos de instâncias importantes que precisam ser colocados separadamente, como bancos de dados mestre/subordinado e clusters de alta disponibilidade. Ao iniciar as instâncias em um grupo de posicionamento disperso, você pode minimizar a falha simultânea de instâncias com o mesmo hardware.
Um grupo de posicionamento disperso é específico da região e pode ser implantado em várias zonas de disponibilidade. Existe um limite para a quantidade de instâncias que podem ser colocadas em um grupo. Para obter mais informações, consulte [Console](https://console.cloud.tencent.com/cvm/ps).

> Ao iniciar instâncias em um grupo de posicionamento disperso, ocorrerá falha da solicitação se você não tiver hardware suficiente. Você pode aguardar um pouco e tentar novamente.

## Regras e limites de grupos de posicionamento disperso

Antes de usar um grupo de posicionamento disperso, confira as seguintes regras:
-  Os grupos de posicionamento não podem ser mesclados.
-  Uma instância não pode ser colocada em vários grupos de posicionamento.
-  O grupo de posicionamento disperso pode ser colocado em computadores, interruptores ou racks físicos.
-  A quantidade máxima de instâncias que o grupo de posicionamento disperso suporta em computadores, interruptores ou racks físicos é diferente. Para obter mais informações, consulte o site oficial.
-  Se você especificar e usar a política do grupo de recuperação de desastres, ela será seguida à risca. Lembre-se de que, se não houver hardware suficiente para distribuir as instâncias, ocorrerá falha na criação de algumas instâncias.
-  As instâncias no CDH não são compatíveis com grupos de posicionamento disperso.

## Guia de operação
Para obter mais informações sobre as operações, consulte [Grupo de posicionamento disperso](https://intl.cloud.tencent.com/document/product/213/17020).
