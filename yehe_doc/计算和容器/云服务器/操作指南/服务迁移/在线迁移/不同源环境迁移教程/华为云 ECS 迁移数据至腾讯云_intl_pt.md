## 1. Obtenção da ferramenta de migração  
 [Clique aqui](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) para obter o pacote de ferramentas de migração compactado.

## 2. Escolha de um modo de migração com base no ambiente de rede
Escolha o modo de migração apropriado de acordo com os ambientes de rede dos seus servidores de origem e CVMs de destino.
Atualmente, a ferramenta de migração é compatível com o modo padrão e o modo de rede privada. O modo de rede privada se aplica a três cenários. Cada modo ou cenário de migração possui diferentes requisitos de rede para os servidores de origem e os CVMs de destino. Se os servidores de origem e os CVMs de destino puderem acessar a rede pública, será possível usar o modo padrão para migração. Se os servidores de origem ou os CVMs de destino não puderem acessar diretamente a rede pública, será necessário estabelecer uma conexão entre eles por meio do [VPC Peering Connections](https://intl.cloud.tencent.com/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003) ou [Direct Connect](https://intl.cloud.tencent.com/document/product/216) antes de usar o modo de rede privada para migração.

## 3. Backup de dados
- Servidor de origem: é possível usar a funcionalidade de snapshot da Huawei Cloud ou outros métodos para fazer o backup dos dados.
- CVM de destino: é possível [criar um snapshot](https://intl.cloud.tencent.com/document/product/362/5755) ou usar outros métodos para fazer o backup dos dados.

## 4. Verificação antes da migração
Antes da migração, verifique os seguintes itens do servidor de origem e do CVM de destino:
<table>
	<tr><th style="width: 15%;">CVM de destino</th><td><ol style="margin: 0;"><li>Armazenamento: os discos em nuvem (incluindo discos do sistema e discos de dados) do CVM de destino devem ter capacidade de armazenamento suficiente para armazenar os dados do servidor de origem.</li><li>Grupo de segurança: as portas 443 e 80 devem estar abertas para a internet em um grupo de segurança.</li><li>Largura de banda: recomendamos que você aumente a largura de banda de entrada e de saída para uma migração mais rápida. O tráfego consumido durante a migração será aproximadamente igual ao volume de dados. Se necessário, altere o método de faturamento da rede com antecedência.</li><li>Sistema operacional: recomendamos o uso do mesmo sistema operacional no servidor de origem e no CVM de destino. Sistemas operacionais diferentes resultarão em inconsistência entre a imagem a ser criada e o sistema operacional real. Por exemplo, ao migrar um servidor de origem com o sistema CentOS 7 instalado, escolha um CVM com o sistema CentOS 7 instalado como destino.</li></ol></td></tr>
	<tr><th>Servidor de origem do Linux</th><td><ol style="margin: 0;"><li>Verifique e instale o Virtio. Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/213/9929">Verificação de drivers Virtio no Linux</a>.</li><li>Verifique se o rsync está instalado executando <code>which rsync</code>.</li><li>Verifique se o SELinux está habilitado. Se estiver, desabilite-o.</li><li>Certifique-se de que a hora atual do sistema esteja correta, porque a API do Tencent Cloud usará o carimbo de data/hora UNIX para verificar o token gerado depois de receber uma solicitação de migração.</li><li>Execute o <code>cloud-init --version</code> para verificar a versão do cloud-init instalado no servidor de origem.<ul><li>Recomendamos que você desmonte ou remova o cloud-init se sua versão for anterior à <code>17.1</code>.</li><li>Ignore essa etapa se o servidor de origem não tiver o cloud-init instalado.</li></ul></li></ol></td></tr>
</table>

>? 
> - É possível usar os comandos da ferramenta para verificar automaticamente o servidor de origem, por exemplo, `sudo ./go2tencentcloud_x64 --check`.
> - Por padrão, a ferramenta de migração go2tencentcloud executa verificações automaticamente na inicialização. Para pular as verificações e realizar a migração forçada, configure `Client.Extra.IgnoreCheck` como `true` no arquivo client.json.
> - Para obter mais informações sobre a ferramenta de migração go2tencentcloud, consulte [Ferramenta de migração](https://intl.cloud.tencent.com/document/product/213/35640).
> 


## 5. Início da migração

1. (Opcional) Estabeleça uma conexão entre o servidor de origem e o CVM de destino. 
 - Se você estiver usando o modo de rede privada, estabeleça uma conexão entre o servidor de origem e o CVM de destino por meio do [VPC Peering Connections](https://intl.cloud.tencent.com/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003) ou [Direct Connect](https://intl.cloud.tencent.com/document/product/216).
 - Pule para a próxima etapa se estiver usando o modo padrão.
2. Configure o arquivo “user.json”.
O arquivo “user.json” é usado para configurar o servidor de origem e o CVM de destino. Ele contém os seguintes itens de configuração:
 - As chaves de API da sua conta, ou seja, `SecretId` e `SecretKey`. Para obter mais informações, consulte [Chave de acesso](https://intl.cloud.tencent.com/document/product/598/32675).
 - A região do CVM de destino. Para obter mais informações sobre as regiões compatíveis, consulte [Regiões e zonas de disponibilidade](https://intl.cloud.tencent.com/document/product/213/6091).
 - O ID da instância do CVM de destino, que pode ser verificado na página [Instâncias](https://console.cloud.tencent.com/cvm/instance/index?rid=1).
 - (Opcional) A configuração do disco de dados do servidor de origem.  
3. Configure o arquivo “client.json”.
O arquivo “client.json” é usado para configurar o modo de migração e outros parâmetros. É necessário configurar o parâmetro `Client.Net.Mode` no arquivo “client.json”, independentemente de quais cenários de migração você selecionar.
4. (Opcional) Exclua os arquivos e os diretórios que não precisarem ser migrados do servidor de origem.  
 Edite o arquivo “rsync\_excludes\_linux.txt” no servidor de origem do Linux para remover os arquivos e os diretórios que não precisarem ser migrados.
5. Execute a ferramenta.
Por exemplo, em um servidor de origem do Linux de 64 bits, execute o seguinte comando como usuário raiz para executar a ferramenta.
```
sudo ./go2tencentcloud_x64
```
Aguarde a conclusão do processo de migração.
Se a mensagem a seguir aparecer no console, a migração foi concluída com êxito.
![](https://main.qcloudimg.com/raw/4768e5bbe1fd1deba16c78eea3a19b02.png)
