
Este documento descreve como acelerar o acesso ao COS por meio do CDN do Tencent Cloud.


## Content Delivery Network (CDN)
Ao fornecer recursos para uma grande quantidade de nós de cache implantados globalmente e usar o sistema de programação do GSLB do Tencent, que foi desenvolvido de forma independente, o CDN permite o acesso próximo aos recursos necessários para os usuários finais. Isso reduz os atrasos de acesso causados por congestionamento de rede, distância e problemas de ISP e melhora efetivamente a velocidade de download, a capacidade de resposta e a experiência do usuário.


## Cloud Object Storage (COS)
É possível armazenar todos os seus recursos estáticos, como scripts estáticos, arquivos de áudio/vídeo, imagens e anexos no armazenamento padrão no COS, que apresenta capacidade ilimitada e leituras/gravações de alta frequência para fornecer armazenamento escalonável e confiável para recursos estáticos e reduzir a pressão em servidores de recursos.


## Práticas de entrega de conteúdo
O CDN pode acelerar a entrega global de recursos estáticos, como scripts estáticos, arquivos de áudio/vídeo, imagens e anexos armazenados no COS. Com os nós de cache global e os recursos de programação do CDN, os recursos mais solicitados podem ser entregues aos servidores de borda com antecedência. Ao serem acessados ou baixados por usuários finais, os recursos armazenados em cache em um nó próximo serão retornados. Isso reduz a pressão no servidor de origem e o atraso na transferência, melhorando significativamente a experiência do usuário.
![](https://main.qcloudimg.com/raw/6316f3fde6226ad974d0bc17592c1425.png)

>! O [Enterprise Content Delivery Network (ECDN) do Tencent Cloud](https://intl.cloud.tencent.com/product/ecdn) pode ser usado para acelerar a entrega de recursos dinâmicos/estáticos ou recursos dinâmicos armazenados no COS.


## Implementação

A aceleração do CDN pode ser implementada para o COS das duas maneiras seguintes. Escolha alguma delas para concluir a aceleração：

- Direcione o ponto de extremidade do COS para o nome de domínio de aceleração do CDN e vincule seu nome de domínio ao nome de domínio de aceleração do CDN (por meio do CNAME). Para obter instruções detalhadas, consulte [Implementação pelo console do CDN](https://intl.cloud.tencent.com/document/product/228/32984).
- Vincule seu nome de domínio ao ponto de extremidade do COS e habilite a aceleração de CDN. Para obter instruções detalhadas, consulte [Implementação pelo console do COS](https://intl.cloud.tencent.com/document/product/228/32985).

