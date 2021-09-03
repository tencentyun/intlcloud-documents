## Cenário
Este documento descreve como cancelar o compartilhamento de imagens personalizadas. É possível cancelar seu status de compartilhamento de imagens com outros usuários a qualquer momento. Isso não afeta as instâncias criadas por outros usuários usando essa imagem compartilhada, mas eles não conseguem mais visualizar a imagem nem criar instâncias novas usando essa imagem.

## Instruções
### Cancelamento do compartilhamento de imagens pelo console
 1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
 2. Na barra lateral esquerda, clique em **Images (Imagens)**.
 3. Selecione a guia **Custom Image (Imagem personalizada)** para entrar na página de gerenciamento de imagens personalizadas.
 4. Na lista de imagens personalizadas, selecione as imagens das quais deseja cancelar o compartilhamento e clique em **More (Mais)** > **Cancel Sharing (Cancelar compartilhamento)**.
 5. Na nova página, selecione o ID exclusivo da conta da qual deseja cancelar o compartilhamento de imagens e clique em **Cancel Sharing (Cancelar compartilhamento)**.
 6. Na janela pop-up, clique em **OK** para cancelar o compartilhamento de imagens.

### Cancelamento do compartilhamento de imagens por API
É possível usar a API ModifyImageSharePermission para cancelar o compartilhamento de imagens. Para obter mais informações, consulte [ModifyImageSharePermission](https://intl.cloud.tencent.com/document/product/213/33268).
