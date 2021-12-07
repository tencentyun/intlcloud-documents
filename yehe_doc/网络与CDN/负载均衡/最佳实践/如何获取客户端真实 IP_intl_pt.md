## Observações sobre como obter IPs de clientes reais por CLB
Todos os serviços CLB da camada 4 (TCP/UDP/TCP SSL) e da camada 7 (HTTP/HTTPS) oferecem suporte à obtenção de um IP de cliente real diretamente em uma instância do CVM de back-end sem nenhuma configuração adicional necessária.
- Para CLB da camada 4, o IP de origem obtido na instância do CVM de back-end é o IP do cliente.
- Para CLB da camada 7, você pode usar o campo `X-Forwarded-For` ou `remote_addr` para obter diretamente o IP do cliente. Para obter os registros de acesso do CLB da camada 7, consulte [Armazenando registros de acesso no CLS] (https://intl.cloud.tencent.com/document/product/214/35063). 

>?
> - Para instâncias do CLB da camada 4, o IP do cliente pode ser obtido diretamente sem a necessidade de configuração adicional na instância do CVM de back-end.
> - Para outros serviços de balanceamento de carga da camada 7 com SNAT habilitado, você precisa configurar a instância do CVM de back-end e então usar `X-Forwarded-For` para obter o IP do cliente real.

Abaixo estão os esquemas de configuração de servidor de aplicativos comumente usados.

## Esquema de configuração do IIS 6
1. Baixe e instale o módulo de plug-in [F5XForwardedFor](https://devcentral.f5.com/s/articles/x-forwarded-for-log-filter-for-windows-servers), copie `F5XForwardedFor.dll` no diretório `x86\Release` ou `x64\Release` com base na versão do sistema operacional do servidor para um determinado diretório (como`C:\ISAPIFilters` neste documento) e certifique-se de que o processo do IIS tenha permissão de leitura para este diretório.
2. Abra o Gerenciador do IIS, encontre o site atualmente aberto, clique com o botão direito do mouse no site e selecione **Properties (Propriedades)** para abrir a página de propriedades.
3. Na página de propriedades, mude para **ISAPI Filters (Filtros ISAPI)** e clique em **Add (Adicionar)** para abrir a janela "Add (Adicionar)".
4. Na janela "Add (Adicionar)", digite "F5XForwardedFor" para "Filter Name (Nome do filtro)" e o caminho completo para `F5XForwardedFor.dll` para "Executable (Executável)" e clique em **OK**.
5. Reinicie o servidor IIS para que a configuração tenha efeito.

## Esquema de configuração do IIS 7
1. Baixe e instale o módulo de plug-in [F5XForwardedFor](https://devcentral.f5.com/s/articles/x-forwarded-for-log-filter-for-windows-servers), copie `F5XFFHttpModule.dll` e `F5XFFHttpModule.ini` no diretório `x86\Release` ou `x64\Release` com base na versão do sistema operacional do seu servidor para um determinado diretório (como `C:\x_forwarded_for` neste documento) e certifique-se de que o processo do IIS tem permissão de leitura para este diretório.
2. Selecione **IIS Server (Servidor IIS)** e clique duas vezes em **Modules (Módulos)**.
![](https://main.qcloudimg.com/raw/21372379584488e72ae3d22af44a5017.png)
3. Clique em **Configure Native Modules (Configurar módulos nativos)**.
![](https://main.qcloudimg.com/raw/280f11e95b7ac8cd4a754d98ad0cd2b7.png)
4. Na caixa pop-up, clique em **Register (Registrar)**.
![](https://main.qcloudimg.com/raw/1d6f7bd38077f2c9f089eb84a1995aa1.png)
5. Adicione os arquivos DLL baixados conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/354a35a203c24d802d59782c91dfe02a.png)
6. Após adicionar os arquivos, verifique-os e clique em **OK**.
![](https://main.qcloudimg.com/raw/9fffdfa02fba225f13090ef2598e1c0e.png)
7. Adicione os dois arquivos DLL acima em "ISAPI and CGI Restrictions (Restrições ISAPI e CGI)" e defina as restrições para "Permitir".
![](https://main.qcloudimg.com/raw/8585122da39f14d734eb9d6ded7e486c.png)
8. Reinicie o servidor IIS para que a configuração tenha efeito.

## Esquema de configuração do Apache
1. Instalar o módulo Apache de terceiros "mod_rpaf".
```
wget http://stderr.net/apache/rpaf/download/mod_rpaf-0.6.tar.gz
tar zxvf mod_rpaf-0.6.tar.gz
cd mod_rpaf-0.6
/usr/bin/apxs -i -c -n mod_rpaf-2.0.so mod_rpaf-2.0.c
```
2. Modificar a configuração do Apache `/etc/httpd/conf/httpd.conf` adicionando o seguinte ao final do arquivo:
```
LoadModule rpaf_module modules/mod_rpaf-2.0.so
RPAFenable On
RPAFsethostname On
RPAFproxy_ips IP address (este não é o IP público fornecido pelo CLB. Para o IP específico, consulte os logs do Apache. Geralmente, existem dois endereços IP e você precisa inserir os dois)
RPAFheader X-Forwarded-For
```
3. Depois de adicionar o conteúdo acima, reinicie o Apache.
```
/usr/sbin/apachectl restart
```

## Esquema de configuração do Nginx
1. Você pode usar `http_realip_module` para obter o IP do cliente real quando o Nginx é usado como o servidor. No entanto, este módulo não é instalado no Nginx por padrão, e você precisa recompilar o Nginx para adicionar `--with-http_realip_module`.
```
wget  http://nginx.org/download/nginx-1.14.0.tar.gz 
tar  zxvf nginx-1.14.0.tar.gz 
cd nginx-1.14.0
./configure --user=www --group=www --with-http_stub_status_module --without-http-cache --with-http_ssl_module --with-http_realip_module
make
make install
```
2. Modifique `nginx.conf`.
```
vi /etc/nginx/nginx.conf
```
Modifique o conteúdo em vermelho da seguinte forma:
<div class="code">
<p>
</p>
<pre>  
fastcgi connect_timeout 300;
fastcgi send_timeout 300;
fastcgi read_timeout 300;
fastcgi buffer_size 64k;
fastcgi buffers 4 64k;
fastcgi busy_buffers_size 128k;
fastcgi temp_file_write_size 128k;
<font color="#f2777a">
set_real_ip_from IP address; (este não é o IP público fornecido pelo CLB. Para o IP específico, consulte os logs do Nginx. Você precisa inserir todos os endereços IP, se houver vários)
real_ip_header X-Forwarded-For;
 </font>
</pre>
</div>
3. Reinicie o Nginx.
```
service nginx restart
```
