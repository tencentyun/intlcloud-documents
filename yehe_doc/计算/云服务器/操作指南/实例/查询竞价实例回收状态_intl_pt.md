
As instâncias spot podem ser reavidas pelo Tencent Cloud devido a motivos de preço ou de estoque. Para permitir que os usuários executem operações personalizadas antes da instância ser reavida, fornecemos uma API para obter informações sobre o status da retomada de posse por meio de um mecanismo de metadados interno.

## Metadados
Os metadados da instância referem-se aos dados relevantes para uma instância. Eles podem ser usados para configurar ou gerenciar uma instância em operação. Você pode acessar e obter os metadados da instância por meio de uma instância. Para obter mais informações, consulte os [Metadados da instância](http://intl.cloud.tencent.com/document/product/213/4934).


## Uso de metadados para obter informações sobre o status da retomada de posse de uma instância spot
Para obter informações sobre o status da retomada de posse de uma instância spot, você pode acessar os metadados usando a ferramenta cURL ou uma solicitação HTTP GET.
```
curl metadata.tencentyun.com/latest/meta-data/spot/termination-time
```
- Se a seguinte informação for retornada, ela indica o tempo da retomada de posse da instância spot.
```
18/08/2018 12:05:33
```
- Se o código de erro 404 for retornado, a instância não é uma instância spot ou a retomada de posse não foi acionada.

Para obter mais informações, consulte os [Metadados da instância](http://intl.cloud.tencent.com/document/product/213/4934).
