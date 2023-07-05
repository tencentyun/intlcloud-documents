## Cenário

Este documento descreve como excluir imagens personalizadas.

## Observações
Antes de excluir imagens personalizadas, observe os seguintes itens:
 - Depois que uma imagem personalizada for excluída, ela não poderá mais ser usada para iniciar uma nova instância do CVM, mas não afetará as instâncias que já foram iniciadas. Se você deseja excluir todas as instâncias iniciadas a partir desta imagem, consulte [Recuperação de instâncias](https://intl.cloud.tencent.com/document/product/213/4931) ou [Encerrar instâncias](https://intl.cloud.tencent.com/document/product/213/4930).
 - Uma imagem personalizada que foi compartilhada com outras pessoas não pode ser excluída. Para excluí-la, é necessário primeiro cancelar o compartilhamento de imagens. Para obter mais informações, consulte [Cancelar o compartilhamento de imagens](https://intl.cloud.tencent.com/document/product/213/7148).
 - Só é possível excluir a imagem personalizada, não a imagem comum ou a imagem compartilhada.

## Instruções

### Exclusão de imagens pelo console
1. Faça login no Console do CVM. Na barra lateral esquerda, clique em [**Images (Imagens)**](https://console.cloud.tencent.com/cvm/)
2. E selecione a guia **Custom Image (Imagem personalizada)** para entrar na página de gerenciamento de imagens personalizadas.
3. Selecione o método para excluir as imagens personalizadas com base nas suas necessidades reais.
 - **Exclusão de uma única imagem**: localize a imagem personalizada a ser excluída na lista de imagens e clique em **More (Mais)** > **Delete (Excluir)**.
  ![](https://qcloudimg.tencent-cloud.cn/raw/1211de56434b4b6034dccb1ff9ce4aa1.png)
 - **Exclusão de várias imagens**: selecione todas as imagens personalizadas a serem excluídas na lista de imagens e clique em **Delete (Excluir)** na parte superior.
  ![](https://qcloudimg.tencent-cloud.cn/raw/9f002d5cce1cfa2c94931ea3bca25ac2.png) 
4. Na janela pop-up, clique em **OK**.
Se a exclusão falhar, os possíveis motivos serão exibidos.

### Exclusão de imagens por API
É possível usar a API DeleteImages para excluir imagens. Para obter detalhes, consulte [Excluir imagens](https://intl.cloud.tencent.com/document/product/213/33275).
