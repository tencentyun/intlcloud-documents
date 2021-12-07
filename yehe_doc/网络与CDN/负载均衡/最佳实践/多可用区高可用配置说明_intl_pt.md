## Implementação de HA em várias AZs
A instância do CLB oferece suporte à recuperação de desastres em zonas de disponibilidade. Por exemplo, vários clusters podem ser implantados em duas zonas de disponibilidade na mesma região: Zona 1 de Hong Kong (China) e Zona 2 de Hong Kong (China). Isso resulta na recuperação de desastres em zonas de disponibilidade na mesma região. Com esse recurso, uma instância do CLB pode encaminhar o tráfego de acesso de front-end para outras zonas de disponibilidade na mesma região em 10 segundos se toda a zona de disponibilidade falhar, restaurando a capacidade do serviço.

## Perguntas frequentes e casos de uso
#### Pergunta 1: Se a instância `test1` do CLB estiver configurada para Zona 1 e Zona 2 de Hong Kong (China), qual é a política para o tráfego de entrada em rede pública do cliente?
As Zonas 1 e 2 de Hong Kong (China) têm um par de pools de recursos IP, que podem ser vistos como recursos IP com capacidade de balanceamento de carga equivalente. Os desenvolvedores não precisam discernir entre o cluster mestre e o cluster escravo. Quando eles compram uma instância do CLB e a vinculam ao CVM, dois conjuntos de regras são gerados e gravados nos dois clusters, alcançando alta disponibilidade.

#### Pergunta 2: Suponha que a instância test1 do CLB esteja configurada para as zonas 1 e 2 de Hong Kong (China) e vinculada a 100 servidores de back-end em cada zona de disponibilidade. Durante a operação comercial, 1 milhão de conexões persistentes HTTP (com a conexão TCP mantida ativa) são estabelecidas em cada zona. Se todo o cluster CLB na Zona 1 falhar e ficar indisponível, o que acontecerá com o negócio?
Quando a instância do CLB na Zona 1 de Hong Kong (China) falhar, todas as conexões persistentes atuais serão fechadas, enquanto as conexões não persistentes não serão afetadas. A arquitetura de recuperação de desastres ligará automaticamente os 100 servidores em cada zona à instância do CLB na Zona 2 de Hong Kong (China) em 10s, restaurando imediatamente a capacidade do negócio sem a necessidade de intervenção manual.

#### Pergunta 3: Que tipo de CLB é compatível com a recuperação de desastres multi-AZ? São cobradas taxas extras?
A recuperação de desastres Multi-AZ é gratuita. Este recurso está disponível para instâncias do CLB de rede pública e privada, exceto para instâncias do CLB de rede privada criadas em Guangzhou antes de 29 de abril de 2020, em Xangai antes de 19 de dezembro de 2019 e em Pequim antes de 18 de dezembro de 2019.

