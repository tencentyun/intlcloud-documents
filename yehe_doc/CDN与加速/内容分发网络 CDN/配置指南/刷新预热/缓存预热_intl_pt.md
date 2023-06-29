## Visão geral da funcionalidade

Depois que um nome de domínio é conectado ao serviço do CDN, inicialmente, ele não tem recursos nos nós de cache do CDN em toda a rede. Os recursos serão armazenados em cache quando acionados por uma solicitação do usuário. Se os recursos solicitados expirarem ou não forem armazenados em cache no nó de cache, será efetuado pull do nó intermediário do CDN para os recursos. Se eles estiverem expirados ou não forem armazenados em cache no nó intermediário, será efetuado pull do servidor de origem do usuário.

A funcionalidade de pré-busca do CDN permite enviar uma lista de recursos para carregar recursos para os nós de cache sem solicitações do usuário.

- Quando um nó carrega um recurso, se houver um recurso válido (não expirado) com o mesmo nome já armazenado em cache no nó, o recurso não será carregado. Recomendamos limpar os recursos inteiramente pela rede antes de atualizar recursos com o mesmo nome.
- Os nós carregam recursos do servidor de origem, dos quais a largura de banda aumentará após o envio de uma grande quantidade de tarefas de pré-busca.
- Os serviços de nome de domínio de aceleração são implantados em um mecanismo de aceleração de camada dupla por padrão. Ao realizar a pré-busca de recursos na China Continental, eles são carregados em nós intermediários dentro da China Continental por padrão. Já ao realizar a pré-busca de recursos nas regiões fora da China Continental, eles são carregados em servidores de borda fora da China Continental por padrão.

> Observação:
>
> Ao realizar a pré-busca de recursos nas regiões fora da China Continental, eles são carregados em servidores de borda fora da China Continental por padrão e o tráfego incorrido na camada de borda é cobrado.

## Casos de uso

### Versões do pacote de instalação

Antes de lançar uma nova edição ou atualização de pacotes de instalação, você pode realizar a pré-busca dos recursos para os nós de cache do CDN. Depois que os pacotes forem lançados oficialmente, as solicitações em massa de download dos usuários serão assumidas pelos nós de cache do CDN, aumentando a velocidade de download e reduzindo a pressão no servidor de origem.

### Eventos de marketing

Antes de iniciar eventos de marketing, você pode realizar a pré-busca dos recursos estáticos da web relacionados para os nós de cache do CDN. Depois que os eventos forem iniciados oficialmente, todos os recursos estáticos da web solicitados serão retornados dos nós de cache do CDN, garantindo a disponibilidade do serviço para uma melhor experiência do usuário por meio de reserva abundante de largura de banda.

## Guia de operações

### Como usar

1. Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), clique em **Purge and Prefetch (Limpeza e pré-busca)** na barra lateral esquerda, abra a guia **Prefetch URL (Pré-busca de URL)** para enviar uma tarefa.
2. Você pode especificar uma região de destino para realizar a pré-busca de recursos.
	- Para nomes de domínio de aceleração na China Continental, apenas **Chinese Mainland (China Continental)** pode ser especificado para aceleração.
	- Para nomes de domínio de aceleração fora da China Continental, apenas **Overseas (Exterior)** (ou seja, as regiões fora da China Continental) pode ser especificado para aceleração.
	- Para nomes de domínio de aceleração global, as regiões **Global**, **Chinese Mainland (China Continental)** e **Overseas (Exterior)** (ou seja, fora da China Continental) podem ser especificadas para aceleração.


![](https://main.qcloudimg.com/raw/410621be989e1f0f65c46fd907b6dc6a.png)


3. Na guia **History (Histórico)**, você pode consultar tarefas de pré-busca por um período de tempo e termo especificados. As consultas de períodos de termo aceitam apenas consultas com um nome de domínio ou um URL completo:
![](https://main.qcloudimg.com/raw/5f4d32e7d79a1a8d0a6390e8fecbc0ec.png)

### Precauções

#### Limites da pré-busca

- É possível fazer a pré-busca de até 1.000 URLs por dia para cada conta em cada região de aceleração e de até 20 URLs por vez. Depois que uma tarefa de pré-busca global é realizada, a cota para regiões dentro e fora da China Continental será usada ao mesmo tempo.
- É necessário adicionar o identificador de protocolo `http://` ou `https://` ao enviar uma tarefa de pré-busca.
- Não é possível fazer a pré-busca em URLs no formato `http://*.test.com`.
- Não é possível fazer a pré-busca em URLs contendo caracteres chineses.


#### Configuração de permissões de subusuários

- A pré-busca de URL e a consulta de histórico de pré-busca foram integradas ao sistema de permissões mais recente e aceitam a configuração de permissões no nível de recursos (nomes de domínio).
- Para informações sobre o método de atribuição de permissões, consulte [Permissões do console](https://intl.cloud.tencent.com/document/product/228/35229).



