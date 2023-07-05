## Visão geral

**Imagem compartilhada** significa que você compartilha com **outros usuários** uma [**imagem personalizada**](https://intl.cloud.tencent.com/document/product/213/4942) que você criou. Você também pode obter imagens compartilhadas por outros usuários, obter os componentes necessários e adicionar conteúdo personalizado.

>! O Tencent Cloud não garante a integridade ou a segurança das imagens compartilhadas. Use apenas imagens compartilhadas de fontes confiáveis.
>

## Observações
 - É possível compartilhar cada imagem com no máximo 50 usuários do Tencent Cloud.
 - Não é possível alterar o nome e a descrição das imagens compartilhadas. Eles são usados para criar apenas instâncias do CVM.
 - As imagens compartilhadas com outros usuários não ocupam sua própria cota de imagens.
 - Uma imagem personalizada que foi compartilhada com outras pessoas pode ser excluída, desde que primeiro você cancele o compartilhamento da imagem. Para obter mais informações, consulte [Cancelamento do compartilhamento de imagens](https://intl.cloud.tencent.com/document/product/213/7148). As imagens compartilhadas que você obtém de outras pessoas não podem ser excluídas.
 - As imagens personalizadas só podem ser compartilhadas com contas na mesma região que a conta de origem. Para compartilhar uma imagem com usuários em outra região, é necessário copiá-la para a região de destino antes de compartilhar.
 - As imagens compartilhadas que você obtém de outras pessoas não podem ser compartilhadas com terceiros.

## Instruções

### Obtenção do ID da conta raiz com a qual você deseja compartilhar a imagem

A imagem compartilhada do Tencent Cloud é identificada pelo ID exclusivo da conta raiz com a qual você deseja compartilhar a imagem. É possível obter o ID da conta do outro usuário da seguinte forma:
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
2. Clique no nome da conta no canto superior direito e selecione **Account Information (Informações da conta)**.
3. Visualize e registre o ID da conta.
4. Solicite ao outro usuário que lhe envie o ID da conta.

### Compartilhamento de imagens pelo console

 1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
 2. Clique em **[Images (Imagens)](https://console.cloud.tencent.com/cvm/image)** na barra lateral esquerda.
 3. Clique na guia **Custom Image (Imagem personalizada)** para entrar na página de gerenciamento de imagens personalizadas.
 4. Selecione a imagem personalizada que deseja compartilhar na lista de imagens personalizadas e clique em **Share (Compartilhar)** à direita.
 5. Na janela pop-up “Shared Image (Imagem compartilhada)”, insira o ID da conta com a qual deseja compartilhar a imagem e clique em **Share (Compartilhar)**.
 6.A outra conta precisa fazer login no [console do CVM](https://console.cloud.tencent.com/cvm/) e selecionar **Images (Imagens)** > **Shared Image (Imagem compartilhada)** para visualizar a imagem que você compartilhou.
 7. Repita as etapas acima para compartilhar uma imagem com vários usuários.

### Compartilhamento de imagens por API

É possível usar a API `ShareImage` para compartilhar imagens. Para obter mais informações, consulte a API `ShareImage`.

