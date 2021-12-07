Para instância de **CLB em rede pública ou CLB em rede pública com IP fixo**, a compactação Gzip é habilitada para os protocolos **HTTP e HTTPS** por padrão. Os recursos do Gzip compactam sites, o que reduz efetivamente o volume de dados na transmissão da rede e acelera o acesso do navegador do cliente. Preste atenção ao seguinte:

### Observações

- **Você deve habilitar a compactação Gzip em instâncias do CVM em sincronia**
Para contêineres de serviço Nginx comuns, é preciso habilitar o Gzip nos respectivos arquivos de configuração (nginx.conf por padrão) e reiniciar o serviço
```
gzip on;
```
- **Atualmente, o CLB oferece suporte aos seguintes tipos de arquivo. É possível especificar o tipo de arquivo para compressão no item de configuração gzip_types**
```
application/atom+xml application/javascript application/json application/rss+xml application/vnd.ms-fontobject application/x-font-ttf application/x-web-app-manifest+json application/xhtml+xml application/xml font/opentype image/svg+xml image/x-icon text/css text/plain text/x-component;
```
>!Você deve habilitar o Gzip em sincronia para os tipos de arquivo acima no software comercial das instâncias CVM do CLB.
- **As solicitações do cliente devem conter o identificador de solicitação de compactação**
Para habilitar a compactação Gzip, as solicitações do cliente devem conter o seguinte identificador:
```
Accept-Encoding: gzip,deflate,sdch
```

### Exemplo de ativação do Gzip em instâncias do CVM

Exemplo de ambiente de tempo de execução do CVM: Debian 6

1. Use o Vim para abrir o arquivo de configuração Nginx com base no caminho do usuário:
```
vim /etc/nginx/nginx.conf
```
2. Encontre o seguinte código:
```
gzip on;
gzip_min_length 1k;
gzip_buffers 4 16k;
gzip_http_version 1.1;
gzip_comp_level 2;
gzip_types text/html application/json;
```
Descrição da sintaxe do código acima:
	- gzip: ativa ou desativa o módulo Gzip.
Sintaxe: `gzip on/off`
Escopos: http, server, location
	
	- gzip_min_length: especifica o número mínimo de bytes para a compactação de uma página. O número de bytes pode ser obtido em Content-Length no cabeçalho HTTP. Valor padrão é 1k.
Sintaxe: `gzip_min_length length`
Escopos: http, server, location
	
	- gzip_buffers: especifica a unidade de buffer para armazenar o fluxo de dados do resultado da compressão Gzip. 16k significa que 16k é usado como a unidade e será aplicada memória 4 vezes o tamanho dos dados originais (em 16k).
Sintaxe: `gzip_buffers number size`
Escopos: http, server, location
	
	- gzip_http_version: especifica a versão HTTP mais baixa que pode usar Gzip. Configurar HTTP/1.0 significa que a versão HTTP mais baixa que precisa do Gzip é 1.0, então o Gzip pode ser compatível com HTTP/1.1 ou superior. Você não precisa alterar isso, pois o Tencent Cloud oferece suporte a HTTP/1.1 em toda a rede.
Sintaxe: `gzip_http_version 1.0 | 1.1;`
Escopos: http, server, location

	- gzip_comp_level: especifica a taxa de compressão Gzip com intervalo de valores: 1-9. A menor taxa de compressão com a velocidade de processamento mais rápida é 1, enquanto 9 é a maior taxa de compressão com a velocidade de processamento mais lenta (transmissão rápida com alto consumo de CPU).
Sintaxe: `gzip_comp_level 1..9`
Escopos: http, server, location

	- gzip_types: indica os tipos Multipurpose Internet Mail Extensions (MIME) para compactação e o tipo "text/html" será compactado por padrão. Além disso, o Gzip para Nginx não compacta arquivos de recursos estáticos, como JavaScript e imagens, por padrão. Você pode configurar gzip_types para especificar os tipos MIME a serem compactados. Tipos que não são especificados não serão compactados. **Por exemplo, para compactar dados no formato JSON, você precisa adicionar application/json a esta frase**
Os tipos compatíveis estão abaixo:
```
text/html text/plain text/css application/x-javascript text/javascript application/xml
```
Sintaxe: `gzip_types mime-type [mime-type ...]`
Escopos: http, server, location

3. Para modificar a configuração, salve e saia do arquivo, entre no diretório de arquivos bin do Nginx e execute o seguinte comando para recarregar o Nginx:
```
./nginx -s reload
```
4. Use o comando curl para testar se o Gzip foi habilitado com êxito:
```
curl -I -H "Accept-Encoding: gzip, deflate" "http://cloud.tencent.com/example/"
```
