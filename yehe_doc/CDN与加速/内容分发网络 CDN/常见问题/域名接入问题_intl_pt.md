[](id:q1)
### Como eu conecto um nome de domínio?
Você pode conectar um nome de domínio no console do CDN. Para obter mais informações, consulte [Adição de nomes de domínio](https://intl.cloud.tencent.com/document/product/228/5734).

[](id:q2)
### Existem requisitos para conectar um nome de domínio ao CDN?
Sim. Veja abaixo os requisitos para conectar um nome de domínio ao CDN:
1. A extensão do nome de domínio não pode exceder 81 caracteres.
2. O nome de domínio deve ter um registro de ICP emitido pelo MIIT.
3. O nome de domínio é um nome de subdomínio no formato `a.test.com` ou `a.b.test.com` ou um nome de domínio curinga no formato `*.test.com` ou `*.a.test.com`.
4. A verificação da propriedade do nome de domínio é requerida ao conectar um nome de domínio pela primeira vez, seja ele curinga ou conectado.

[](id:q3)
### O CDN aceita a conexão de nomes de domínio curinga?
Sim, o CDN aceita a conexão de nomes de domínio curinga, para os quais é necessária a verificação de propriedade do nome de domínio. Uma vez verificados, os nomes de domínio podem ser conectados ou recuperados.
Além disso:
1. Se um nome de domínio curinga, como `*.test.com` já estiver conectado à Tencent Cloud, nenhum de seus nomes de subdomínio poderá ser conectado a outra conta.
2. Se o nome de domínio curinga `*.test.com` já estiver conectado à sua conta, então nomes de domínio curinga em formatos como `*.path.test.com` não podem ser conectados à sua conta.

[](id:q4)
### Quanto tempo leva para configurar o CDN?
Em geral, leva menos de 30 minutos para que a configuração do CDN entre em vigor. Se a configuração não entrar em vigor em 30 minutos, você pode [enviar um tíquete](https://console.cloud.tencent.com/workorder/category) para obter ajuda.

[](id:q5)
### Posso configurar vários IPs de servidor de origem?
Sim. Depois de configurar vários IPs, o CDN acessará aleatoriamente um dos IPs ao encaminhar uma solicitação ao servidor de origem. Se o número de falhas de pull de origem com este IP exceder o limite, ele será isolado por 300 segundos por padrão, durante os quais nenhuma solicitação de pull de origem será encaminhada ao IP.

[](id:q6)
### Como eu vinculo o CNAME a um nome de domínio depois que o nome de domínio for conectado ao CDN?
Consulte [Configuração do CNAME](https://intl.cloud.tencent.com/document/product/228/3121) para saber como vincular o CNAME ao seu provedor de serviço de DNS.

[](id:q7)
### Por que um nome de domínio pode ser desabilitado, mas não excluído?
Verifique se o usuário é um colaborador. A permissão do colaborador é configurada pelo criador do serviço CDN. Se o criador não atribuir a permissão relevante ao colaborador, o colaborador não poderá realizar a operação. Se você tiver certeza de que o colaborador recebeu a permissão, mas ainda não consegue realizar a operação, [envie um tíquete](https://console.cloud.tencent.com/workorder/category) para obter ajuda.

[](id:q8)
### A configuração do nome de domínio será mantida após o serviço de aceleração ser desabilitado?
Sim. Depois que o serviço de aceleração for desabilitado, a configuração do nome de domínio será mantida, mas o serviço de aceleração não estará mais disponível. Nesse caso, um código de status 404 será retornado para solicitações do usuário.

[](id:q9)
### A configuração do nome de domínio será mantida depois que um nome de domínio de aceleração for excluído?
Não. Depois que um nome de domínio for excluído, sua configuração não será mantida.

[](id:q10)
### Como eu desabilito o serviço de aceleração?
Você pode desabilitar o serviço de aceleração no console do CDN. Para obter instruções detalhadas, consulte "Desabilitação do serviço de aceleração" em [Operações de nomes de domínio](https://intl.cloud.tencent.com/document/product/228/5736).

[](id:q11)
### Como eu excluo um nome de domínio de aceleração?
Você pode excluir um nome de domínio de aceleração no console do CDN. Para obter instruções detalhadas, consulte "Exclusão de nomes de domínio de aceleração" em [Operações de nomes de domínio](https://intl.cloud.tencent.com/document/product/228/5736).

[](id:q12)
### Como eu desbloqueio um nome de domínio?
[Envie um tíquete](https://console.cloud.tencent.com/workorder/category) para obter ajuda.

[](id:q13)
### Quais tipos de negócios o CDN aceita?
O tipo de serviço selecionado determina qual plataforma de recursos é usada pelo nome de domínio. As configurações de aceleração variam de acordo com as plataformas de recursos. Escolha o tipo de serviço que corresponde à sua empresa:
- Aceleração estática: adequada para cenários de aceleração de recursos estáticos, como comércio eletrônico, sites e imagens de jogos.
- Aceleração de download: adequada para cenários como instalações de jogos, downloads de áudio/vídeo e distribuição de pacote de firmware de celular.
- Aceleração de streaming de VOD: adequada para cenários de aplicações como aceleração de VOD de áudio/vídeo.

[](id:q14)
### Como eu modifico o projeto de um nome de domínio no CDN?

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, clique em **Manage (Gerenciar)** à direita de um nome de domínio, abra a guia **Basic Configuration (Configuração básica)** e modifique o projeto do nome de domínio. Para modificar os projetos de vários nomes de domínio em lotes, marque os nomes de destino na página **Domain Management (Gerenciamento de domínio)**, clique na lista suspensa **More Actions (Mais ações)** e selecione **Edit Project (Editar projeto)**. É possível operar até 50 nomes de domínio ao mesmo tempo.

>!Os usuários no sistema de permissões do CDN devem proceder com cuidado, pois essa operação pode causar alterações nas permissões dos subusuários.


[](id:m1)
### Meu nome de domínio já obteve um registro de ICP do MIIT. Por que o sistema avisa que o nome de domínio não possui um registro de ICP quando tento conectá-lo ao CDN?
Depois de obter seu registro de ICP, leva algum tempo para sincronizar as informações do MIIT para o CDN da Tencent Cloud. Aguarde 24 horas e tente novamente.

[](id:q16)
### Posso configurar portas para nomes de domínio de aceleração ou servidores de origem?
- Porta de nome de domínio de aceleração do CDN: atualmente, as portas de aceleração do CDN podem ser apenas 80, 443 e 8080.
- Porta do servidor de origem: as portas de 1 a 65535 podem ser configuradas após o endereço do servidor de origem.

[](id:q17)
### O que é a configuração do domínio de origem do CDN?
Domínio de origem é o nome de domínio do site acessado no servidor de origem durante o pull de origem em um nó do CDN. Servidor de origem e domínio de origem: o IP ou nome de domínio configurado no servidor de origem permite que um nó do CDN encontre o servidor de origem correspondente durante o pull de origem. Pode haver vários sites no servidor, e o domínio de origem indica em qual site um recurso está localizado.

[](id:q18)
### Como posso saber se o CDN entrou em vigor?

Você pode executar o comando `nslookup` para consultar a resolução DNS do seu nome de domínio de aceleração do CDN. Se o nome de domínio do resultado da resolução tiver o sufixo `dnsv1.com` (o registro CNAME) conforme mostrado na imagem, isso indica que o serviço de aceleração do CDN para seu nome de domínio entrou em vigor.
![](https://main.qcloudimg.com/raw/4576b46fd8a04b726e6893a08f3fe61f.png)


[](id:q19)
### O que eu devo fazer se não for possível baixar os arquivos do CDN?

Se não for possível baixar os arquivos do CDN, recomendamos solucionar o problema pelos seguintes métodos:
1. Verifique se é possível baixar normalmente os arquivos do servidor de origem.
2. Verifique se o nome de domínio está configurado corretamente no console do CDN (consulte o domínio de origem na guia **Basic Configuration (Configuração básica)**). Certifique-se de que o domínio de origem configurado pode ser acessado corretamente. Caso contrário, o pull de origem pode falhar, o que afetará sua empresa.
Verifique se a falha do pull de origem é causada pela política de segurança configurada no servidor de origem e, em caso afirmativo, [entre em contato conosco](https://intl.cloud.tencent.com/support) para obter o intervalo de IP intermediário e adicionar o servidor de origem à lista de permissões.

[](id:q20)
### O que eu devo fazer se não conseguir fazer login no back-end do WordPress depois que a aceleração do CDN for configurada?
O WordPress envolve solicitações dinâmicas. Se a configuração do cache for inadequada, podem ocorrer exceções de login. Recomendamos definir a validade do cache do tipo de arquivo dinâmico correspondente como 0, para que os arquivos desse tipo não sejam armazenados em cache automaticamente. Os tipos de arquivos dinâmicos comuns incluem .asp, .jsp, .php, .perl e .cgi. Para obter instruções detalhadas, consulte [Configuração de validade do cache do nó (Herdada)](https://intl.cloud.tencent.com/document/product/228/35317).


