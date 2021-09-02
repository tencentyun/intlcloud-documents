## Visão geral de uma instância do CVM
Uma **instância** é um Cloud Virtual Machine (CVM). Ela contém componentes básicos de computação, como CPU, memória, sistema operacional, rede e disco.

As instâncias do CVM fornecem serviços de computação elásticos na nuvem de forma segura e confiável, para atender aos requisitos de computação. Conforme as demandas da empresa mudam, os recursos de computação podem ser dimensionados em tempo real, a fim de reduzir os custos de software e de hardware e simplificar o trabalho das operações de TI.

Cada tipo de instância oferece diferentes recursos de computação e de armazenamento, tornando-os adequados para diferentes casos de uso. Você pode escolher a capacidade de computação, o armazenamento e o método de acesso à rede da instância com base no escopo do serviço que você precisa fornecer. Para obter mais informações sobre os tipos de instâncias e os casos de uso, consulte os [Tipos de instâncias](https://intl.cloud.tencent.com/document/product/213/11518). Depois de iniciar uma instância, você pode usá-la como faria com um computador tradicional. Você também terá controle total sobre suas instâncias.

## Imagem da instância
Uma **imagem** é um modelo que contém configurações de software (sistemas operacionais, programas pré-instalados etc.) necessárias para iniciar as instâncias do CVM. Você pode usar uma imagem para iniciar uma instância ou várias instâncias repetidamente. Ou seja, uma imagem é o "disco instalado" do CVM.

O Tencent Cloud fornece os seguintes tipos de imagens:
 - Imagem pública: disponível para todos os usuários e adequada para os principais sistemas operacionais.
 - Imagem personalizada: disponível apenas para o criador e os usuários com quem a imagem for compartilhada. Uma imagem personalizada é criada a partir de instâncias em execução ou importada de fontes externas.
 - Imagem compartilhada: compartilhada por outros usuários. Elas só podem ser usadas para criar instâncias.

Para obter mais informações sobre as imagens, consulte a [Visão geral](https://intl.cloud.tencent.com/document/product/213/4940) ou a [Visão geral dos tipos de imagens](https://intl.cloud.tencent.com/document/product/213/4941).

## Armazenamento da instância
Assim como um CVM normal, as instâncias podem ser armazenadas no **disco do sistema** e no **disco de dados**:
Disco do sistema: semelhante à unidade C do sistema Windows. O disco do sistema contém uma cópia completa da imagem usada para iniciar uma instância e o ambiente de execução da instância. Ao iniciar uma instância, é necessário um disco do sistema maior do que a imagem usada.
Disco de dados: semelhante às unidades D e E no sistema Windows. O disco de dados salva os dados do usuário e permite expansão, montagem e desmontagem flexíveis.

Tanto o disco do sistema quanto o disco de dados são compatíveis com diferentes tipos de armazenamento fornecidos pelo Tencent Cloud. Para obter mais informações, consulte a [Visão geral do armazenamento](https://intl.cloud.tencent.com/document/product/213/4952).

## Segurança da instância

O Tencent Cloud fornece os seguintes métodos de proteção da segurança da instância:
- [Política](https://intl.cloud.tencent.com/document/product/598/10601): quando contas diferentes precisam controlar o mesmo conjunto de recursos de nuvem, você pode usar uma política para controlar o acesso delas a esses recursos.
- [Grupos de segurança](https://intl.cloud.tencent.com/document/product/213/12452): você pode usar um grupo de segurança para controlar o acesso de endereços confiáveis às instâncias.
- Controle de login: faça login em suas instâncias do Linux usando [chaves SSH](https://intl.cloud.tencent.com/document/product/213/6092), sempre que possível. Se você efetuar login em suas instâncias do Linux usando [senhas de login](https://intl.cloud.tencent.com/document/product/213/6093), altere suas senhas regularmente.

