Este documento descreve como acelerar o acesso ao CVM por meio do CDN do Tencent Cloud.

## Content Delivery Network (CDN)
Ao fornecer recursos para uma grande quantidade de nós de cache implantados globalmente e usar o sistema de programação do GSLB do Tencent, que foi desenvolvido de forma independente, o CDN permite o acesso próximo aos recursos necessários para os usuários finais. Isso reduz os atrasos de acesso causados por congestionamento de rede, distância e problemas de ISP e melhora efetivamente a velocidade de download, a capacidade de resposta e a experiência do usuário.

## Cloud Virtual Machine (CVM)
O CVM fornece recursos de computação virtual dimensionáveis na nuvem. Você pode iniciar as instâncias do CVM em diferentes sistemas operacionais e carregá-las em seu ambiente de aplicação personalizado. Conforme suas necessidades empresariais mudarem, será possível dimensionar seus recursos de computação em tempo real e ajustar as especificações da sua instância do CVM de acordo.


## Práticas de entrega de conteúdo

O CDN pode acelerar a entrega global de recursos estáticos, como grandes quantidades de arquivos de áudio/vídeo, imagens e arquivos armazenados no CVM. Com os nós de cache global e os recursos de programação do CDN, os recursos mais solicitados podem ser entregues aos servidores de borda com antecedência. Ao serem acessados ou baixados por usuários finais, os recursos armazenados em cache em um nó próximo serão retornados.

A aceleração do CDN para o CVM não apenas reduz a pressão no servidor de origem, o atraso de transferência e os custos de largura de banda, mas também melhora significativamente a disponibilidade do serviço.
![](https://main.qcloudimg.com/raw/66e176f86760440228d930e077f21247.png)

>! O [Enterprise Content Delivery Network (ECDN) do Tencent Cloud](https://intl.cloud.tencent.com/product/ecdn) pode ser usado para acelerar a entrega de recursos dinâmicos/estáticos ou recursos dinâmicos armazenados no CVM.


## Implementação

A aceleração do CDN pode ser implementada para o CVM da seguinte forma:

Vincule o nome de domínio de aceleração do CDN ao nome de domínio ou endereço IP do CVM e ative o serviço de aceleração do CDN. Para obter instruções detalhadas, consulte [Implementação pelo console do CDN](https://intl.cloud.tencent.com/document/product/228/32988).
