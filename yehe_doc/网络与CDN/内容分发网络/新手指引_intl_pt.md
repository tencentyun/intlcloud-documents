Este documento o ajudará a dar os primeiros passos no Content Delivery Network (CDN) do Tencent Cloud.

## 1. Informações básicas sobre o CDN

- [Como funciona o CDN?](https://intl.cloud.tencent.com/document/product/228/2939)
- [Por que escolher o CDN do Tencent Cloud?](https://intl.cloud.tencent.com/document/product/228/2941)
- [Casos de uso do CDN](https://intl.cloud.tencent.com/document/product/228/32980)
- [Quais são os limites de uso do CDN?](https://intl.cloud.tencent.com/document/product/228/32981)
- [Conceitos básicos](https://intl.cloud.tencent.com/document/product/228/36183)



## 2. Modos de faturamento do CDN

O CDN do Tencent Cloud tem dois modos de faturamento: o **bill-by-bandwidth (faturamento por largura de banda)** e o **bill-by-traffic (faturamento por tráfego)**. É necessário entender os dois modos de faturamento do CDN para escolher o modo certo para você. Para obter mais informações, consulte a [Visão geral do faturamento](https://intl.cloud.tencent.com/document/product/228/2949).






## 3. Introdução

#### 3.1. Ativar o serviço e selecionar o modo de faturamento

Antes de usar o CDN, é necessário criar uma conta no Tencent Cloud e ativar o serviço do CDN. Para obter mais informações, consulte [Configuração do CDN do zero](https://intl.cloud.tencent.com/document/product/228/32978).

#### 3.2. Conectar um nome de domínio

É preciso adicionar um nome de domínio de aceleração para seu serviço de aceleração. Através de um nome de domínio de aceleração, o CDN armazena recursos em cache de um servidor de origem para um nó de cache do CDN mais próximo do cliente para acelerar o acesso aos recursos. Para obter mais informações, consulte a [Adição de nomes de domínio](https://intl.cloud.tencent.com/document/product/228/5734).

#### 3.3 Configurar o CNAME

Quando a distribuição for criada, o CDN atribuirá a você um endereço CNAME correspondente, que precisa ser configurado antes de entrar em vigor. Para obter instruções detalhadas, consulte [Configuração do CNAME](https://intl.cloud.tencent.com/document/product/228/3121).

>? Você também pode seguir as práticas recomendadas abaixo para começar a usar o CDN e acelerar o seu nome de domínio:
>- [Aceleração do acesso ao CVM com o CDN](https://intl.cloud.tencent.com/document/product/228/34035)
>- [Aceleração do acesso ao COS com o CDN](https://intl.cloud.tencent.com/document/product/228/34036)




## 4. Console

Veja abaixo a página de visão geral do console do CDN:
![](https://main.qcloudimg.com/raw/95fff730b132974403698b512260f3fb.png)




## 5. Visão geral das funcionalidades do console

<table>
<thead>
<tr>
<th>Operação desejada</th>
<th>Documento de referência</th>
</tr>
</thead>
<tbody><tr>
<td>Exibir, habilitar ou desabilitar um nome de domínio de aceleração conectado.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/5736" target="_blank">Operações de nomes de domínio</a></td>
</tr>
<tr>
<td>Filtrar e exibir os recursos do Tencent Cloud ou gerenciá-los por tag, projeto, etc.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/32913" target="_blank">Pesquisa de nomes de domínio</a></td>
</tr>
<tr>
<td>Otimizar o efeito de aceleração do seu CDN. O CDN permite várias configurações personalizadas.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6288" target="_blank">Visão geral das configurações</a></td>
</tr>
<tr>
<td>Exibir os mapeamentos entre as funcionalidades do console e os valores de `Action`.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35229" target="_blank">Permissões do console</a></td>
</tr>
<tr>
<td>Conceder permissões no nível do nome de domínio por meio de instruções de política personalizadas.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35228" target="_blank">Criação de políticas</a></td>
</tr>
<tr>
<td>Conceder permissões diferentes de nível de projeto.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35743" target="_blank">Permissões de nível de projeto</a></td>
</tr>
<tr>
<td>Usar dados de monitoramento em tempo real para analisar o status de execução.</td>
<td><a href="https://cloud.tencent.com/document/product/228/30794" target="_blank">Monitoramento em tempo real</a></td>
</tr>
<tr>
<td>Analisar as fontes, a distribuição e o uso dos seus usuários.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/32923" target="_blank">Análise de dados</a></td>
</tr>
<tr>
<td>Limpar os recursos armazenados em cache nos nós do CDN regularmente para que os nós efetuem pull das versões mais recentes dos recursos do servidor de origem e os armazenem em cache novamente.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6299" target="_blank">Limpeza de cache</a></td>
</tr>
<tr>
<td>Carregar recursos especificados em um nó de cache com antecedência.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/39000" target="_blank">Pré-busca de cache</a></td>
</tr>
<tr>
<td>Baixar logs de acesso e analisar recursos populares e usuários ativos conforme necessário.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6316" target="_blank">Logs de download</a></td>
</tr>
<tr>
<td>Pesquisar e analisar os seus dados de log rapidamente.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35380" target="_blank">Logs em tempo real</a></td>
</tr>
<tr>
<td>Exibir a visão geral do status em tempo real e os detalhes de toda a rede.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6311" target="_blank">Monitoramento completo do status de rede</a></td>
</tr>
<tr>
<td>Visualizar relatórios multidimensionais que mostram o status da sua empresa para análise.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6312" target="_blank">Relatório operacional</a></td>
</tr>
<tr>
 
 
</tr>
<tr>
<td>Verificar se um IP especificado é de um nó do CDN.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/10747" target="_blank">Verificação de IP do Tencent</a></td>
</tr>
<tr>
<td>Diagnosticar um URL com uma exceção de acesso e localizar o problema rapidamente.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6304" target="_blank">Ferramenta de autodiagnóstico</a></td>
</tr>
<tr>
<td>Monitorar e proteger seus recursos contra ataques DDoS e CC.</td>
<td>Security Content Delivery Network</a></td>
</tr>
<tr>
<td>Use o CDN para fornecer uma grande quantidade de imagens.</td>
<td><a href="https://cloud.tencent.com/document/product/228/43121" target="_blank">Otimização de imagens</a></td>
</tr>
</tbody></table>


## 6. Perguntas frequentes
#### Faturamento
- [Como consultar as faturas do CDN?](https://intl.cloud.tencent.com/document/product/228/31479)
 
- [O CDN pode ser faturado pela quantidade de solicitações?](https://intl.cloud.tencent.com/document/product/228/31479)
- [Se o servidor de origem usar o COS, serei cobrado pelo tráfego gerado pelo pull de origem do CDN para o COS?](https://intl.cloud.tencent.com/document/product/228/31479)
- [Quando o CDN for desabilitado ou desativado, ele vai gerar tráfego e incorrer em taxas?](https://intl.cloud.tencent.com/document/product/228/31479)
- [Como eu altero o modo de faturamento do CDN?](https://intl.cloud.tencent.com/document/product/228/31479)
 
- [Somente o tráfego downstream é faturado no CDN?](https://intl.cloud.tencent.com/document/product/228/31479)

#### Conexão de nomes de domínio

- [O CDN aceita nomes de domínio curinga?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Meu nome de domínio já obteve uma declaração ICP do MIIT. Por que o sistema avisa que não tem uma declaração ICP quando tento conectá-lo ao CDN?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Quanto tempo leva para configurar o CDN?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Posso configurar vários IPs de servidor de origem?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Como posso saber se o CDN entrou em vigor?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Por que um nome de domínio pode ser desabilitado, mas não excluído?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Como eu desativo o serviço de aceleração?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Como eu excluo um nome de domínio de aceleração?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Posso configurar portas para nomes de domínio de aceleração ou servidores de origem?](https://intl.cloud.tencent.com/document/product/228/31476)
- [O que eu devo fazer se não for possível baixar os arquivos do CDN?](https://intl.cloud.tencent.com/document/product/228/31476)



## 7. Feedback e sugestões
Se você tiver dúvidas ou sugestões ao utilizar o CDN do Tencent Cloud, envie seu feedback pelos seguintes canais. A equipe encarregada entrará em contato com você para resolver seus problemas.
- Se você tiver alguma dúvida sobre a documentação do CDN, como links, conteúdo ou APIs, clique em **Send Feedback (Enviar feedback)** na parte inferior da página.
- Se você tiver alguma dúvida sobre o CDN, [envie um tíquete](https://console.cloud.tencent.com/workorder/category).

