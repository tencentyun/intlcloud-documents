O CLB é compatível com a configuração de logs de acesso para coletar e registrar os detalhes de cada solicitação de cliente, como horário da solicitação, caminho da solicitação, IP e porta do cliente, código de retorno e tempo de resposta. Este recurso pode ajudá-lo a entender melhor as solicitações do cliente, solucionar problemas e analisar o comportamento do usuário.
>?
> - Apenas o CLB de camada 7 é compatível com a configuração de logs de acesso.
> - Este recurso está disponível apenas nas regiões listadas abaixo.

## Métodos de armazenamento
- Os logs de acesso do CLB podem ser armazenados no [Cloud Log Service (CLS)](https://intl.cloud.tencent.com/document/product/614): O CLS é uma plataforma completa de serviço de log que fornece uma variedade de serviços de log, incluindo coleta, armazenamento, pesquisa, análise, exportação em tempo real e remessa de logs. Ele auxilia na implementação de operações de negócios, monitoramento de segurança, auditoria e análise de log.

<table class="table">
<thead>
<tr>
<th>Item</th>
<th>Armazenamento de logs de acesso no CLS</th>
</tr>
</thead>
<tbody>
<tr>
<td>Granularidade de tempo para obtenção de log</td>
<td>Minuto</td>
</tr>
<tr>
<td>Pesquisa on-line</td>
<td>Compatível</td>
</tr>
<tr>
<td>Sintaxe de pesquisa</td>
<td>Pesquisa de texto completo, pesquisa de valor de chave, pesquisa de palavra-chave difusa, etc. Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/614/37882">Sintaxe de pesquisa do CLS legado</a>.</td>
</tr>
<tr>
<td>Regiões com suporte</td>
<td>Guangzhou, Xangai, Nanjing, Pequim, Chengdu, Chongqing, Hong Kong (China), Singapura, Mumbai, Seul, Tóquio, Vale do Silício, Virgínia, Toronto, Frankfurt. </td>
</tr>
<tr>
<td>Tipo de CLB compatível</td>
<td>CLB de rede pública/rede privada</td>
</tr>
<tr>
<td>Links de envio de dados e de recebimento de dados</td>
<td>Os logs do CLS podem ser remetidos para o COS e exportados para o CKafka para processamento posterior.</td>
</tr> 
<tr>
<td>Retenção de log </td>
<td>O Tencent Cloud não armazena logs de acesso por padrão. O recurso de armazenamento pode ser configurado conforme necessário.</td>
</tr>
</tbody></table>

## Operações relevantes
- [Armazenamento de logs de acesso no CLS](https://intl.cloud.tencent.com/document/product/214/35063)
