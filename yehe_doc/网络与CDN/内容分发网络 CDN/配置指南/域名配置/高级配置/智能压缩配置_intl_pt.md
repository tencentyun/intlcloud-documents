## Visão geral das configurações
Com o auxílio da compactação inteligente, o CDN do Tencent Cloud pode compactar os recursos retornados com Gzip ou Brotli de acordo com as regras definidas, o que reduz efetivamente o tamanho do conteúdo transferido e os custos.

> ! 
> - Atualmente, a compactação inteligente é compatível apenas com dois tipos de serviço: a aceleração estática e a aceleração de download.
> - Se o seu nome de domínio estiver configurado para a aceleração global, a configuração de compactação inteligente terá efeito global. Essa configuração não faz distinção entre solicitações da China Continental e de fora da China Continental.
> - Atualmente, a compactação Brotli não é compatível nas regiões fora da China Continental.


## Guia de configuração
### Visualização da configuração
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia **Advanced Configuration (Configuração avançada)** para localizar a seção **Smart Compression (Compactação inteligente)**. Essa configuração fica ativada por padrão.
- Depois que um nome de domínio de aceleração for conectado, os recursos com tamanhos variando de 256 bytes a 2 MB com extensões de arquivo .js, .html, .css, .xml, .json, .shtml e .htm serão compactados com Gzip por padrão.

![](https://main.qcloudimg.com/raw/db292e0fcc2a0d993b72117756c76b63.png)

### Modificação da configuração
Clique em **Modify (Modificar)** para modificar as regras de compressão:
![](https://main.qcloudimg.com/raw/887c62b7a53f6193f061ffc14b372de2.png)

**Limitações de configuração**
- O tipo de arquivo permite até 200 caracteres.
- O tamanho do arquivo deve ser de até 30 MB.
- Atualmente, a compactação Brotli não é compatível com algumas plataformas que estão sendo atualizadas.

>? 
> - A configuração pode ser modificada quando estiver desativada, mas não será implantada oficialmente até que seja ativada.
> - Se Gzip e Brotli forem selecionados, os arquivos compactados serão retornados de acordo com o cabeçalho de compactação da solicitação.
> - Se apenas Brotli for selecionado e o cabeçalho de compactação da solicitação não for compatível, os recursos originais serão retornados sem serem compactados.


