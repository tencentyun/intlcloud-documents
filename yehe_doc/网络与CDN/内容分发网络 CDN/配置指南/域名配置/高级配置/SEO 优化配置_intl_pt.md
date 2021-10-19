## Visão geral
A configuração do SEO é uma funcionalidade que soluciona o problema de pesos incorretos para pesquisas de nomes de domínio, devido às mudanças frequentes de IP pelo CDN depois que um nome de domínio é conectado ao CDN. Ao identificar se um IP de acesso pertence a um mecanismo de pesquisa, é possível optar por efetuar pull do recurso diretamente do servidor de origem, garantindo a estabilidade dos pesos do mecanismo de pesquisa.

> !
> - Como os IPs do mecanismo de pesquisa são alterados com frequência, o CDN do Tencent Cloud só consegue garantir que a maioria, mas nem todos os IPs, possam ser identificados.
> - A funcionalidade de configuração do SEO fica disponível apenas quando o nome de domínio conectado é **próprio**. Depois que essa funcionalidade for ativada, se um nome de domínio tiver vários endereços de servidor de origem, o primeiro será o endereço de pull de origem padrão.

## Guia de configuração

### Visualização da configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Você encontrará a configuração do SEO na guia **Advanced Configuration (Configuração avançada)**. Por padrão, ela fica desativada:
![](https://main.qcloudimg.com/raw/44f35a715f922cda12191d50e1cfc723.png)

### Modificação da configuração
Você pode ativar o botão de alternância para ativar ou desativar a configuração do SEO:
![](https://main.qcloudimg.com/raw/8ea737dbd456397286f3ef8ff965aaf2.png)

>!  Atualmente, a funcionalidade de configuração do SEO não está disponível em regiões fora da China Continental. Se a região de aceleração do seu nome de domínio estiver fora da China Continental, essa funcionalidade não pode ser ativada. Se o seu nome de domínio estiver configurado para a aceleração global, a configuração do SEO terá efeito apenas na China Continental.

