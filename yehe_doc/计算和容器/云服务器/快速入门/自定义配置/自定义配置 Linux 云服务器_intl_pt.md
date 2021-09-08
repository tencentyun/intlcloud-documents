A configuração personalizada oferece mais plataformas de imagens e configurações avançadas para armazenamento, largura de banda e grupo de segurança. É possível selecionar o modo de configuração conforme necessário. Este documento usa a configuração personalizada como exemplo.

## Registro e verificação

Antes de usar um CVM, é necessário realizar as seguintes operações:
1. Crie uma conta do Tencent Cloud e conclua a verificação de identidade.
Um novo usuário precisa [criar](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F) uma conta no site do Tencent Cloud. Para obter detalhes, consulte a [Criação de conta do Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985).
2. Acesse a página de [Introdução ao Tencent CVM](https://intl.cloud.tencent.com/product/cvm) e clique em **Get Started (Começar a usar)**.

<span id="SelectType"></span>
## Seleção de um modelo de dispositivo

1. Configure as seguintes informações conforme solicitado pela página:
![Selecione a região e o modelo](https://main.qcloudimg.com/raw/07493412dd043911fe8aa3ecb0d0bcd4.png)
<table>
<tr><th style="width: 20%">Categoria</th><th style="width: 12%">Obrigatória/Opcional</th><th>Descrição da configuração</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/213/2180">Modo de faturamento</a></td><td>Obrigatório</td><td><ul><li><b>Pagamento conforme o uso</b>: um modo de faturamento elástico para o CVM.</li></ul></td></tr>
<tr><td>Região</td><td>Obrigatória</td><td>Recomendamos que você selecione uma região mais próxima do seu cliente para reduzir a latência de acesso e aumentar a velocidade de acesso.</td></tr>
<tr><td>Zona de disponibilidade</td><td>Obrigatória</td><td>Selecione uma zona de disponibilidade conforme necessário.</br>Se você deseja adquirir vários CVMs, recomendamos que selecione zonas de disponibilidade diferentes para implementar a recuperação de desastres.</td></tr>
<tr><td>Rede</td><td>Obrigatória</td><td>Um espaço de rede isolado logicamente criado no Tencent Cloud. Um Virtual Private Cloud (VPC) inclui pelo menos uma sub-rede. O sistema fornece um VPC e uma sub-rede padrão para cada região.</br>
Se o VPC ou a sub-rede atual não atender aos seus requisitos, é possível criar um VPC ou uma sub-rede no console do VPC.</br><b>Observação</b>:<ul><li>os recursos no mesmo VPC podem ser compartilhados na rede privada.</li><li>Ao adquirir o CVM, certifique-se de que ele e a sub-rede na qual o CVM foi criado tenham as mesmas zonas de disponibilidade.</li></ul></td></tr>
<tr><td>Instância</td><td>Obrigatória</td><td>O Tencent Cloud disponibiliza tipos de instância diferentes com base no hardware subjacente. Para obter o desempenho ideal, recomendamos que você use os tipos de instância da última geração.</br>Para obter mais informações sobre as instâncias, consulte os <a href="https://intl.cloud.tencent.com/document/product/213/11518">Tipos de instâncias</a>.</td></tr>
<tr><td>Imagem</td><td>Obrigatória</td><td>O Tencent Cloud fornece imagens públicas, imagens personalizadas e imagens compartilhadas. Para obter mais informações sobre imagens, consulte a <a href="https://intl.cloud.tencent.com/document/product/213/4941">Visão geral dos tipos de imagens</a>.</br>Se você acabou de começar a usar o Tencent Cloud, recomendamos que escolha as imagens públicas.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">Disco do sistema</a></td><td>Obrigatório</td><td>Usado para instalar o sistema operacional. Sua capacidade padrão é 50 GB.</br>Os tipos de Cloud Block Storage (CBS) disponíveis variam com as regiões. Selecione um valor conforme as instruções da página.</br>Para obter mais informações sobre o CBS, consulte os <a href="https://intl.cloud.tencent.com/document/product/362/31636">Tipos de CBS</a>.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">Disco de dados</a></td><td>Opcional</td><td>Usado para aumentar a capacidade de armazenamento do CVM, para garantir alta eficiência e confiabilidade. Por padrão, os discos de dados do CBS não são adicionados.</br>Para obter mais informações sobre o CBS, consulte os <a href="https://intl.cloud.tencent.com/document/product/362/31636">Tipos de CBS</a>.</td></tr>
<tr><td>Largura de banda da rede pública</td><td>Obrigatória</td><td>O Tencent Cloud oferece dois modos de faturamento de rede. Defina um valor conforme necessário.<ul><li><b>Faturamento por largura de banda</b>: selecione uma largura de banda fixa. A perda de pacotes ocorrerá quando a largura de banda exceder este valor. Isso se aplica a cenários em que a conexão de rede flutua ligeiramente.</li><li><b>Faturamento por tráfego</b>: o faturamento é baseado no tráfego realmente usado. É possível especificar uma largura de banda de pico para evitar cobranças decorrentes de tráfego inesperado. A perda de pacotes ocorrerá quando a largura de banda instantânea exceder esse valor. Isso se aplica a cenários em que a conexão de rede flutua significativamente.</li></ul></td></tr>
<tr><td>Gateway público</td><td>Opcional</td><td>Como uma interface de rede entre o VPC e a rede pública, o gateway público pode encaminhar solicitações de CVMs que estão em sub-redes diferentes do VPC e não têm endereços IP públicos. </br><b>Observação:</b> o Tencent Cloud descontinuou a configuração do gateway público na página de aquisição do CVM após 6 de dezembro de 2019. Para configurar o gateway público, consulte a <a href="https://cloud.tencent.com/document/product/213/34835">Configuração de um gateway público</a>.</td></tr> 
<tr><td>Quantidade</td><td>Obrigatória</td><td>Quantidade de CVMs a serem adquiridos.</td></tr>
</table>
2. Clique em **Next: Complete Configuration (Avançar: concluir a configuração)** para acessar a página de configuração do CVM.

## Configuração do CVM
1. Configure as seguintes informações conforme solicitado pela página:
![Grupo de segurança e CVM](https://main.qcloudimg.com/raw/44493e285aee4d9523e009b7690fc616.png)
<table>
<tr><th style="width: 20%">Categoria</th><th style="width: 12%">Obrigatória/Opcional</th><th>Descrição da configuração</th></tr>
<tr><td>Projeto</td><td>Obrigatório</td><td>O projeto padrão é selecionado. É possível selecionar um projeto existente conforme necessário para gerenciar diferentes CVMs.</td></tr>
<tr><td>Grupo de segurança</td><td>Obrigatório</td><td>Usado para configurar as políticas de acesso à rede para um ou mais CVMs.</br><b>Certifique-se de que a porta de login 22 esteja aberta.</b>Para obter mais informações, consulte os <a href="https://intl.cloud.tencent.com/document/product/213/12452">Grupos de segurança</a>.</td></tr>
<tr><td>Nome da instância</td><td>Opcional</td><td>O nome do CVM a ser criado.</br>É definido pelo usuário. Recomendamos <b>CVM-01</b>.</td></tr>
<tr><td>Método de login</td><td>Obrigatório</td><td>Configure o método para fazer login no CVM conforme necessário.<ul><li><b>Senha personalizada</b>: personalize a senha para fazer login na instância.</li><li><b>Par de chaves SSH</b>: associe a instância a uma chave SSH para garantir um login seguro no CVM.</br>Se nenhuma chave estiver disponível ou as chaves existentes forem inadequadas, clique em <b>Create Now (Criar agora)</b> para criar uma chave. Para obter mais informações sobre chaves SSH, consulte as <a href="http://cloud.tencent.com/doc/product/213/SSH%E5%AF%86%E9%92%A5">Chaves SSH</a>.</li><li><b>Senha aleatória</b>: uma senha gerada automaticamente será enviada pelo<a href="https://console.cloud.tencent.com/message">Centro de mensagens</a>.</li></ul></td></tr>
<tr><td>Serviço de segurança</td><td>Opcional</td><td>Por padrão, o serviço de segurança é habilitado gratuitamente para ajudar você a criar um sistema de segurança do CVM, para evitar o vazamento de dados.</td></tr>
<tr><td>Monitoramento em nuvem</td><td>Opcional</td><td>Por padrão, o monitoramento em nuvem é habilitado gratuitamente. Ele fornece monitoramento abrangente de dados do CVM, análise de dados inteligente, alarmes de falha em tempo real e relatórios de dados personalizados para monitorar com precisão os serviços do Tencent Cloud e as condições de integridade dos CVMs.</td></tr>
<tr><td>Configurações avançadas</td><td>Opcional</td><td>Defina configurações adicionais para a instância conforme necessário.<ul><li><b>Nome do host</b>: é possível personalizar o nome do computador no sistema operacional do CVM. Depois que um CVM é criado, você pode fazer login no CVM para visualizar o nome do host.</li><li><b>Função do CAM</b>: é possível definir uma função e usá-la para conceder à entidade de função as permissões para acessar os serviços e recursos do CVM e realizar operações no Tencent Cloud. Para obter mais informações sobre as configurações, consulte o <a href="https://intl.cloud.tencent.com/document/product/213/38290">Gerenciamento de funções</a>.</li><li><b>Grupo de posicionamento</b>: é possível adicionar uma instância a um grupo de posicionamento, conforme necessário, para melhorar a disponibilidade do serviço. Para obter mais informações, consulte o <a href="https://intl.cloud.tencent.com/document/product/213/15486">Grupo de posicionamento</a>.</li><li><b>Tag</b>: é possível especificar uma tag para gerenciar recursos do CVM por categoria. Para obter mais informações, consulte o <a href="https://intl.cloud.tencent.com/document/product/213/19548">Guia do usuário sobre tags</a>.</li><li><b>Dados personalizados</b>: é possível configurar uma instância especificando dados personalizados, e os scripts configurados serão executados quando uma instância for iniciada. Se vários CVMs forem adquiridos juntos, os dados personalizados serão executados em todos os CVMs. O sistema operacional Linux aceita o formato Shell e um máximo de 16 KB de dados brutos. Para obter detalhes, consulte a <a href="https://intl.cloud.tencent.com/document/product/213/17525">Configuração de dados personalizados (CVM do Linux)</a>.</br><b>Observação</b>: a configuração de dados personalizados é compatível apenas com determinadas imagens comuns com o serviço cloud-init. Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/213/19670">Cloud-init e cloudbase-init</a>.</li></ul></td></tr>
</table>
2. Clique em **Next: Complete Configuration (Avançar: concluir a configuração)** para acessar a página de confirmação das informações de configuração.


## Confirmação das informações de configuração

1. Valide as informações do CVM a ser adquirido e os detalhes de custo de cada item de configuração.
2. Clique em **Purchase (Adquirir)** e conclua o pagamento. Em seguida, você pode fazer login no [Console do CVM](https://console.cloud.tencent.com/cvm) para visualizar o seu CVM.
As informações, como nome da instância, endereço IP público, endereço IP privado, nome de usuário de login e senha de login inicial do CVM serão enviadas para sua conta pelo [Centro de mensagens](https://console.cloud.tencent.com/message). Você pode usar essas informações para fazer login e gerenciar suas instâncias. Para garantir a segurança do seu CVM, altere a senha de login do CVM o mais rápido possível.

## Login e conexão da instância

Depois de concluir as operações do CVM, você pode fazer login no seu CVM no console do Tencent Cloud e realizar operações, como criar um site, conforme necessário.
Selecione um método para fazer login no CVM no console do Tencent Cloud, conforme necessário:
- [Login em uma instância do Linux usando o modo de login padrão (recomendado)](https://intl.cloud.tencent.com/document/product/213/5436)
- [Login em uma instância do Linux usando o software de login remoto](https://intl.cloud.tencent.com/document/product/213/32502).
- [Login em uma instância do Linux usando SSH](https://intl.cloud.tencent.com/document/product/213/32501)

## Particionamento e formatação do disco de dados

Se você adicionou um disco de dados ao [selecionar o tipo de instância](#SelectType), é necessário formatar e particionar o disco de dados depois de fazer login na instância do CVM. **Se você não adicionou nenhum disco de dados, pule esta etapa.**
Selecione o guia de operações adequado de acordo com a capacidade do disco e o sistema operacional do CVM.
- Para um disco menor que 2 TB:
 [Inicialização de um disco em nuvem (Linux)](https://intl.cloud.tencent.com/document/product/362/31597)
- Para um disco igual ou maior que 2 TB:
 [Inicialização de um disco em nuvem (Linux)](https://intl.cloud.tencent.com/document/product/362/31598)

> Para saber mais operações, consulte os [Cenários de inicialização](https://intl.cloud.tencent.com/document/product/362/31596).
