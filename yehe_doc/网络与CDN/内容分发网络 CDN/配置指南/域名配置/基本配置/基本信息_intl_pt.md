## Visão geral das configurações

Para as empresas que foram conectadas ao CDN do Tencent Cloud, é possível visualizar informações como a hora de criação do nome de domínio, o nome de domínio do CNAME correspondente, a região de aceleração, o projeto, o tipo de serviço e os protocolos aceitos no módulo de informações básicas do nome de domínio. Também é possível modificar informações como a região de aceleração, o tipo de serviço e o projeto, conforme necessário.

## Guia de configuração

### Exibição de informações básicas

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. As informações básicas do nome de domínio estão na guia **Basic Configuration (Configurações básicas)**.
![](https://main.qcloudimg.com/raw/5b6d2f8572ba022c5a18bb787953b1d0.png)



### Modificação da região de aceleração de nome de domínio

Clique em **Modify (Modificar)** à direita da região de aceleração para alterá-la.
- Se um nome de domínio estiver configurado para a aceleração global, as solicitações serão programadas para o nó de cache do CDN global mais próximo. Em geral, os nós dentro e fora da China Continental atendem aos usuários dentro e fora da China Continental, respectivamente.
- Se um nome de domínio estiver configurado para a aceleração na China Continental, as solicitações de acesso de usuários globais serão atendidas por nós de cache na China Continental.
- Se um nome de domínio estiver configurado para a aceleração fora da China Continental, as solicitações de acesso de usuários globais serão atendidas por nós de cache fora da China Continental.



> ! Os serviços de aceleração dentro e fora da China Continental são faturados separadamente com preços diferentes. Para obter mais informações, [clique aqui](https://intl.cloud.tencent.com/document/product/228/2949).


### Modificação do projeto

Clique em **Modify (Modificar)** à direita do projeto de nome de domínio para alterá-lo.


> !
> - Observe que a modificação do projeto mudará as estatísticas baseadas no projeto e as permissões de subusuário. Modifique com cuidado.
> - Para criar um projeto ou gerenciar projetos existentes, acesse a página [Gerenciamento de projetos](https://console.cloud.tencent.com/project).






### Modificação do tipo de serviço

O CDN do Tencent Cloud otimiza o desempenho de aceleração com base no tipo de serviço. Para obter o melhor resultado de aceleração, recomendamos escolher o tipo de serviço semelhante ao da sua empresa real. Se você quiser ajustar, clique em **Modify (Modificar)** à direita:


> !
> - A modificação do tipo de serviço mudará a plataforma de aceleração do CDN subjacente, o que pode causar uma pequena quantidade de solicitações com falha e aumentar a largura de banda de pull de origem. Recomendamos modificar o tipo de serviço fora do horário de pico.
> - Se você não conseguir encontrar o botão **Modify (Modificar)** ao lado do seu nome de domínio, [entre em contato conosco](https://intl.cloud.tencent.com/zh/contact-sales) para obter ajuda.

### Modificação do acesso IPv6
Acione o botão de acesso IPv6 para ativá-lo ou desativá-lo. Os nós do CDN poderão ser acessados pelo protocolo IPv6 depois que o acesso IPv6 for ativado.

>! 
>- Algumas plataformas estão sendo atualizadas; o acesso IPv6 não é compatível no momento. Fique atento ao lançamento oficial.
>- O acesso IPv6 está disponível apenas na China Continental. Para nomes de domínio de aceleração global, se o acesso IPv6 for ativado, ele terá efeito apenas na China Continental. Não é possível ativá-lo para nomes de domínio com aceleração fora da China Continental.
>- Para nomes de domínio de aceleração global com acesso IPv6 ativado, se a região de aceleração for trocada para regiões fora da China Continental, o acesso IPv6 será desativado automaticamente e não poderá ser ativado.


