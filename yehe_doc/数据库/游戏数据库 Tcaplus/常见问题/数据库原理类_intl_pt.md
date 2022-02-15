
- [Como o servidor do jogo elimina um nó tcaproxy (camada de acesso) inválido?](#52)
- [Como o servidor do jogo escolhe o nó tcaproxy (camada de acesso)?](#53)
- [O TcaplusDB tem a funcionalidade de compactação?](#59)
- [A API do TcaplusDB é thread-safe?](#61)
- [Como o tcapsvr (camada de armazenamento) realiza a recuperação de desastres?](#63)
- [Como o tcaproxy (camada de acesso) realiza a recuperação de desastres?](#62)
- [O TcaplusDB possui proteção contra sobrecarga?](#66)
- [Qual é o princípio de troca de dados de acesso frequente e não frequente para o TcaplusDB?](#71)
- [Como o tcaproxy (camada de acesso) escolhe o tcapsvr (camada de armazenamento)?](#81)
- [Qual é o nível de bloqueio no TcaplusDB?](#84)

<span id="52"></span>
### Como o servidor do jogo elimina um nó tcaproxy (camada de acesso) inválido?
A API do TcaplusDB permite a recuperação de desastres no caso de qualquer exceção de tcaproxy. Existem duas maneiras principais de a API eliminar processos tcaproxy inválidos:

1. A API considera fisicamente que um tcaproxy não está disponível. A API envia pacotes de detecção de pulsação a todos os tcaproxy conectados a cada segundo. Se um servidor de jogo não receber os pacotes de retorno de pulsação correspondentes do tcaproxy em 10 segundos, a API desconectará ativamente a conexão TCP com o tcaproxy e conectará ativamente o tcaproxy na próxima atualização.
2. A API considera logicamente que um tcaproxy não está disponível. A API calcula a taxa de solicitação e resposta de um tcaproxy a cada 10 segundos como base para a avaliação. O tempo limite máximo para um pacote de solicitação é de três segundos. Se um tcaproxy expirar mais de três vezes, o tcaproxy será considerado indisponível e nenhuma solicitação será enviada a ele. Uma solicitação `getmetdata` é enviada ao tcaproxy 60 segundos depois. Se o tcaproxy pode lidar corretamente com a solicitação `getmetadata`, a API considera o tcaproxy disponível e as solicitações serão enviadas para ele novamente.

Se o servidor do jogo descobrir que um tcaproxy não está disponível em 10 segundos, ele não enviará dados para o nó tcaproxy.

<span id="53"></span>
### Como o servidor do jogo escolhe o nó tcaproxy (camada de acesso)?
O servidor do jogo mantém um anel Hash consistente localmente. Depois que um nó tcaproxy (camada de acesso) for verificado, ele será adicionado ao anel Hash. Se um nó tcaproxy (camada de acesso) reduzir a capacidade ou o link TCP entre o servidor do jogo e o tcaproxy (camada de acesso) for desconectado devido a anormalidades na máquina, o servidor do jogo removerá o nó tcaproxy (camada de acesso) do anel Hash. O servidor do jogo calcula os valores de hash com base na chave primária na solicitação (se for uma solicitação `batchget`, ele seleciona aleatoriamente um único nó tcaproxy (camada de acesso)) e, em seguida, seleciona um único nó tcaproxy (camada de acesso) do anel de Hash consistente.

<span id="59"></span>
### O TcaplusDB tem a funcionalidade de compactação?
O TcaplusDB tem uma funcionalidade de compactação baseada no algoritmo de compactação ágil do Google, incluindo compactação de protocolo (ou seja, compactação do pacote de solicitação/resposta entre o servidor do jogo e o tcaproxy (camada de acesso) e compactação de dados (ou seja, compactação dos dados que precisam ser armazenados por tcapsvr (camada de armazenamento)). Se você deseja reduzir os custos de tráfego de rede entre o servidor do jogo e o tcaproxy (camada de acesso), recomendamos que você habilite a compactação de protocolo. Você também pode chamar a função `SetCompressSwitch` da API do TcaplusDB para habilitar a compactação do tcapsvr (camada de armazenamento), que pode economizar espaço em disco, melhorar o desempenho do disco de E/S e reduzir os recursos da CPU usados para compactação e descompactação.

<span id="61"></span>
### A API do TcaplusDB é thread-safe?
A API do TcaplusDB não é thread-safe, principalmente porque componentes como tlog e tdr não são thread-safe. Recomenda-se que uma única thread use um único objeto de API e uma única região do jogo use um único objeto de API. Se você precisar interagir entre regiões do jogo, é recomendável manter vários objetos de API com um único servidor do jogo.

<span id="62"></span>
### Como o tcaproxy (camada de acesso) realiza a recuperação de desastres?
O tcaproxy (camada de acesso) adota um esquema de design ponto a ponto, ou seja, todos os nós tcaproxy (camada de acesso) em uma única região do jogo contêm informações de roteamento de todas as tabelas em uma única região do jogo. Se um tcaproxy (camada de acesso) falhar, desde que os nós tcaproxy (camada de acesso) restantes não estejam sobrecarregados, o servidor do jogo vai eliminar o nó tcaproxy (camada de acesso) anormal, que não afetará o uso do servidor do jogo. Não existe um ponto único de risco de falha para o tcaproxy (camada de acesso).

<span id="63"></span>
### Como o tcapsvr (camada de armazenamento) realiza a recuperação de desastres?
O tcapsvr (camada de armazenamento) é executado em um modo primário-secundário (tcapsvr primário e tcapsvr secundário). Os tcapsvr primários e secundários sincronizam dados em tempo real e são implantados em diferentes IDCs na mesma cidade, garantindo que a latência de sincronização primário-secundário seja inferior a 10 ms. Se o tcapsvr secundário estiver anormal, não afetará o uso do servidor do jogo (se o descarregamento da solicitação de leitura não estiver habilitado, as solicitações do servidor do jogo serão processadas pelo tcapsvr primário. Se o descarregamento da solicitação de leitura estiver habilitado, o tcapsvr secundário ajudará no processamento de parte das solicitações de leitura e o DBA recriará o tcapsvr secundário; se o tcapsvr primário for anormal, o tcapsvr secundário executará a recuperação de falhas e o DBA solicitará uma nova máquina para recriar o tcapsvr secundário. Não existe um ponto único de risco de falha para o tcapsvr (camada de armazenamento).

<span id="66"></span>
### O TcaplusDB possui proteção contra sobrecarga?
A camada de acesso e a camada de armazenamento têm medidas de proteção contra sobrecarga no nível dos processos para garantir que os serviços não entrem em colapso durante os horários de pico.

<span id="71"></span>
### Qual é o princípio de troca de dados de acesso frequente e não frequente para o TcaplusDB?
O TcaplusDB usa memória + armazenamento em disco SSD. Os primeiros GB de dados de um único arquivo de mecanismo são mapeados na memória. Os dados de acesso frequente são colocados na memória e os dados de acesso não frequente são colocados no disco. O algoritmo LRU é usado para troca de dados de acesso frequente e não frequente. A operação `get` do servidor do jogo dispara a operação de swap-in LRU, e a thread LRU de tcapsvr (camada de armazenamento) é responsável pela operação de swap-out LRU. Tente garantir que os dados de acesso frequente sejam armazenados na memória, garantindo assim uma alta taxa de acertos do cache e baixa latência de leitura e gravação única.

<span id="81"></span>
### Como o tcaproxy (camada de acesso) escolhe o tcapsvr (camada de armazenamento)?
Cada tabela define uma shardkey. Se nenhuma shardkey for definida, a shardkey padroniza para a chave primária. O tcaproxy (camada de acesso) seleciona o tcapsvr (camada de armazenamento) correspondente de acordo com `hash (shardkey) % 10000` (em que % é o operador restante), então a shardkey deve ser altamente discreta.

<span id="84"></span>
### Qual é o nível de bloqueio no TcaplusDB?
A granularidade do bloqueio no TcaplusDB é o nível de registro em log.
