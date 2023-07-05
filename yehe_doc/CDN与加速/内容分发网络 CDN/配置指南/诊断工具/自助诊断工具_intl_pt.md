O CDN fornece uma ferramenta de autodiagnóstico para ajudar você a solucionar problemas de falha de acesso à URL. Ele localiza o problema verificando a resolução de DNS, a qualidade do vínculo, o status do nó, o servidor de origem e a consistência de acesso aos dados, e oferece soluções relevantes.

>! O URL do recurso a ser diagnosticado deve ser um nome de domínio **ativo** em sua conta. Como a largura de banda gerada durante o diagnóstico incorre em custos, recomendamos que o recurso diagnosticado não tenha mais do que 200 MB.



## Diagnóstico de falhas
### Processo de diagnóstico

Se um URL de recurso não puder ser acessado, é possível iniciar o diagnóstico por meio do **Fault Self-diagnosis (Autodiagnóstico de falhas)** nas seguintes etapas:
1. Faça login no [console do CDN](https://console.cloud.tencent.com/cdn) e selecione **Inspect Tool (Ferramenta de inspeção)** -> **Fault Self-diagnosis (Autodiagnóstico de falhas)**.
2. Na página **Fault Self-diagnosis (Autodiagnóstico de falhas)**, insira o URL a ser diagnosticado. O URL deve começar com `http://` ou `https://`.
 ![](https://main.qcloudimg.com/raw/0b5b89dee36676027aeb15a118b4584e.png)
3. Clique em **Get a Diagnosis Link (Obter um link de diagnóstico)** e o endereço do link será exibido na página.
 ![](https://main.qcloudimg.com/raw/35e6dc6b335db10c63dc729cbe11ddbe.png)
4. Clique no link para abrir a página de diagnóstico, na qual as informações de diagnóstico serão coletadas. Não feche a página durante o progresso do diagnóstico. Você pode fechá-la manualmente após a conclusão do diagnóstico.
    ![](https://main.qcloudimg.com/raw/1e41c147e1e0ae216efc6635a43b1298.png)
5. Você também pode enviar o link de diagnóstico a outras pessoas para o diagnóstico local de falhas. Depois que o diagnóstico for concluído, será necessário fechar a página da web manualmente.

>!
- O link de diagnóstico é válido por 24 horas e aceita até 10 diagnósticos de falhas.
- Você pode copiar os links de diagnóstico disponíveis na página "Diagnostic Report (Relatório de diagnóstico)".

## Relatório de diagnóstico
### Visualização do relatório
1. Após a conclusão do diagnóstico, clique em **Diagnostic Report (Relatório de diagnóstico)** para visualizar os relatórios, que são exibidos em uma tabela em ordem cronológica. O conteúdo da tabela inclui:
	- O URL para o qual um link de diagnóstico foi gerado.
	- A área-alvo do diagnóstico de URL.
	- O link de diagnóstico correspondente ao URL.
	- A hora em que o link de diagnóstico foi gerado.
	- O status do link de diagnóstico.
	- A quantidade de diagnósticos disponíveis restantes do link de diagnóstico.

![](https://main.qcloudimg.com/raw/47c48777ace8428bb065695e1475600e.png)

2. Clique em **Expand (Expandir)** na coluna de operação para exibir o relatório gerado por cada diagnóstico e os resultados do diagnóstico.
![](https://main.qcloudimg.com/raw/a439f2dbcadcb6d2790e846416717cea.png)
3. Os relatórios de diagnóstico farão uma avaliação geral com base no diagnóstico de cada etapa, conforme mostrado abaixo:
 - Regular
 - Irregular
 - Página fechada de forma irregular. Normalmente, isso acontece quando a página é fechada antes que o diagnóstico seja concluído.
4. Clique em **View Report (Exibir relatório)** para consultar os detalhes e as sugestões do diagnóstico.

### Interpretação do relatório
1. A primeira parte do relatório exibe as informações de diagnóstico, incluindo:
 - ID do relatório de diagnóstico.
 - URL a ser diagnosticado.
 - Hora em que o diagnóstico foi acionado.
![](https://main.qcloudimg.com/raw/a7b7c60533782c95927d4860491594fd.png)

2. A segunda parte fornece uma visão geral do processo de diagnóstico e os resultados de cada módulo de diagnóstico. Os módulos excepcionais são identificados de forma clara. Os módulos de diagnóstico incluem:
 - Resultado da verificação das informações do cliente.
 - Resultado da verificação de DNS.
 - Resultado da verificação do CNAME.
 - Resultado da verificação de vínculo de rede.
 - Resultado da verificação do nó de acesso.
 -- Resultado da verificação do nó de pull de origem.
 -- Resultado da verificação do servidor de origem.
![](https://main.qcloudimg.com/raw/1298a6d0b2e72b70ca202a03660b409f.png)

3. A terceira parte traz os resultados do diagnóstico.
 #### Seção 1. Informações do cliente
São obtidas informações como IP do cliente, distrito/ISP e agente do usuário, referencial e método de solicitação da solicitação HTTP/HTTPS iniciada. Sem as informações do cliente, algumas verificações posteriores não podem ser realizadas.
![](https://main.qcloudimg.com/raw/8219224766176ed87ebb421330170f4a.png)

 #### Seção 2. Verificação de DNS
O IP de DNS do cliente é coletado e verificado em relação ao IP do cliente, para determinar se as exceções na configuração do DNS local estão causando problemas na programação de solicitações para os nós de cache ideais.
![](https://main.qcloudimg.com/raw/4ab79b159c3e983cd6db7c1fefeae9ea.png)

 #### Seção 3. Verificação do CNAME
A configuração do CNAME do nome de domínio é obtida. A resolução CNAME do nome de domínio precisa ser configurada com o nome de domínio correto, com o sufixo `*.cdn.dnsv1.com` (padrão); caso contrário, as solicitações não conseguirão alcançar os nós do CDN.
![](https://main.qcloudimg.com/raw/c3bbbb52440985415d9433b838dbde42.png)
>! Se a verificação da configuração do CNAME falhar, as solicitações não alcançarão os nós do CDN e os diagnósticos posteriores não serão realizados.

 #### Seção 4. Verificação de vínculo de rede
Vários sites são verificados localmente para obter o status de rede do cliente. Se um site não puder ser acessado devido à configuração do proxy local, a verificação do vínculo de rede falhará e os diagnósticos posteriores não serão realizados.
![](https://main.qcloudimg.com/raw/be249d3593b9956bf4e03393f02bb1d4.png)

 #### Seção 5. Verificação do nó de acesso
Depois que uma solicitação do cliente atinge um nó do CDN, as informações do nó serão coletadas, incluindo o IP do nó, o distrito/ISP do nó, o código de status retornado pelo nó, o status de acerto e o recurso MD5.
 - Se um recurso já tiver sido armazenado em cache em um nó do CDN, ele será atingido diretamente e a verificação do nó do pull de origem não será realizada.
 - Em caso de erro de cache, a verificação do nó do pull de origem será realizada.
 - Se o código de status retornado pelo URL for 301, 302 ou 504, as informações de verificação do nó não serão obtidas e as verificações posteriores não serão realizadas.
 - Se uma ACL tiver sido configurada para o nome de domínio, o nó de acesso retornará diretamente o código 403 e o status de acerto será **hit (acerto)**.
![](https://main.qcloudimg.com/raw/cce938713c83879c50899efb71b9ea2e.png)

 #### Seção 6. Verificação do nó de pull de origem
 1. Se o recurso for retornado diretamente por um nó do CDN, o status de acerto tanto do nó de acesso quanto do nó de pull de origem será **hit (acerto)**, e o CDN continuará verificando o servidor de origem para ajudar a verificar se os códigos de status e o conteúdo retornados do servidor de origem são iguais aos do nó.
![](https://main.qcloudimg.com/raw/88ec7bc47877ef3c96b468a2a9c19a00.png)
 2. Se o recurso não for retornado diretamente por um nó do CDN, o status de acerto tanto do nó de acesso quanto do nó de pull de origem será **missed (erro)** e o conteúdo será retornado pelo servidor de origem.
![](https://main.qcloudimg.com/raw/ce8f450c620a6ed2b13de186a04b677b.png)
 3. Se um código de status excepcional for gerado neste momento, você pode comparar o código de status do servidor de origem e o valor do arquivo MD5 com aqueles retornados pelo módulo de acesso, a fim de determinar se a exceção foi causada por um nó do CDN ou pelo servidor de origem e, em seguida, corrigir o problema em conformidade.

>?Se o relatório de diagnóstico não ajudar a resolver o problema, [envie um tíquete](https://console.cloud.tencent.com/workorder/category) ou entre em contato com o suporte técnico do Tencent Cloud.

