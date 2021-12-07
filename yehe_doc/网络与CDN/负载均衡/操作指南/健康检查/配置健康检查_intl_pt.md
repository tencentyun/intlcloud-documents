Ao configurar listeners, você pode ativar a verificação de integridade para obter as informações de disponibilidade de servidores de back-end. Para obter mais informações sobre verificação de integridade, consulte [Visão geral da verificação de integridade](https://intl.cloud.tencent.com/document/product/214/6097).

<span id="postreq"></span>
## Pré-requisitos
1. Crie uma instância do CLB. Para obter mais informações, consulte [Criação de instâncias do CLB](https://intl.cloud.tencent.com/document/product/214/6149).
2. Crie um listener do CLB.
 - Para criar um listener TCP, consulte mais informações em [Configuração de um listener TCP](https://intl.cloud.tencent.com/document/product/214/32517).
 - Para criar um listener UDP, consulte mais informações em [Configuração de um listener UDP](https://intl.cloud.tencent.com/document/product/214/32518).
 - Para criar um listener TCP SSL, consulte mais informações em [Configuração de um listener TCP SSL](https://intl.cloud.tencent.com/document/product/214/32519).
 - Para criar um listener HTTP, consulte mais informações em [Configuração de um listener HTTP](https://intl.cloud.tencent.com/document/product/214/32515).
 - Para criar um listener HTTPS, consulte mais informações em [Configuração de um listener HTTPS](https://intl.cloud.tencent.com/document/product/214/32516).

## Listener TCP
Os listeners TCP da camada 4 são compatíveis com três tipos de verificações de integridade: verificação de integridade do TCP de camada 4, verificação de integridade do HTTP de camada 7 e a verificação de integridade de protocolo personalizado.
- As verificações de integridade do TCP são conduzidas com pacotes SYN, ou seja, handshakes TCP de três vias são iniciados para obter as informações de status das instâncias do CVM de back-end.
- As verificações de integridade de HTTP são conduzidas enviando solicitações de HTTP para obter as informações de status de instâncias do CVM de back-end.
- As verificações de integridade do protocolo personalizado são conduzidas personalizando o conteúdo de entrada e saída do protocolo da camada de aplicativo para obter as informações de status das instâncias do CVM de back-end.

### Configuração de verificação de integridade do TCP
1. Configure um listener para a etapa de **Health Check (Verificação de integridade)** conforme instruído em [Pré-requisitos](#postreq).
2. Na etapa de **Health Check (Verificação de integridade)**, selecione **TCP** como o protocolo.
<table>
<tr>
<th>Parâmetro</th><th>Descrição</th>
</tr>
<tr>
<td>Verificação de integridade</td><td>Pode ser habilitada ou desabilitada. Recomendamos habilitá-la para verificações automáticas em instâncias do CVM de back-end e remoção de portas anormais.</td>
</tr>
<tr>
<td>Protocolo</td><td>As verificações de integridade do TCP serão realizadas se **TCP** for selecionado.</td>
</tr>
<tr>
<td>Porta</td><td>É opcional. Recomendamos não especificar a porta, a menos que você precise verificar algumas específicas. A porta do servidor de back-end será verificada se a porta não for especificada aqui.</td>
</tr>
<tr>
<td>Mostrar opções avançadas</td><td>Para mais informações, consulte <a href="#advance">Opções avançadas</a>.</td>
</tr>
</table>

### Configuração de verificação de integridade do HTTP
1. Configure um listener para a etapa de **Health Check (Verificação de integridade)** conforme instruído em [Pré-requisitos](#postreq).
2. Na etapa de **Health Check (Verificação de integridade)**, selecione **HTTP** como o protocolo.
<table>
<tr>
<th>Parâmetro</th><th>Descrição</th>
</tr>
<tr>
<td>Verificação de integridade</td><td>Pode ser habilitada ou desabilitada. Recomendamos habilitá-la para verificações automáticas em instâncias do CVM de back-end e remoção de portas anormais.</td>
</tr>
<tr>
<td>Protocolo</td><td>As verificações de integridade do HTTP serão realizadas se **HTTP** for selecionado.</td>
</tr>
<tr>
<td>Porta</td><td>É opcional. Recomendamos não especificar a porta, a menos que você precise verificar algumas específicas. A porta do servidor de back-end será verificada se a porta não for especificada aqui.</td>
</tr>
<tr>
<td>Verificar domínio</td><td>Requisitos em nomes de domínio de verificação de integridade:
<ul>
<li>Comprimento: 1 a 80 caracteres.</li>
<li>É o nome do domínio de encaminhamento por padrão.</li>
<li>Expressões regulares não são compatíveis. Se o seu nome de domínio de encaminhamento for um curinga, você precisará especificar um nome de domínio fixo (não regular) como o nome de domínio de verificação de integridade.</li>
<li>Caracteres compatíveis: letras minúsculas (a a z), dígitos (0 a 9), pontos decimais (.) e hifens (-).</li>
</ul></td>
</tr>
<tr>
<td>Caminho</td><td>Requisitos em caminhos de verificação de integridade:
<ul>
<li>Comprimento: 1 a 200 caracteres.</li>
<li>`/` é o valor padrão e deve ser o primeiro caractere.</li>
<li>Expressões regulares não são compatíveis. Recomendamos especificar um URL fixo (página da web estática) para a verificação de integridade.</li>
<li>Caracteres compatíveis: letras minúsculas (a a z), letras maiúsculas (A a Z), dígitos (0 a 9), pontos decimais (.), hifens (-), sublinhados (_), barras (/), sinais de igual (=) e pontos de interrogação (?).</li>
</ul></td>
</tr>
<tr>
<td>Método de solicitação HTTP</td><td>Método de solicitação HTTP de verificações de integridade. Opções: GET (método padrão) e HEAD.
<ul>
<li>Se HEAD for selecionado, o servidor retornará apenas as informações do cabeçalho HTTP, o que pode reduzir sobrecargas de back-end e melhorar a eficiência da solicitação. O servidor de back-end deve ser compatível com HEAD.</li>
<li>Se GET for selecionado, o servidor de back-end deve ser compatível com GET.</li>
</ul></td>
</tr>
<tr>
<td>Versão HTTP</td><td>Versão HTTP do servidor de back-end.
<ul>
<li>Se a versão compatível com o servidor de back-end for HTTP 1.0, o campo host da solicitação não precisa de autenticação, ou seja, o domínio de verificação não precisa ser configurado.</li>
<li>Se a versão compatível com o servidor de back-end for HTTP 1.1, o campo host da solicitação precisa de autenticação, ou seja, o domínio de verificação precisa ser configurado ou o código de erro 404 será retornado.</li>
</ul></td>
</tr>
<tr>
<td>Código de status normal</td><td>Se o código de status for dos selecionados, o servidor de back-end é considerado ativo (íntegro). Opções: http_1xx, http_2xx, http_3xx, http_4xx e http_5xx. Você pode selecionar várias opções.</td>
</tr>
<tr>
<td>Mostrar opções avançadas</td><td>Para mais informações, consulte <a href="#advance">Opções avançadas</a>.</td>
</tr>
</table>

### Configuração de verificação de integridade do protocolo personalizado
1. Configure um listener para a etapa de **Health Check (Verificação de integridade)** conforme instruído em [Pré-requisitos](#postreq).
2. Na etapa de **Health Check (Verificação de integridade)**, selecione **HTTP** como o protocolo.
<table>
<tr>
<th>Parâmetro</th><th>Descrição</th>
</tr>
<tr>
<td>Verificação de integridade</td><td>Pode ser habilitada ou desabilitada. Recomendamos habilitá-la para verificações automáticas em instâncias do CVM de back-end e remoção de portas anormais.</td>
</tr>
<tr>
<td>Protocolo</td><td>As verificações de integridade do protocolo personalizado serão realizadas se **Custom Protocol (Protocolo personalizado)** for selecionado.</td>
</tr>
<tr>
<td>Porta</td><td>É opcional. Recomendamos não especificar a porta, a menos que você precise verificar algumas específicas. A porta do servidor de back-end será verificada se a porta não for especificada aqui.</td>
</tr>
<tr>
<td>Formato de entrada</td><td>Compatível com texto e strings hexadecimais.
<ul>
<li>Se Texto for selecionado, o texto será convertido em uma string binária para enviar solicitações e comparar os resultados retornados.</li>
<li>Se Hexadecimal for selecionado, a string hexadecimal será convertida em uma string binária para enviar solicitações e comparar os resultados retornados.</li>
</ul></td>
</tr>
<tr>
<td>Solicitação</td><td>Conteúdo da solicitação de verificação de integridade personalizada</td>
</tr>
<tr>
<td>Resultado de retorno</td><td>Ao personalizar uma solicitação de verificação de integridade, é preciso inserir o resultado de retorno da verificação de integridade.</td>
</tr>
<tr>
<td>Mostrar opções avançadas</td><td>Para mais informações, consulte <a href="#advance">Opções avançadas</a>.</td>
</tr>
</table>


## Listener UDP
Os listeners UDP são compatíveis com verificações de integridade de UDP, que podem ser realizadas verificando as portas e executando o comando Ping.

### Configuração de verificação de integridade do UDP - verificação de porta
1. Configure um listener para a etapa de **Health Check (Verificação de integridade)** conforme instruído em [Pré-requisitos](#postreq).
2. Na etapa de **Health Check (Verificação de integridade)**, selecione **Port (Porta)** como o protocolo.
<table>
<tr>
<th>Parâmetro</th><th>Descrição</th>
</tr>
<tr>
<td>Verificação de integridade</td><td>Pode ser habilitada ou desabilitada. Recomendamos habilitá-la para verificações automáticas em instâncias do CVM de back-end e remoção de portas anormais.</td>
</tr>
<tr>
<td>Protocolo</td><td>Se a Port (Porta) for selecionada, os pacotes de detecção de UDP serão enviados para a instância do CVM de back-end por meio do VIP (ou seja, o endereço IP usado por uma instância do CLB para fornecer serviço aos clientes), e o IP da instância do CVM de back-end será pingado para obter o status da instância do CVM de back-end.</td>
</tr>
<tr>
<td>Porta</td><td>É opcional. Recomendamos não especificar a porta, a menos que você precise verificar algumas específicas. A porta do servidor de back-end será verificada se a porta não for especificada aqui.</td>
</tr>
<tr>
<td>Formato de entrada</td><td>Compatível com texto e strings hexadecimais.
<ul>
<li>Se Texto for selecionado, o texto será convertido em uma string binária para enviar solicitações e comparar os resultados retornados.</li>
<li>Se Hexadecimal for selecionado, a string hexadecimal será convertida em uma string binária para enviar solicitações e comparar os resultados retornados.</li>
</ul></td>
</tr>
<tr>
<td>Solicitação</td><td>É opcional. Conteúdo da solicitação de verificação de integridade personalizada.</td>
</tr>
<tr>
<td>Resultado de retorno</td><td>É opcional. Ao personalizar uma solicitação de verificação de integridade, é preciso inserir o resultado de retorno da verificação de integridade.</td>
</tr>
<tr>
<td>Mostrar opções avançadas</td><td>Para mais informações, consulte <a href="#advance">Opções avançadas</a>.</td>
</tr>
</table>


### Configuração de verificação de integridade do UDP- Comando ping
1. Configure um listener para a etapa de **Health Check (Verificação de integridade)** conforme instruído em [Pré-requisitos](#postreq).
2. Na etapa de **Health Check (Verificação de integridade)**, selecione **PING** como o protocolo.
<table>
<tr>
<th>Parâmetro</th><th>Descrição</th>
</tr>
<tr>
<td>Verificação de integridade</td><td>Pode ser habilitada ou desabilitada. Recomendamos habilitá-la para verificações automáticas em instâncias do CVM de back-end e remoção de portas anormais.</td>
</tr>
<tr>
<td>Protocolo</td><td>Se PING for selecionado, o IP da instância do CVM de back-end será pingado para obter o status da instância de CVM de back-end.</td>
</tr>
<tr>
<td>Mostrar opções avançadas</td><td>Para mais informações, consulte <a href="#advance">Opções avançadas</a>.</td>
</tr>
</table>


## Listener TCP SSL

### Configuração de verificação de integridade do TCP
1. Configure um listener para a etapa de **Health Check (Verificação de integridade)** conforme instruído em [Pré-requisitos](#postreq).
2. Na etapa de **Health Check (Verificação de integridade)**, selecione **TCP** como o protocolo.
<table>
<tr>
<th>Parâmetro</th><th>Descrição</th>
</tr>
<tr>
<td>Verificação de integridade</td><td>Pode ser habilitada ou desabilitada. Recomendamos habilitá-la para verificações automáticas em instâncias do CVM de back-end e remoção de portas anormais.</td>
</tr>
<tr>
<td>Protocolo</td><td>As verificações de integridade do TCP serão realizadas se **TCP** for selecionado.</td>
</tr>
<tr>
<td>Porta</td><td>A porta de verificação de integridade e a porta de escuta dos listeners TCP SSL são as mesmas.</td>
</tr>
<tr>
<td>Mostrar opções avançadas</td><td>Para mais informações, consulte <a href="#advance">Opções avançadas</a>.</td>
</tr>
</table>

### Configuração de verificação de integridade do HTTP
1. Configure um listener para a etapa de **Health Check (Verificação de integridade)** conforme instruído em [Pré-requisitos](#postreq).
2. Na etapa de **Health Check (Verificação de integridade)**, selecione **HTTP** como o protocolo.
<table>
<tr>
<th>Parâmetro</th><th>Descrição</th>
</tr>
<tr>
<td>Verificação de integridade</td><td>Pode ser habilitada ou desabilitada. Recomendamos habilitá-la para verificações automáticas em instâncias do CVM de back-end e remoção de portas anormais.</td>
</tr>
<tr>
<td>Protocolo</td><td>As verificações de integridade do HTTP serão realizadas se **HTTP** for selecionado.</td>
</tr>
<tr>
<td>Porta</td><td>A porta de verificação de integridade e a porta de escuta dos listeners TCP SSL são as mesmas.</td>
</tr>
<tr>
<td>Verificar domínio</td><td>Requisitos em nomes de domínio de verificação de integridade:
<ul>
<li>Comprimento: 1 a 80 caracteres.</li>
<li>É o nome do domínio de encaminhamento por padrão.</li>
<li>Expressões regulares não são compatíveis. Se o seu nome de domínio de encaminhamento for um curinga, você precisará especificar um nome de domínio fixo (não regular) como o nome de domínio de verificação de integridade.</li>
<li>Caracteres compatíveis: letras minúsculas (a a z), dígitos (0 a 9), pontos decimais (.) e hifens (-).</li>
</ul></td>
</tr>
<tr>
<td>Caminho</td><td>Requisitos em caminhos de verificação de integridade:
<ul>
<li>Comprimento: 1 a 200 caracteres.</li>
<li>`/` é o valor padrão e deve ser o primeiro caractere.</li>
<li>Expressões regulares não são compatíveis. Recomendamos especificar um URL fixo (página da web estática) para a verificação de integridade.</li>
<li>Caracteres compatíveis: letras minúsculas (a a z), letras maiúsculas (A a Z), dígitos (0 a 9), pontos decimais (.), hifens (-), sublinhados (_), barras (/), sinais de igual (=) e pontos de interrogação (?).</li>
</ul></td>
</tr>
<tr>
<td>Método de solicitação HTTP</td><td>Método de solicitação HTTP de verificações de integridade. Opções: GET (método padrão) e HEAD.
<ul>
<li>Se HEAD for selecionado, o servidor retornará apenas as informações do cabeçalho HTTP, o que pode reduzir sobrecargas de back-end e melhorar a eficiência da solicitação. O servidor de back-end deve ser compatível com HEAD.</li>
<li>Se GET for selecionado, o servidor de back-end deve ser compatível com GET.</li>
</ul></td>
</tr>
<tr>
<td>Versão HTTP</td><td>Versão HTTP do servidor de back-end. Apenas o HTTP 1.1 é compatível. O servidor de back-end precisa autenticar o campo host da solicitação, ou seja, o domínio da verificação precisa ser configurado, ou o código de erro 404 será retornado.
</td>
</tr>
<tr>
<td>Código de status normal</td><td>Se o código de status for dos selecionados, o servidor de back-end é considerado ativo (íntegro). Opções: http_1xx, http_2xx, http_3xx, http_4xx e http_5xx. Você pode selecionar várias opções.</td>
</tr>
<tr>
<td>Mostrar opções avançadas</td><td>Para mais informações, consulte <a href="#advance">Opções avançadas</a>.</td>
</tr>
</table>

<span id="http"></span>
## Listener HTTP
### Configuração de verificação de integridade do HTTP
1. Configure um listener para a etapa de **Health Check (Verificação de integridade)** conforme instruído em [Pré-requisitos](#postreq).
<table>
<tr>
<th>Parâmetro</th><th>Descrição</th>
</tr>
<tr>
<td>Verificação de integridade</td><td>Pode ser habilitada ou desabilitada. Recomendamos habilitá-la para verificações automáticas em instâncias do CVM de back-end e remoção de portas anormais.</td>
</tr>
<tr>
<td>Verificar domínio</td><td>Requisitos em nomes de domínio de verificação de integridade:
<ul>
<li>Comprimento: 1 a 80 caracteres.</li>
<li>É o nome do domínio de encaminhamento por padrão.</li>
<li>Expressões regulares não são compatíveis. Se o seu nome de domínio de encaminhamento for um curinga, você precisará especificar um nome de domínio fixo (não regular) como o nome de domínio de verificação de integridade.</li>
<li>Caracteres compatíveis: letras minúsculas (a a z), dígitos (0 a 9), pontos decimais (.) e hifens (-).</li>
</ul></td>
</tr>
<tr>
<td>Caminho</td><td>O caminho da verificação de integridade pode ser definido como o diretório raiz do servidor de back-end ou um URL especificado Os requisitos são os seguintes:
<ul>
<li>Comprimento: 1 a 200 caracteres.</li>
<li>`/` é o valor padrão e deve ser o primeiro caractere.</li>
<li>Expressões regulares não são compatíveis. Recomendamos especificar um URL fixo (página da web estática) para a verificação de integridade.</li>
<li>Caracteres compatíveis: letras minúsculas (a a z), letras maiúsculas (A a Z), dígitos (0 a 9), pontos decimais (.), hifens (-), sublinhados (_), barras (/), sinais de igual (=) e pontos de interrogação (?).</li>
</ul>
</td>
</tr>
<tr>
<td>Tempo limite de resposta</td><td><ul><li>Tempo limite máximo de resposta para uma verificação de integridade.</li><li>Se um servidor de back-end não responder dentro do tempo limite, será considerado anormal.</li><li>Intervalo de valores: 2 a 60 segundos.</li></ul></td>
</tr>
<tr>
<td>Intervalo de verificação</td><td><ul><li>Intervalo entre duas verificações de integridade.</li><li>Intervalo de valores: 5 a 300 segundos.</li></ul></td>
</tr>
<tr>
<td>Limite de não integridade</td><td><ul><li>Se o resultado da verificação de integridade falhar por n (um valor personalizável) vezes, considera-se que a instância do CVM de back-end não está íntegra e o status exibido no console é **Abnormal (Anormal)**.</li><li>Intervalo de valores: 2 a 10 vezes.</li></ul></td>
</tr>
<tr>
<td>Limite de integridade</td><td><ul><li>Se o resultado da verificação de integridade falhar por n (um valor personalizável) vezes, considera-se que a instância do CVM de back-end está íntegra e o status exibido no console é **Healthy (Íntegro)**</li><li>Intervalo de valores: 2 a 10 vezes. </li></ul></td>
</tr>
<tr>
<td>Método de solicitação HTTP</td><td>Método de solicitação HTTP de verificações de integridade. Opções: GET (método padrão) e HEAD.
<ul>
<li>Se HEAD for selecionado, o servidor retornará apenas as informações do cabeçalho HTTP, o que pode reduzir sobrecargas de back-end e melhorar a eficiência da solicitação. O servidor de back-end deve ser compatível com HEAD.</li>
<li>Se GET for selecionado, o servidor de back-end deve ser compatível com GET.</li>
</ul></td>
</tr>
<tr>
<td>Código de status normal</td><td>Se o código de status for dos selecionados, o servidor de back-end é considerado ativo (íntegro). Opções: http_1xx, http_2xx, http_3xx, http_4xx e http_5xx. Você pode selecionar várias opções.</td>
</tr>
</table>

## Listener HTTPS
>?Se HTTP for selecionado como o protocolo de back-end das regras de encaminhamento do listener HTTPS, a verificação de integridade de HTTP será conduzida; se HTTPS for selecionado, a verificação de integridade de HTTPS será conduzida.
>
Para a configuração de verificação de integridade de listeners HTTPS, consulte <a href="#http">Listener HTTP</a>.

<span id="advance"></span>
## Opções avançadas
| Configuração de verificação de integridade | Descrição     | Valor padrão        |
| ------- | ------------------------ | ---------------------------------------- |
| Tempo limite de resposta | <li>Tempo limite máximo de resposta para uma verificação de integridade.</li><li>Se um servidor de back-end não responder dentro do tempo limite, será considerado anormal.</li><li>Intervalo de valores: 2 a 60 segundos.</li> | 2 segundos |
| Intervalo de verificações | <li>Intervalo entre duas verificações de integridade.</li><li>Intervalo de valores: 5 a 300 segundos.</li> | 5 segundos |
| Limite de não integridade | <li>Se o resultado da verificação de integridade falhar por n (um valor personalizável) vezes, considera-se que a instância do CVM de back-end não está íntegra e o status exibido no console é **Abnormal (Anormal)**.</li><li>Intervalo de valores: 2 a 10 vezes.</li> | 3 vezes |
| Limite de integridade |<li>Se o resultado da verificação de integridade for satisfatório por n (um valor personalizável) vezes, considera-se que a instância do CVM de back-end está íntegra e o status exibido no console é **Healthy (Íntegro)**.</li><li>Intervalo de valores: 2 a 10 vezes. </li> | 3 vezes |
