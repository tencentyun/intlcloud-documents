## Fluxos de processo
Os fluxos de processo do CLB da camada 7 e da camada 4 (anteriormente conhecido como CLB do aplicativo) são mostrados abaixo:
![](https://main.qcloudimg.com/raw/9c30c679e6a5fd70f9dd9273f8784d6d.jpg)
Se o CLB da camada 7 for usado para encaminhar protocolos HTTP/HTTPS, você pode adicionar um nome de domínio correspondente ao criar a regra de encaminhamento em um listener do CLB.
- Se apenas uma regra de encaminhamento for criada, você poderá acessá-la e o serviço por meio do VIP + URL.
- Se várias regras de encaminhamento forem criadas, o uso de VIP + URL não garante o acesso a um nome de domínio + URL especificado. Você deve acessar um nome de domínio + URL diretamente para se certificar de que uma regra de encaminhamento entrou em vigor. Em outras palavras, quando você configura várias regras de encaminhamento, um VIP pode corresponder a vários nomes de domínio. Nesse caso, recomendamos que você acesse o serviço por meio do nome de domínio + URL especificado, em vez de VIP + URL.

## Configurações de encaminhamento da camada 7
### Configurações de encaminhamento de domínios
O CLB da camada 7 pode encaminhar solicitações de nomes de domínio e URLs diferentes para servidores diferentes. Um listener da camada 7 pode ser configurado com vários nomes de domínio, cada um dos quais pode ser configurado com vários caminhos de encaminhamento.
- Limite de comprimento para o nome de domínio encaminhado: 1 a 80 caracteres.
- Não pode começar com `_`.
- Um domínio exato é aceito, como `www.example.com`.
- Nomes de domínio curinga são aceitos, mas atualmente apenas aqueles na forma de `*.exemplp.com` ou `www.example.*`, ou seja, nomes de domínio curinga que começam ou terminam com `*`, o qual aparece apenas uma vez.
- Para nomes de domínio encaminhados sem regex, os conjuntos de caracteres válidos incluem `a-z`, `0-9`, `.`, ` -` e `_`.
- O nome de domínio encaminhado aceita regex. Nomes de domínio regex:
  - Os conjuntos de caracteres aceitos incluem `a-z`, `0-9`, `.`, `-`, `?`, `=`, `~`, `_`, `-`, `+`, `<code>\\</code>`, `^`, `*`, `!`, `$`, `&`, `|`, `(`, `)`, `[` e `]`.
  - Deve começar com `~`, que pode aparecer apenas uma vez.
  - Um exemplo de nome de domínio regex aceito pelo CLB pode ser `~^www\d+\.exemplo\.com$`.

### Correspondência de nomes de domínio encaminhados
#### Políticas gerais de correspondência
1. Se você inserir um endereço IP em vez de um nome de domínio na regra de encaminhamento e configurar vários URLs no grupo de encaminhamento, o VIP + URL serão usados para acessar o serviço.
2. Se você configurar um nome de domínio completo na regra de encaminhamento e vários URLs no grupo de encaminhamento, o nome de domínio + URL serão usados para acessar o serviço.
3. Se configurar um nome de domínio curinga na regra de encaminhamento e vários URLs no grupo de encaminhamento, você acessará o serviço por meio da correspondência do nome de domínio e URLs solicitados. Para que nomes de domínio diferentes apontem para o mesmo URL, você pode usar este método de configuração. Considerando `example.qcould.com` como exemplo, o formato é o seguinte:
 - Correspondência exata: corresponde ao nome de domínio que é totalmente compatível com o domínio inserido
 - Prefixo curinga: corresponde a todos os nomes de domínio com o domínio de segundo e superior nível especificado, como `*.qcloud.com`. 
 - Sufixo curinga: corresponde a todos os nomes de domínio com o domínio de terceiro e segundo nível especificado, como `example.qcloud. *`.
 - Correspondência regex:  `~^www\d+\.exemplo\.com$`
 - Prioridade: **Correspondência exata** > **Prefixo curinga** > **Sufixo curinga** > **Correspondência regex**. É recomendável usar um nome de domínio mais preciso para evitar a ativação de várias regras de correspondência. Caso contrário, você poderá obter resultados de correspondência imprecisos quando vários nomes de domínio no mesmo nível forem atingidos ao mesmo tempo.
4. Se você configurar um nome de domínio na regra de encaminhamento e um URL para correspondência difusa no grupo de encaminhamento, pode iniciar a correspondência completa usando correspondências de prefixo e adicionando um caractere curinga com sufixo `$`.
Por exemplo, se você inserir `URL ~*.(gif|jpg|bmp)$`, ele corresponderá a todos os arquivos .gif, .jpg e .bmp.

#### Política de nome de domínio padrão[](id:default)
Quando o nome de domínio solicitado não corresponde a nenhuma regra, o CLB encaminhará a solicitação ao nome de domínio padrão (servidor padrão). Um listener pode ter apenas um nome de domínio padrão.
Por exemplo, o listener `HTTP: 80` da instância 1 do CLB foi configurado com dois nomes de domínio: `www.test1.com` e `www.test2.com`, em que `www.test1.com` é o nome de domínio padrão. Quando um usuário visitar `www.example.com` e nenhum nome de domínio for correspondido, o CLB encaminhará a solicitação para o nome de domínio padrão `www.test1.com`.

>?
>  - Se o listener da camada 7 tiver um nome de domínio padrão configurado, as solicitações do cliente que não corresponderem a outras regras serão encaminhadas a ele.
>  - Se o listener da camada 7 não tiver um nome de domínio padrão configurado, as solicitações do cliente que não corresponderem a outras regras serão encaminhadas para o primeiro nome de domínio carregado pelo CLB (sua ordem de carregamento pode ser diferente daquela configurada no console; portanto, pode não ser o primeiro configurado no console). 
>- A partir de 18 de maio de 2020:
>  - Todos os listeners novos da camada 7 devem ter um nome de domínio padrão: a primeira regra de um listener da camada 7 será definida como o nome de domínio padrão. Quando você cria uma regra da camada 7 via API, o campo `DefaultServer` é definido como `true`.
>  - Para todos os listeners que têm um nome de domínio padrão configurado, você precisa especificar um novo nome de domínio padrão ao modificar ou excluir o nome de domínio padrão existente: quando você executa a operação no console, precisa especificar um novo nome de domínio padrão; quando você executa a operação chamando uma API, se não definir um novo nome de domínio padrão, o CLB definirá o primeiro criado entre os nomes de domínio restantes como o novo nome de domínio padrão.
>  - Para regras existentes sem um nome de domínio padrão, você pode configurar diretamente um nome de domínio padrão com base em suas necessidades de negócios, conforme instruído na [operação 4](#step4) abaixo. Se não fizer isso, o Tencent Cloud definirá o primeiro nome de domínio carregado pelo CLB como o nome de domínio padrão. Os listeners existentes serão todos processados antes de 19 de junho de 2020.
>
>A política acima será implementada gradualmente a partir de 18 de maio de 2020, e a data de vigência de cada instância pode variar um pouco. A partir de 20 de junho de 2020, todos os listeners da camada 7 que possuem um nome de domínio encaminhado terão um nome de domínio padrão.

As quatro operações a seguir podem ser realizadas no nome de domínio padrão:
- **Operação 1**: ao configurar a primeira regra de encaminhamento para o listener da camada 7, o nome de domínio padrão deve estar com o status "enabled (ativado)".
- **Operação 2**: desative o nome de domínio padrão atual.
 - Se houver vários nomes de domínio em um listener, ao desativar o nome de domínio padrão atual, você precisa especificar um novo nome de domínio padrão.
 - Se um listener tiver apenas um nome de domínio e ele for o nome de domínio padrão, não poderá ser desativado.
- **Operação 3**: exclua o nome de domínio padrão.
 - Se houver vários nomes de domínio em um listener, ao excluir uma regra no nome de domínio padrão:
   - Se a regra não for a última regra do nome de domínio padrão, você poderá exclui-la diretamente.
   - Se a regra for a última regra do nome de domínio padrão, você precisará definir um novo nome de domínio padrão.
 - Se houver apenas um nome de domínio em um listener, você poderá excluir diretamente todas as regras sem definir um novo nome de domínio padrão.
- <span id = "step4"></span>**Operação 4**: você pode modificar o nome de domínio padrão rapidamente na lista de listeners.

### Regras de configuração do caminho do URL encaminhado
O CLB da camada 7 pode encaminhar solicitações de URLs diferentes a servidores diferentes para processamento, e vários caminhos de URL encaminhados podem ser configurados para um único nome de domínio.
- Limite de comprimento do URL encaminhado: 1 a 200 caracteres.
- Um URL encaminhado sem regex deve começar com `/`., com conjuntos de caracteres válidos incluindo `a-z`, `A-Z`, `0-9`, `.`, `-`, `_`, `/`, `=`, `?` e `:`.
- O URL encaminhado aceita regex:
  - Um URL regex deve começar com `~`, que pode aparecer apenas uma vez.
  - Para um URL regex, os conjuntos de caracteres válidos incluem `a-z`, `A-Z`, `0-9`, `.`, `-`, `_`, `/`, `=`, `?`, `~`, `^`, `*`, `$`, `:`, `(`, `)`, `[`, `]`, `+` e `|`.
  - Um exemplo de URL regex pode ser `~* .png$`.
- As regras de correspondência para um URL encaminhado são as seguintes:
   - Começar com `=` indica correspondência exata.
   - Começar com `^~` indica que o URL começa com uma string regular e não é para correspondência regex.
   - Começar com `~` indica correspondência regex com distinção entre maiúsculas e minúsculas.
   - Começar com `~*` indica correspondência regex que não diferencia maiúsculas de minúsculas.
   - `/` indica correspondência genérica, onde todas as solicitações serão correspondidas se não houver outras correspondências.

### Descrição de correspondência do caminho do URL encaminhado
![](https://main.qcloudimg.com/raw/6399b39845c9f23adccb90089e10bade.jpg)
1. Regras de correspondência: com base na correspondência de prefixo mais longo, a correspondência exata é realizada primeiro, seguida pela correspondência difusa.
Por exemplo, após a configuração das regras e os grupos de encaminhamento conforme mostrado acima, as solicitações a seguir serão combinadas em diferentes regras de encaminhamento em sequência.
 1. Como `example.qloud.com/test1/image/index1.html` corresponde exatamente à regra de URL configurada pelo grupo de encaminhamento 1, a solicitação será encaminhada ao servidor de back-end associado ao grupo de encaminhamento 1, ou seja, a porta 80 do CVM1 e CVM2 na figura.
 2. Como `example.qloud.com/test1/image/hello.html` não tem correspondência exata, ele corresponderá à regra de encaminhamento 2 com base na correspondência de prefixo mais longo; portanto, a solicitação será encaminhada aos servidores de back-end associados à regra de encaminhamento 2, ou seja, a porta 81 do CVM2 e CVM3 na figura.
 3. Como `example.qloud.com/test2/video/mp4/` não tem correspondência exata, ele corresponderá à regra de encaminhamento 3 com base na correspondência de prefixo mais longo; portanto, a solicitação será encaminhada para o servidor de back-end associado à regra de encaminhamento 3, ou seja, a porta 90 do CVM4 na figura. 
 4. Como `example.qloud.com/test3/hello/index.html` não tem correspondência exata, ele corresponderá ao URL padrão do diretório raiz `example.qloud.com/` pela correspondência de prefixo mais longo. Nesse caso, o Nginx encaminhará a solicitação para o servidor de back-end, como FastCGI (php) ou Tomcat (jsp), já o Nginx existirá como um servidor proxy reverso.
 5. Como `example.qloud.com/test2/` não tem correspondência exata, ele corresponderá ao URL padrão do diretório raiz `example.qloud.com/` pela correspondência de prefixo mais longo.
2. Se o serviço não funcionar corretamente nas regras de URL definidas, ele não será redirecionado para outras páginas após a correspondência bem-sucedida.
Por exemplo, o cliente solicita `example.qloud.com/test1/image/index1.html` e o corresponde com o grupo de encaminhamento 1. No entanto, o servidor de back-end do grupo de encaminhamento 1 tem uma exceção e uma página de erro 404 é exibida. Você verá a página de erro 404, mas não será redirecionado para outras páginas.
3. É recomendável apontar o URL padrão para uma página estável (como uma página estática ou página inicial) e vinculá-lo a todos os servidores de back-end. Se nenhuma das regras corresponder, o sistema apontará a solicitação para a página URL padrão; caso contrário, um erro 404 pode ocorrer.
4. Se você não definir o URL padrão e nenhuma das regras de encaminhamento corresponder, um erro 404 será retornado quando você acessar o serviço.
5. Observe a barra "/" no final do caminho do URL da camada 7: se o URL que você definiu terminar com `/`, mas a solicitação de acesso do cliente não contiver `/`, então a solicitação será redirecionada para um fim de regra com `/` (redirecionamento 301).
Por exemplo, no listener `HTTP: 80`, o nome de domínio configurado é `www.test.com`:
 1. Se o URL definido sob este nome de domínio for `/abc/`:
     - Quando o cliente acessar `www.test.com/abc`, ele será redirecionado para `www.test.com/abc/`.
     - Quando o cliente acessar `www.test.com/abc/`, ele corresponderá `www.test.com/abc/`.
 2. Se o URL definido sob este nome de domínio for `/abc`:
     - Quando o cliente acessar `www.test.com/abc`, ele corresponderá `www.test.com/abc`.
     - Quando o cliente acessar `www.test.com/abc/`, ele também corresponderá `www.test.com/abc`.

## Descrição da configuração da verificação de integridade da camada 7
### Regras de configuração de nomes de domínio de verificação de integridade
Um nome de domínio de verificação de integridade é o nome de domínio usado pelo CLB da camada 7 para detectar o status de integridade de um servidor de back-end.
- Limite de comprimento: 1 a 80 caracteres.
- Padrão: nome de domínio encaminhado.
- O regex não é aceito. Se o seu nome de domínio encaminhado for um nome de domínio curinga, você deve especificar um fixo (não regex).
- Os conjuntos de caracteres válidos incluem `a-z`, `0-9`, `.`, `-` e `_`. Por exemplo, `www.example.qcould.com`.

### Regras de configuração do caminho de verificação de integridade
Um caminho de verificação de integridade é o caminho do URL usado pelo CLB da camada 7 para detectar o status de integridade de um servidor de back-end.
- Limite de comprimento: 1 a 200 caracteres.
- Padrão: `/`. Você pode inserir um caminho personalizado começando com /.
- O regex não é aceito. É recomendável especificar um URL fixo (página estática) para verificação de integridade.
- Os conjuntos de caracteres válidos incluem `a-z`, `A-Z`, `0-9`, `.`, `-`, `_`, `/`, `=`, `?` e `:`. Por exemplo, `/index`.
