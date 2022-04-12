
Este documento descreve três políticas de isolamento de recursos do TencentDB for MySQL: básica, geral e dedicada.

>?
>- A antiga “Edição básica” foi renomeada como “nó único básico”, e a antiga “Edição de alta E/S de nó único (single-node)” foi renomeada como "nó único geral".
>- As Instâncias de dois e três nós aceitam as políticas geral e dedicada. Atualmente, a política dedicada está em versão beta; portanto, para adquirir instâncias dedicadas, [envie um tíquete](https://console.cloud.tencent.com/workorder/category).

| Política de isolamento de recursos | Descrição                                                         |
| -------- | ------------------------------------------------------------ |
| Básica   | Somente as instâncias de nó único aceitam essa política. Uma instância de nó único básico (anteriormente conhecida como edição básica) permite a separação de armazenamento de computação e usa discos em nuvem como armazenamento subjacente. |
| Geral   | <li>Uma instância geral tem uso exclusivo da memória alocada e dos recursos de disco, mas compartilha recursos de CPU com outras instâncias gerais na mesma máquina física. <li>Ao compartilhar recursos de CPU, uma instância geral desfruta de especificações mais altas a um custo menor. <li>A capacidade do disco de uma instância geral é independente de suas especificações de CPU e memória. |
| Dedicada   | <li>Uma instância dedicada tem uso exclusivo de recursos de CPU (fixação de CPU configurada), memória e disco. Possui desempenho estável a longo prazo e não será afetada pelo comportamento de outras instâncias na máquina física. <li>Uma instância dedicada com as configurações mais altas pode monopolizar uma máquina física e todos os seus recursos. | 


