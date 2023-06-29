

A tabela abaixo explica os códigos de status do CDN.

| Código de status | Significado | Sugestão |
| :----- | :------------------------------- | :----------------------------------------------------------- |
| 400 | Erro de sintaxe de solicitação HTTP e o servidor não consegue analisar o pedido | Verifique se a sintaxe da solicitação está correta.|
| 403    | Solicitação rejeitada                             | Verifique se os controles de acesso, como a lista de bloqueio/permissões do referenciador, a lista de bloqueio/permissões de IP ou a autenticação estão bloqueando o acesso.|
| 404 | O servidor não é capaz de retornar informações corretas | Verifique se o servidor original está funcionando normalmente e se as informações do servidor original ou as configurações do domínio de origem foram alteradas. |
| 413    | O comprimento do conteúdo da solicitação POST está excedendo o limite                    | Verifique o tamanho do conteúdo da solicitação POST do cliente (o tamanho máximo é 32 MB por padrão).|
| 414    | O comprimento do URL está excedendo o limite                     | O tamanho máximo do URL é 2 KB por padrão.|
| 423    | Solicitação de loop                           | Verifique a configuração de 301/302, o pull de origem de HTTPS e o método de regravação do servidor de origem.|
| 499    | O cliente fecha a conexão                  | Verifique o status do cliente e a configuração de tempo limite.|
| 502    | Erro de gateway                             | Verifique se o servidor de origem corporativo está normal.|
| 503    | O controle de frequência do COS está sendo acionado                          | Verifique a configuração do cache ou se o servidor de origem do COS retorna no-cache/no-store.|
| 509    | Bloqueado devido a ataque CC                    | [Envie-nos um tíquete](https://console.intl.cloud.tencent.com/workorder/category) |
| 514    | A frequência de acesso de IP está excedendo limite                       | Verifique a configuração de controle de frequência de acesso de IP no console do CDN.|
| 531    | Erro ao resolver o nome de domínio de pull de origem na solicitação HTTP          | Verifique a configuração de resolução de nome de domínio do servidor de origem.|
| 532    | Falha ao estabelecer uma conexão com o servidor de origem na solicitação HTTPS              | Verifique o status da porta 443 do servidor de origem, a configuração do certificado ou a disponibilidade do servidor de origem.|
| 533    | Tempo limite de conexão de pull de origem na solicitação HTTPS              | Verifique o status da porta 443 do servidor de origem, a configuração do certificado ou a disponibilidade do servidor de origem.|
| 537    | Tempo limite de recepção de dados do servidor de origem na solicitação HTTPS             | Verifique a estabilidade do servidor de origem corporativo.|
| 538    | O handshake SSL da solicitação HTTPS falhou                | Verifique a compatibilidade entre o protocolo e o algoritmo do servidor de origem.|
| 539    | A validação do certificado da solicitação HTTPS falhou           | Verifique se o certificado do servidor de origem está configurado corretamente (período de validade e integridade da cadeia de certificados).|
| 540    | Falha na validação do nome de domínio do certificado da solicitação HTTPS          | Verifique se o certificado do servidor de origem está configurado corretamente.|
| 562    | Falha ao estabelecer uma conexão na solicitação HTTPS                | [Envie um tíquete](https://console.intl.cloud.tencent.com/workorder/category) e forneça as informações de X-NWS-LOG-UUID para solucionar o problema.| |
| 563    | Tempo limite de conexão na solicitação HTTPS              |[Envie um tíquete](https://console.intl.cloud.tencent.com/workorder/category) com as informações de X-NWS-LOG-UUID para solucionar o problema.| |
| 564    | A origem da solicitação HTTP falhou                | Se o HTTP estiver configurado como o protocolo de solicitação de origem, verifique a carga e a utilização da largura de banda ou o limite de acesso do servidor de origem. Se o protocolo estiver definido como **Follow Request (Seguir a solicitação)**, verifique o status da porta 443 e a configuração do certificado do servidor de origem. Se nenhum erro for encontrado no servidor de origem, [envie um tíquete](https://console.intl.cloud.tencent.com/workorder/category) com as informações de X-NWS-LOG-UUID para solucionar o problema.|











