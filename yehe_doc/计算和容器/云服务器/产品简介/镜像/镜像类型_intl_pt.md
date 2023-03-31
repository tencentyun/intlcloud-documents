Você pode escolher uma imagem com base nos seguintes atributos:
- Localização (consulte as [Regiões e zonas de disponibilidade](https://intl.cloud.tencent.com/document/product/213/6091))
- Sistema operacional
- Arquitetura (32 bits ou 64 bits)

O Tencent Cloud fornece três tipos de imagens, imagens puramente públicas, imagens personalizadas e imagens compartilhadas.

## Imagens públicas
As **imagens públicas** são imagens fornecidas pelo Tencent Cloud. Cada imagem contém um sistema operacional e componentes de inicialização fornecidos pelo Tencent Cloud, e está disponível a todos os usuários.

Funcionalidades:
 - **Sistema operacional:** você pode escolher um sistema operacional de preferência, como o Linux ou o Windows. Os sistemas operacionais são atualizados regularmente.
 - **Software:** as imagens públicas são integradas com pacotes de software fornecidos pelo Tencent Cloud e aceitam várias versões de software com todas as permissões, como Java, MySQL, SQL Server, Python, Ruby e Tomcat.
 - **Segurança:** todos os sistemas operacionais fornecidos são licenciados. Todas as imagens são criadas pela equipe de segurança e de operações do Tencent Cloud, e são rigorosamente testadas. Os componentes de segurança do Tencent Cloud também estão disponíveis.
 - **Limite:** nenhum.
 - **Taxas:** todas as imagens públicas são gratuitas, exceto as imagens do Windows em algumas regiões fora da China continental, em que uma taxa de licença pode ser cobrada.
 - **Suporte técnico:**
  - O Tencent Linux é fornecido e mantido pelo Tencent Cloud.
  - Para questões envolvendo imagens de terceiros, entre em contato com a comunidade open-source ou com o fornecedor do sistema operacional. O Tencent Cloud fornecerá assistência técnica durante o processo de solução de problemas, se necessário.



## Imagens personalizadas
As **imagens personalizadas** são feitas pelos usuários usando a funcionalidade de criação ou importadas por meio da funcionalidade de importação. As imagens personalizadas só estão disponíveis aos criadores e às pessoas com quem eles compartilham.

Funcionalidades:
 - **Caso de uso:** uma imagem criada a partir de uma instância do CVM com aplicativos implantados pode ser usada para criar rapidamente mais instâncias que contenham a mesma configuração.
 - **Funcionalidades:** você pode criar, copiar, compartilhar e encerrar imagens.
 - **Limitação:** cada região suporta apenas um máximo de 10 imagens personalizadas.
 - **Taxas:** a criação de imagens pode gerar custos. Para saber o custo real, consulte o preço apresentado ao criar a imagem. A replicação da imagem personalizada entre regiões é gratuita.

Para obter mais informações sobre imagens personalizadas, consulte [Criação de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4942), [Cópia de imagens](https://intl.cloud.tencent.com/document/product/213/4943), [Compartilhamento de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4944), [Cancelamento do compartilhamento de imagens](https://intl.cloud.tencent.com/document/product/213/7148) e [Importação de imagens](https://intl.cloud.tencent.com/document/product/213/4945).

## Imagens compartilhadas
As **imagens compartilhadas** são imagens personalizadas compartilhadas com você por outro usuário do Tencent Cloud, usando a funcionalidade de compartilhamento de imagens.
Essas imagens são exibidas na mesma região que as imagens originais.

Funcionalidades:
 - **Caso de uso:** ajuda outros usuários a criar rapidamente uma instância do CVM.
 - **Funcionalidades:** a imagem compartilhada só pode ser usada para criar instâncias do CVM. Não é permitido renomear, copiar ou recompartilhar a imagem com outras pessoas.
 - **Segurança**: as imagens compartilhadas não são verificadas pelo Tencent Cloud, o que pode representar riscos à segurança. Recomendamos fortemente que não utilize imagens de fontes desconhecidas.
 - **Limitações**: cada imagem personalizada pode ser compartilhada com um máximo de 50 usuários do Tencent Cloud. As imagens personalizadas só podem ser compartilhadas com contas na mesma região que a conta de origem.

Para obter mais informações acerca das imagens compartilhadas, consulte [Compartilhamento de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4944) e [Cancelamento do compartilhamento de imagens](https://intl.cloud.tencent.com/document/product/213/7148).


