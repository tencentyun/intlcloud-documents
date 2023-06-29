## Visão geral das configurações

- O arraste de vídeo costuma acontecer em cenários de VOD. Quando um usuário arrastar a barra de progresso do vídeo, uma solicitação semelhante à mostrada abaixo será enviada ao servidor:
`http://www.test.com/test.flv?start=10`
  Nesse caso, os dados serão retornados a partir do décimo byte. Os arquivos de vídeo em cenários de VOD são todos armazenados em cache em vários nós do CDN; portanto, os nós podem responder diretamente a essas solicitações, uma vez que essa configuração estiver ativa.
- A configuração Ignorar string de consulta deve estar ativada para o arraste de vídeo. Ou seja, a funcionalidade Ignorar string de consulta de todas as regras em [Configuração de regra de chave de cache](https://intl.cloud.tencent.com/document/product/228/35316) deve ser configurada como "Filter All (Filtrar tudo)" e o servidor de origem deve ser compatível com solicitações de intervalo. Os formatos de arquivo compatíveis são MP4, FLV e TS.

| Tipo de arquivo | Metainformações                                                 | Descrição do parâmetro (start)             | Exemplo de solicitação                                       |
| :------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| MP4 | Para um vídeo no servidor de origem, as metainformações devem estar localizadas no cabeçalho do arquivo. Os vídeos com metainformações, localizadas no final do arquivo, não são compatíveis. | O parâmetro `start` especifica um ponto de tempo (em segundos) e usa um decimal para especificar um milissegundo. Por exemplo, "start = 1.01" significa que o tempo de início é 1,01 s. O CDN localizará o último keyframe antes do tempo especificado pelo `start` caso esse não seja um keyframe. | `http://www.test.com/demo.mp4?start=10` indica que o vídeo será reproduzido a partir do décimo segundo. |
| FLV      | O vídeo no servidor de origem deve conter metainformações.                                   | O parâmetro `start` especifica um byte. O CDN localizará automaticamente o último keyframe antes do byte especificado pelo `start` caso esse não seja um keyframe.| `http://www.test.com/demo.flv?start=10` indica que o vídeo será reproduzido a partir do décimo byte. |
| TS       | Nenhum requisito especial.                                                   | O parâmetro `start` especifica um ponto de tempo (em segundos) e usa um decimal para especificar um milissegundo. Por exemplo, "start = 1.01" significa que o tempo de início é 1,01 s. O CDN localizará o último keyframe antes do tempo especificado pelo `start` caso esse não seja um keyframe. | `http://www.test.com/demo.ts?start=10` indica que o vídeo será reproduzido a partir do décimo segundo.  |


## Visualização da configuração
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em um nome de domínio de aceleração de streaming de VOD para acessar a página de configuração. Abra a guia **Access Control (Controle de acesso)** para encontrar a seção **Video Dragging (Arraste de vídeo)**. O arraste de vídeo fica desativado por padrão.
![img](https://main.qcloudimg.com/raw/515a46c56b93b9932f5bbcab39a8293e.png)
