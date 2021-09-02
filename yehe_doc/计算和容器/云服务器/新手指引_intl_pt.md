Este documento ajuda você a começar a usar a instância do Tencent Cloud Virtual Machine (CVM). 

## 1. Visão geral
O Tencent Cloud CVM é um serviço de computação em nuvem dimensionável, sem a necessidade de estimativa do uso de recursos nem investimento inicial. Com o Tencent Cloud CVM, você pode iniciar CVMs e implantar aplicativos imediatamente.


## 2. Saiba mais sobre o CVM
Consulte os documentos a seguir para saber mais sobre as instâncias do CVM.
- [Visão geral do CVM](https://intl.cloud.tencent.com/document/product/213/495)
- [Modos de cobrança da instância](https://intl.cloud.tencent.com/document/product/213/2180)
- [Visão geral dos limites de uso](https://intl.cloud.tencent.com/document/product/213/15379)
- [Conceitos](https://intl.cloud.tencent.com/document/product/213/38678).


## 3. Criação de instâncias do CVM
Você tem flexibilidade na escolha da região, do modelo, da imagem, da largura de banda da rede pública, da quantidade de aquisição e do período de validade na página [Configuração personalizada](http://manage.qcloud.com/shoppingcart/shop.php?tab=cvm&_ga=1.91351132.770173325.1571651505), para adquirir as instâncias do CVM que atendam às necessidades da sua empresa.
Para criar CVMs de forma personalizada, consulte [Personalização das configurações do CVM no Linux](https://intl.cloud.tencent.com/document/product/213/10517) ou [Personalização das configurações do CVM no Windows](https://intl.cloud.tencent.com/document/product/213/10516).
![](https://main.qcloudimg.com/raw/40c2812ff1294f901238cc3e39ba25f9.png)

## 4. Login nas instâncias do CVM
Depois de adquirir as instâncias do CVM, você pode fazer login nelas. Para obter mais informações, consulte:
 - [Login em uma instância do Linux](https://intl.cloud.tencent.com/document/product/213/5436)
 - [Login em uma instância do Windows](https://intl.cloud.tencent.com/document/product/213/5435)


Em seguida, você pode fazer login nelas para armazenar seus arquivos locais, usá-las como suas máquinas virtuais ou criar sites. Para obter mais informações e práticas, consulte o conteúdo a seguir.


## 5. Informações relevantes

### Visão geral das funcionalidades do console
| Funcionalidade | Referência |
|---------|---------|
| Criar instâncias do CVM | [Diretrizes para a criação de instâncias](https://intl.cloud.tencent.com/document/product/213/36302) |
| Nomear as instâncias ou CVMs de acordo com uma regra | [Nomenclatura sequencial em lote ou nomenclatura baseada em string de padrão](https://intl.cloud.tencent.com/document/product/213/32020) |
| Fazer upgrade ou downgrade da especificação do CVM | [Alteração da configuração da instância](https://intl.cloud.tencent.com/document/product/213/2178) |
| Escolher o par de chaves SSH como o método de login criptografado do CVM e gerenciar as chaves SSH | [Gerenciamento de chaves SSH](https://intl.cloud.tencent.com/document/product/213/16691) |
| Alterar ou redefinir a senha da instância | [Redefinição das senhas de instâncias](https://intl.cloud.tencent.com/document/product/213/16566) |
| Encerrar, liberar ou devolver uma instância do CVM | [Encerramento de instâncias](https://intl.cloud.tencent.com/document/product/213/4930) |
| Obter a lista de instâncias do CVM de uma região| [Exportar instâncias](https://intl.cloud.tencent.com/document/product/213/16563) |
| Procurar instâncias do CVM e outros recursos| Pesquisa entre regiões |
| Criar uma imagem personalizada e usá-la para iniciar outras instâncias novas que tenham as mesmas configurações personalizadas da original | [Criação de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4942) |
| Obter imagens compartilhadas por outros usuários, além dos componentes necessários, e adicionar conteúdo personalizado | [Compartilhamento de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4944) |
| Importar a imagem do disco do sistema em computadores locais ou outras plataformas para a imagem personalizada no CVM | [Visão geral](https://intl.cloud.tencent.com/document/product/213/4945) |
| Criar e exportar uma imagem do Linux | [Criação de imagens do Linux](https://intl.cloud.tencent.com/document/product/213/17814) |
| Criar e exportar uma imagem do Windows | [Criação de imagens do Windows](https://intl.cloud.tencent.com/document/product/213/17815) |
| Migrar sistemas e aplicativos nos servidores de origem de seus IDCs ou de outras plataformas de nuvem para o Tencent Cloud | [Visão geral](https://intl.cloud.tencent.com/document/product/213/35639) |
| Expandir os discos em nuvem para aumentar a capacidade de armazenamento | [Expansão de discos em nuvem](https://intl.cloud.tencent.com/document/product/213/32377) |
| Converter um IP público em um EIP para mascarar uma falha de instância | [IP elástico](https://intl.cloud.tencent.com/document/product/213/16586) |
| Criar um CVM com bloco CIDR IPv6 e habilitar o IPv6 para ENI, implementando a comunicação IPv6 nas redes privadas e públicas | [Configuração do IPv6](https://intl.cloud.tencent.com/document/product/213/34836) |
| Configurar grupos de segurança com base em casos de uso | [Casos de uso de grupos de segurança](https://intl.cloud.tencent.com/document/product/213/32369) |
| Usar tags para categorizar e gerenciar os recursos do CVM | [Guia do usuário sobre tags](https://intl.cloud.tencent.com/document/product/213/19548) |
| Visualizar os dados de monitoramento de instâncias do CVM, como CPU, memória, largura de banda da rede e discos | [Obtenção de estatísticas de monitoramento](https://intl.cloud.tencent.com/document/product/213/5178) |

### Uso avançado
Você pode criar um site ou fórum pessoais em instâncias do CVM, conforme as instruções em [Configuração de um site](https://intl.cloud.tencent.com/document/product/213/34815).

### Ferramentas de desenvolvimento
A API do Tencent Cloud fornece diversas ferramentas, como API Explorer, TCCLI, SDK e API Inspector, que ajudam você a usar e gerenciar rapidamente os serviços do Tencent Cloud com poucos códigos. 


## 6. Feedback e sugestões
Se você tiver dúvidas ou sugestões ao utilizar os produtos e serviços do Tencent Cloud CVM, envie seu feedback pelos seguintes canais. A equipe encarregada entrará em contato com você para resolver seus problemas.
- Para relatar problemas na documentação do produto, como erros de link, conteúdo ou API, você pode clicar em **Send Feedback (Enviar feedback)** na parte inferior do documento.
- Se você encontrar problemas relacionados ao produto, [envie um tíquete](https://console.cloud.tencent.com/workorder/category).

  


