<style>
table th:nth-of-type(3) {
	width: 586px;
}
</style>
A tabela abaixo explica os códigos de status do CDN.

| Código de status | Significado | Sugestão |
| ----- | --------------------------------------------------- | ------------------------------------------------------------ |
| 0|A solicitação está terminando antes que o código de status seja obtido|Verifique se o cliente está desconectando a solicitação antecipadamente ou se o há falha de pull de origem.|
| 400 | Erro de sintaxe de solicitação HTTP <br/>O servidor não consegue analisar o pedido. | Verifique se a sintaxe da solicitação está correta.|
| 403    | Solicitação rejeitada                             | Verifique se a solicitação está sendo bloqueada pelos controles de acesso, como a lista de bloqueio/permissões do referenciador, a lista de bloqueio/permissões de IP ou a autenticação.|
| 413    | O comprimento do conteúdo da solicitação POST está excedendo o limite                    | Verifique o tamanho do conteúdo da solicitação POST do cliente (o tamanho máximo é 32 MB por padrão).|
| 414    | O comprimento do URL excedeu o limite                     | O tamanho máximo do URL é 2 KB por padrão.|
| 423    | Solicitação de loop                           | Verifique a configuração de 301/302, o pull de origem de HTTPS e o método de reescrita do servidor de origem.|
| 499    | O cliente fecha a conexão                  | Verifique o status do cliente e a configuração de tempo limite.|
| 502    | Erro de gateway                             | Verifique se o servidor de origem comercial está normal.|
| 503    | O controle de frequência do COS está sendo acionado                          | Verifique a configuração do cache ou se o servidor de origem do COS retorna no-cache/no-store.|
| 504    | Tempo limite do gateway                          | Entre em contato pelo site oficial.              |
| 509    | Bloqueado devido a ataque CC                    | [Entre em contato conosco](https://intl.cloud.tencent.com/contact-sales) ou [envie um tíquete](https://console.cloud.tencent.com/workorder/category) para desbloqueá-lo.|
| 514    | A frequência de acesso de IP está excedendo o limite                       | Verifique a configuração de controle de frequência de acesso de IP no console do CDN.|
| 531    | Erro ao resolver o nome de domínio de pull de origem na solicitação HTTP          | Verifique a configuração de resolução de nome de domínio do servidor de origem.|
| 532    | Falha ao estabelecer uma conexão com o servidor de origem na solicitação HTTPS              | Verifique o status da porta 443 do servidor de origem, a configuração do certificado ou a disponibilidade do servidor de origem.|
| 533    | Tempo limite de conexão de pull de origem na solicitação HTTPS              | Verifique o status da porta 443 do servidor de origem, a configuração do certificado ou a disponibilidade do servidor de origem.|
| 537    | Tempo limite de recepção de dados do servidor de origem na solicitação HTTPS             | Verifique a estabilidade do servidor de origem corporativo.|
| 538    | O handshake SSL da solicitação HTTPS falhou                | Verifique a compatibilidade entre o protocolo e o algoritmo do servidor de origem.|
| 539    | A validação do certificado da solicitação HTTPS falhou           | Verifique se o certificado do servidor de origem está configurado corretamente (período de validade e integridade da cadeia de certificados).|
| 540    | Falha na validação do nome de domínio do certificado da solicitação HTTPS          | Verifique se o certificado do servidor de origem está configurado corretamente.|
| 562    | Falha ao estabelecer uma conexão na solicitação HTTPS                | [Entre em contato conosco](https://intl.cloud.tencent.com/contact-sales) com as informações de X-NWS-LOG-UUID ou [envie um tíquete](https://console.cloud.tencent.com/workorder/category) para solucionar o problema.|
| 563    | Tempo limite de conexão na solicitação HTTPS              | [Entre em contato conosco](https://intl.cloud.tencent.com/contact-sales) com as informações de X-NWS-LOG-UUID ou [envie um tíquete](https://console.cloud.tencent.com/workorder/category) para solucionar o problema.|
| 564    | O pull de origem na solicitação HTTPS falhou                | Se HTTP estiver configurado como o protocolo de pull de origem, verifique a carga e a utilização da largura de banda ou o limite de acesso do servidor de origem. </br>Se o método de seguir o protocolo estiver configurado, verifique o status da porta 443 e a configuração do certificado do servidor de origem. </br>Se nenhum erro for encontrado no servidor de origem, [entre em contato conosco](https://intl.cloud.tencent.com/contact-sales) com as informações de X-NWS-LOG-UUID ou [envie um tíquete](https://console.cloud.tencent.com/workorder/category) para solucionar o problema. |












