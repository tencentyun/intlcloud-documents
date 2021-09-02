## Visão geral
Um disco local é um dispositivo de armazenamento no mesmo servidor físico da instância do CVM. Possui alta E/S de leitura/gravação e baixa latência.
O disco local é um dispositivo de armazenamento local no mesmo servidor físico que a instância do CVM. É um espaço de armazenamento reservado no servidor físico (atualmente disponível somente para os CVMs de alta E/S e de big data). A confiabilidade dos dados armazenados em um disco local é proporcional à confiabilidade do servidor físico. Talvez exista a possibilidade de haver um ponto único de falha.



>! 
> - Se ocorrer uma falha de hardware no servidor físico da instância do CVM, o disco local poderá perder dados valiosos. Recomendamos a redundância de dados na camada de aplicativos para garantir a confiabilidade. Se o seu aplicativo não for compatível com esse recurso, avalie utilizar o [Cloud Block Storage](https://intl.cloud.tencent.com/document/product/213/4953) para melhorar a confiabilidade dos dados.
> - Você não pode atualizar o hardware (CPU, memória, armazenamento) de uma instância do CVM apenas com discos locais. A única atualização permitida é a da largura de banda.
> 

## Cenário
- **Aplicativos com uso intensivo de E/S**: para grandes bancos de dados relacionais, NoSQL, ElasticSearch e outros aplicativos com uso intensivo de E/S que são mais sensíveis à latência, você tem a opção do disco local SSD NVME que acompanha os CVMs de alta E/S, mas saiba que ele traz o risco de um ponto único de falha.
- **Aplicativos de big data**: para aplicativos de big data, como EMR, que são menos sensíveis à latência e apresentam redundância de dados na camada superior para tolerar um ponto único de falha, a opção é utilizar o disco HDD SATA que acompanha os CVMs de big data.


## Ciclo de vida
O ciclo de vida de um disco local é o mesmo da instância do CVM à qual está montado. Portanto, os discos locais são iniciados e encerrados com as instâncias do CVM.

## Tipos

Os discos locais são dispositivos de armazenamento local no mesmo servidor físico que a instância do CVM. Existem dois tipos de discos locais por mídia: HDD SATA e SSD NVME.

| CVM | Especificação e desempenho |
|---------|---------|
| Disco local HDD SATA | [CVMs de big data](https://intl.cloud.tencent.com/document/product/213/11518#D) |
| Disco local SSD NVME | [CVMs de alta E/S](https://intl.cloud.tencent.com/document/product/213/11518#I) |

## Aquisição
Um disco local só pode ser adquirido junto à uma instância do CVM. Para obter mais informações sobre como adquirir uma instância do CVM, consulte [Criação de instâncias](https://intl.cloud.tencent.com/document/product/213/4855).

