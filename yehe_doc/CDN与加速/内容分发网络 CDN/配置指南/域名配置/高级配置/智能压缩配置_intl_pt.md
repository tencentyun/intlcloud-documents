
## Visão geral
Com o auxílio da compactação inteligente, o CDN da Tencent Cloud pode compactar os recursos retornados com Gzip ou Brotli de acordo com as regras definidas, o que reduz efetivamente o tamanho do conteúdo transferido e os custos.

> ! 
> - Se o seu nome de domínio estiver configurado para a aceleração global, a configuração de compactação inteligente terá efeito global. Essa configuração não faz distinção entre solicitações de dentro ou fora da China continental.
> - O tipo de arquivo (tipo de conteúdo) e a compactação Brotli, atualmente, não estão disponíveis em regiões fora da China continental.


## Instruções
### Visualização da configuração
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia ***Advanced Configuration (Configuração avançada)** para localizar a seção **Smart Compression (Compactação inteligente)**. Essa configuração é habilitada por padrão.
- Depois que um nome de domínio de aceleração for conectado, os recursos com tamanhos variando de 256 bytes a 2 MB com extensões de arquivo .js, .html, .css, .xml, .json, .shtml e .htm serão compactados com Gzip por padrão.

![](https://main.qcloudimg.com/raw/db292e0fcc2a0d993b72117756c76b63.png)

### Modificação da configuração
Clique em **Modify (Modificar)** para modificar as regras de compactação:
![](https://main.qcloudimg.com/raw/887c62b7a53f6193f061ffc14b372de2.png)

**Limitações de configuração**
- **Type (Tipo)**: compatível com **All Files (Todos os arquivos)**, *File Extension (Extensão de arquivo)** e **File Content-Type (Tipo de conteúdo de arquivo)**. É definida como **File Extension (Extensão de arquivo)** por padrão.
- Se **File Extension (Extensão de arquivo)** for selecionado, o comprimento máximo do conteúdo será de 200 caracteres.
- Se **File Content-Type (Tipo de conteúdo do arquivo)** for selecionado, o conteúdo padrão será o seguinte: `text/html, text/xml, text/plain, text/css, text/javascript, application/json, application/javascript, application/x-javascript, application/rss+xml, application/xmltext, image/svg+xml, image/tiff`. É possível editar o conteúdo conforme necessário. Observe que você pode inserir até 100 grupos de conteúdo separados por ponto e vírgula (;). Cada grupo pode ter até 50 caracteres.
- Algumas plataformas estão sendo atualizadas e não suportam o tipo de arquivo (tipo de conteúdo) e compactação Brotli.


>? 
> - A configuração pode ser modificada quando estiver desativada, mas não será implantada oficialmente até que seja ativada.
> - Se Gzip e Brotli forem selecionados, os arquivos compactados serão retornados de acordo com o cabeçalho de compactação da solicitação.
> - Se apenas Brotli for selecionado e o cabeçalho de compactação da solicitação não for compatível, os recursos originais serão retornados sem compactação.


