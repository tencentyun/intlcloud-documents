## O que é uma imagem?
Uma imagem é uma cópia seriada do estado completo de um sistema de computador armazenado como um arquivo. Uma imagem pode ser considerada como um disco de instalação do sistema. Ela contém tudo o que você precisa para iniciar uma instância do CVM. Uma imagem pode iniciar quantas instâncias do CVM você desejar, e você pode iniciar instâncias do CVM a partir de quantas imagens desejar. 

## Tipos de imagens
O Tencent Cloud fornece os seguintes tipos de imagens:
- **Imagens públicas**: ficam disponíveis a todos os usuários e abrangem a maioria dos sistemas operacionais do mercado.
- **Imagens personalizadas**: ficam disponíveis apenas ao proprietário e aos usuários com quem elas são compartilhadas. As imagens personalizadas são criadas a partir de instâncias ou importadas de fontes externas.
- **Imagens compartilhadas**: compartilhadas por outros usuários. Só podem ser usadas para a criação de instâncias.

Para obter mais informações sobre os tipos de imagens, consulte [Tipos de imagens](https://intl.cloud.tencent.com/document/product/213/4941).

## Casos de uso
 - **Implante um ambiente de software específico**
Para fornecer serviços Web ou desenvolver aplicativos, muitas vezes é necessário um pacote específico de softwares sendo executado em um ambiente coeso. A criação desses ambientes e a instalação dos softwares são demoradas e complexas, razão pela qual o Tencent Cloud é perfeito para tais tarefas. As imagens personalizadas e compartilhadas podem ajudar você a atender às suas necessidades de forma rápida e sem esforço.
 - **Implantar o ambiente de software em lotes**
Você pode criar uma imagem a partir de uma instância com um ambiente implantado e, em seguida, usá-la para criar instâncias em lotes. Após a criação, essas instâncias terão o mesmo ambiente de software que a instância original.
 - **Backup do ambiente de tempo de execução do servidor**
Você pode criar uma imagem personalizada a partir de uma instância do CVM para fazer o backup do ambiente de tempo de execução. Se, depois disso, o ambiente for corrompido você poderá usar a imagem para restaurá-lo. 

## Ciclo de vida da imagem

O esquema a seguir ilustra o ciclo de vida de uma imagem personalizada. Após essa imagem ser criada ou importada, você poderá usá-la para iniciar uma instância do CVM. As imagens personalizadas podem ser copiadas para outras regiões sob a mesma conta. Também é possível compartilhar imagens personalizadas com outros usuários.
![](http://mc.qcloudimg.com/static/img/b11a8e644fd89ce844c8fb0b69e7044a/image.png)


