[//]: # (chinagitpath:XXXXX)

### Protobuf

O Protocol Buffers do Google (Protobuf) é um formato de armazenamento de dados estruturados leve e eficiente desenvolvido pelo Google para a serialização de dados estruturados. É adequado para armazenamento de dados ou troca de dados de RPC. O TcaplusDB define estruturas de tabelas e serializa registros de dados por meio do Protobuf.

### Tabela do TcaplusDB

Para as tabelas utilizadas para armazenamento de dados, a estrutura é definida utilizando o arquivo Protobuf que está alinhado à semântica do TcaplusDB. 
### Aplicativo

É a unidade de aplicativo do TcaplusDB, que corresponde ao aplicativo do jogo. O AppID é exibido na página de informações de configuração, e é usado como um parâmetro de conexão para a tabela de conexões SDK do TcaplusDB.

### AppKey

É a chave da unidade de aplicativo do TcaplusDB. A AppKey é exibida na página de informações de configuração, e é usada como um parâmetro de conexão para a tabela de conexões SDK do TcaplusDB.

### Unidade de implantação (zona)

É a unidade de implantação de dados dentro de uma unidade de aplicativo do TcaplusDB, que pode ser interpretada como uma zona. Várias zonas podem ser criadas em um aplicativo, e tabelas com o mesmo nome devem ser criadas em zonas diferentes. O ZoneID é exibido na coluna **Deployment Unit (Unidade de implantação)** da lista e é usado como um parâmetro de conexão para a tabela de conexões SDK do TcaplusDB.

### Acesso pela rede do VPC

O ponto de acesso do serviço de diretório do TcaplusDB é a entrada para os usuários acessarem as tabelas do TcaplusDB por meio do SDK do Tcaplus. A URL de rede do VPC é exibida na página de informações de configuração, e é usada como um parâmetro de conexão para a tabela de conexões SDK do TcaplusDB.





