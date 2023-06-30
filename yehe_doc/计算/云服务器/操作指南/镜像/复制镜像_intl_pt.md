## Visão geral

### Etapas comuns

A **Replicação entre regiões** pode ajudar os usuários a implantar o mesmo CVM **em todas as regiões** rapidamente. É possível usar essa funcionalidade para copiar imagens entre regiões e, depois, criar um CVM copiando as imagens na nova região.

### Observações
 - A imagem copiada deve ser uma imagem personalizada. É necessário criar uma imagem personalizada primeiro. Para obter detalhes, consulte [Criação de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4942).
 - A replicação entre regiões permite que você copie imagens dentro ou fora da China. Se você precisar copiar imagens da China para outros países ou vice-versa, entre em contato com o serviço de pós-venda.
 - Atualmente, a replicação de imagens entre regiões é gratuita.
 - No momento, a replicação entre regiões não é compatível com imagens personalizadas com mais de 50 GB.
 - A replicação entre regiões leva de 10 a 30 minutos.
 
## Métodos
### Cópia de imagens pelo console
 1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
 2. Na barra lateral esquerda, clique em **[Images (Imagens)](https://console.cloud.tencent.com/cvm/image)** para entrar na página de gerenciamento de imagens.
 3. Selecione a região na qual a imagem original que você deseja copiar está localizada e clique na guia **Custom Image (Imagem personalizada)**, conforme mostrado abaixo:
 Por exemplo, selecione a região de Guangzhou.
 ![](https://main.qcloudimg.com/raw/f845cfeef21663bf8aaff58d5145f08c.png)
 4. Encontre a instância cuja imagem precisa ser copiada, clique em **More (Mais)** > **Cross-region replication (Replicação entre regiões)**.
 >? Para operações em lote, selecione todas as imagens que deseja copiar e clique em **Cross-region replication (Replicação entre regiões)**.
 >
 5. Na janela pop-up "Cross-region copying (Cópia entre regiões)", selecione as regiões para onde a imagem será copiada e clique em **OK**.
Após a conclusão da cópia, a lista de imagens nas regiões de destino exibirá as imagens com o mesmo nome e IDs diferentes.
 6. Mude para uma região de destino. Selecione a imagem copiada na lista de imagens da região e clique em **Create Instance (Criar instância)** para criar a mesma instância do CVM.

### Cópia de imagens por API
Também é possível usar a API SyncCvmImage para copiar imagens. 
