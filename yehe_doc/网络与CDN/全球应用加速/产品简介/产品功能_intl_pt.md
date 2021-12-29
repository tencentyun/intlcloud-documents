As principais funcionalidades do GAAP incluem configuração de proxy de aceleração, gerenciamento de servidores de origem, coleta de estatísticas sobre a aceleração, monitoramento de conexão e aquisição de IPs reais de usuários.
## Proxy de aceleração
- O GAAP permite a configuração de uma conexão de aceleração por região do usuário de destino e região do servidor de origem. Ele selecionará automaticamente a conexão mais apropriada com base na região do usuário de destino e na região do servidor de origem, a fim de obter o caminho mais curto e ideal do usuário ao servidor de origem, proporcionando uma melhor experiência de acesso. Para obter mais informações sobre configuração, consulte [Gerenciamento de acesso](https://intl.cloud.tencent.com/document/product/608/13765).
- Os encaminhamentos TCP e UDP são aceitos.
- O encaminhamento de regras de URL é aceito para HTTP e HTTPS.
- Um listener pode ser vinculado a vários servidores de origem e uma conexão pode ter vários listeners criados.
- Permite a configuração e modificação de regras de encaminhamento, que entram em vigor em tempo real e não afetam os negócios online.
- A configuração flexível das regras de encaminhamento de aceleração em uma conexão satisfaz cenários que precisam de verificação de teste beta passo a passo. Para obter mais informações sobre configuração, consulte [Gerenciamento de listener](https://intl.cloud.tencent.com/document/product/608/13764).

## Gerenciamento de servidores de origem
- O GAAP pode gerenciar uma grande quantidade de servidores de origem, cujos tipos são IP e nome de domínio, e adicioná-los em lotes.

## Coleta de estatísticas
- O GAAP pode coletar estatísticas de uma conexão de aceleração, como largura de banda, simultaneidade, perda de pacotes, atraso e volume de encaminhamento de pacotes. Com base nas estatísticas, você pode ajustar com flexibilidade o limite de capacidade de uma conexão de aceleração conforme necessário. Para obter mais informações, consulte [Estatísticas](https://intl.cloud.tencent.com/document/product/608/14425).

## Monitoramento de conexão
- O GAAP possibilita o monitoramento do status da conexão e do servidor de origem. Ele alerta você imediatamente sobre problemas de conexão ou com o servidor de origem, para uma solução mais fácil e rápida. Para obter mais informações, consulte [Monitoramento do acesso em nuvem](https://intl.cloud.tencent.com/document/product/608/17541).

## Obtenção de IPs reais de usuários
- O GAAP permite que o módulo TOA obtenha IPs reais de usuários, garantindo a passagem de IP eficaz para fins de análise de dados. Para obter mais informações, consulte [Obtenção de IPs reais de acesso de usuários](https://intl.cloud.tencent.com/document/product/608/14429).
