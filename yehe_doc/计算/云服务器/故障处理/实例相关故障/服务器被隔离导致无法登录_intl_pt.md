Este documento descreve como solucionar falhas de login se o CVM estiver isolado da rede pública.

## Problemas
O CVM pode ter sido isolado por violar as leis e os regulamentos vigentes. Você pode usar os métodos a seguir para verificar se o CVM está isolado.
- Quando um CVM estiver isolado da rede pública, você será notificado do isolamento por meio de uma [mensagem interna no console](https://console.cloud.tencent.com/message) ou mensagem de texto.
<!--
 - Mensagem interna:
![](//mc.qcloudimg.com/static/img/3c8ecd4ac301180e3632a25343be0697/image.png)
Ou
![](//mc.qcloudimg.com/static/img/cd3fbf748d3ff61adf3d2198853d18de/image.png)
 - SMS:
![](//mc.qcloudimg.com/static/img/afaff154fa12695844055422f4f103e6/image.png)
- A guia **Monitoring/Status (Monitoramento/Status)** no [console do CVM](https://console.cloud.tencent.com/cvm/index) exibe o status do CVM: Isolated (Isolado).
-->

## Causas
Quando ocorrer uma violação de regulamento ou evento de risco em um CVM, a máquina que violou as regras será parcialmente isolada (exceto as portas de login da rede privada 22, 36000 e 3389, todo o acesso à rede será isolado). Os desenvolvedores podem usar um servidor trampolim para fazer login no servidor.
Para mais detalhes, consulte a “Classificação dos níveis de violação de segurança da nuvem e descrição das penalidades”.

## Soluções

 1. Exclua o conteúdo inapropriado seguindo as instruções da mensagem interna ou mensagem de texto. Encerre os riscos de segurança e reinstale o sistema, se necessário.
 2. Se a violação não foi causada por você, significa que pode ter ocorrido uma invasão mal-intencionada no seu CVM. Para resolver esse problema, consulte a seção [Segurança do host](https://intl.cloud.tencent.com/document/product/296).
 3. Após sanar os riscos de segurança e excluir o conteúdo em violação, você pode [enviar um tíquete](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=7&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM) para entrar em contato com o atendimento ao cliente e remover o isolamento.

