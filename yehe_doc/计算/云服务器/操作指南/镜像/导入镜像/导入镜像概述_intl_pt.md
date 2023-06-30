Além da [criação de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4942), o Tencent Cloud permite que você importe imagens. É possível importar um arquivo de imagem do disco do sistema em um servidor local ou diferente para imagens personalizadas do CVM. Você pode usar a imagem importada para criar um CVM ou reinstalar o sistema operacional para um CVM existente.

<span id="Preparations"></span>
## Preparações

Prepare um arquivo de imagem que atenda aos requisitos de importação.
- **Requisitos para imagens do Linux:**
<table>
<tr><th style="width:16%">Atributo da imagem</th><th>Requisitos</th></tr>
<tr><td>Sistema operacional</td><td><ul><li>CentOS, Ubuntu, Debian, CoreOS, OpenSUSE e SUSE</li><li>Ambos os sistemas operacionais de 32 e 64 bits são compatíveis.</li></ul></td></tr>
<tr><td>Formato da imagem</td><td><ul><li>RAW, VHD, QCOW2 e VMDK</li><li>Execute <code>qemu-img info imageName | grep 'file format'</code> para verificar o formato da imagem.</li></ul></td></tr>
<tr><td>Tipo de sistema de arquivos</td><td>A partição GPT não é compatível.</td></tr>
<tr><td>Tamanho da imagem</td><td><ul><li>O tamanho real da imagem não pode exceder 50 GB. Execute <code>qemu-img info imageName | grep 'disk size'</code> para verificar o tamanho da imagem.</li><li>O vsize da imagem não pode exceder 500 GB. Execute <code>qemu-img info imageName | grep 'virtual size'</code> para verificar o vsize da imagem.</li></ul><b>Observação: </b>o tamanho de uma imagem no formato QCOW2 é usado na verificação durante a importação.</td></tr>
<tr><td>Rede</td><td><ul><li>Por padrão, o Tencent Cloud fornece a interface de rede <code>eth0</code> para a instância.</li><li>É possível usar o serviço de metadados para consultar a configuração de rede da instância. Para obter mais informações, consulte os <a href="https://intl.cloud.tencent.com/document/product/213/4934">Metadados da instância</a>.</li></ul></td></tr>
<tr><td>Driver</td><td><ul><li>O driver Virtio do módulo de virtualização KVM deve estar instalado para uma imagem. Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/213/9929">Verificação de drivers Virtio no Linux</a>.</li><li>Recomendamos instalar o cloud-init para a imagem. Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/213/12587">Instalação do Cloud-Init no Linux</a>. </li><li>Se o cloud-init não puder ser instalado, configure a instância referindo-se a <a href="https://intl.cloud.tencent.com/document/product/213/12849">Importação forçada de imagem</a>.</li></ul></td></tr>
<tr><td>Kernel</td><td>Prefere-se o kernel nativo para uma imagem. Qualquer modificação no kernel pode causar falha na importação.</td></tr>
<tr><td>Região</td><td>A importação de imagens do COS em outra região não está disponível para Finanças de Xangai e Finanças de Shenzhen.</td></tr>
</table>
- **Requisitos para imagens do Windows:**
<table>
<tr><th style="width:16%">Atributo da imagem</th><th>Requisitos</th></tr>
<tr><td>Sistema operacional</td><td><ul><li>Versões relacionadas ao Windows Server 2008, Windows Server 2012 e Windows Server 2016</li><li>Ambos os sistemas operacionais de 32 e 64 bits são compatíveis.</li></ul></td></tr>
<tr><td>Formato da imagem</td><td><ul><li>RAW, VHD, QCOW2 e VMDK</li><li>Execute <code>qemu-img info imageName | grep 'file format'</code> para verificar o formato da imagem.</li></ul></td></tr>
<tr><td>Tipo de sistema de arquivos</td><td><ul><li>Apenas NTFS com partição MBR é compatível.</li><li>A partição GPT não é compatível.</li><li>O Gerenciamento de volume lógico (LVM) não é compatível.</li></ul></td></tr>
<tr><td>Tamanho da imagem</td><td><ul><li>O tamanho real da imagem não pode exceder 50 GB. Execute <code>qemu-img info imageName | grep 'disk size'</code> para verificar o tamanho da imagem.</li><li>O vsize da imagem não pode exceder 500 GB. Execute <code>qemu-img info imageName | grep 'virtual size'</code> para verificar o vsize da imagem.</li></ul><b>Observação: </b>o tamanho de uma imagem no formato QCOW2 é usado na verificação durante a importação.</td></tr>
<tr><td>Rede</td><td><ul><li>Por padrão, o Tencent Cloud fornece a interface de rede de <code>conexão de área local</code> para a instância. </li><li>É possível usar o serviço de metadados para consultar a configuração de rede da instância. Para obter mais informações, consulte os <a href="https://intl.cloud.tencent.com/document/product/213/4934">Metadados da instância</a>.</li></ul></td></tr>
<tr><td>Driver</td><td>O driver Virtio do módulo de virtualização KVM deve estar instalado para uma imagem. O sistema Windows não vem com um driver Virtio por padrão, então instale o driver Virtio do Windows antes de exportar uma imagem local. Escolha o endereço de download com base no ambiente de rede:<ul><li>Endereço de download da internet:<code>http://mirrors.tencent.com/install/windows/virtio_64_1.0.9.exe</code></li><li>Endereço de download da rede privada:<code>http://mirrors.tencentyun.com/install/windows/virtio_64_1.0.9.exe</code></li></ul></td></tr>
<tr><td>Região</td><td>A importação de imagens do COS em outra região não está disponível para Finanças de Xangai e Finanças de Shenzhen.</td></tr>
<tr><td>Outros</td><td>As imagens importadas do Windows <b>não são compatíveis com a </b><a href="https://intl.cloud.tencent.com/document/product/213/2757">ativação do sistema Windows</a>.</td></tr>
</table>

## Instruções

 1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
 2. Na barra lateral esquerda, clique em **[Images (Imagens)](https://console.cloud.tencent.com/cvm/image)**.
 3. Selecione **Custom Image (Imagem personalizada)** e clique em **Import Image (Importar imagem)**.
 4. [Ative o Cloud Object Storage](https://console.cloud.tencent.com/cos4/index) e depois [crie o bucket](/doc/product/436/6232). Carregue o arquivo de imagem para o bucket e obtenha o [URL do arquivo de imagem](/doc/product/436/6260).
 5. Clique em **Next (Avançar)**.
 6. Conclua as configurações e clique em **Import (Importar)**.
 >! Certifique-se de que o URL do arquivo COS inserido esteja correto.
 >
Você será notificado sobre o resultado da importação pelo [Centro de mensagens](https://console.cloud.tencent.com/message) do console.

## Importações com falha

Se a importação falhou, solucione o problema da seguinte maneira:

### Observações

Certifique-se de que você se inscreveu para receber notificações de serviços de produtos pela [Assinatura de mensagens](https://console.cloud.tencent.com/messageCenter/messageConfig). Isso garante que você possa receber mensagens internas, mensagens SMS e e-mails sobre a causa da falha.
>! Se você não assinar as notificações de serviços de produtos, não receberá a mensagem interna se uma importação obteve êxito.

### Solução de problemas

Para obter mais informações sobre mensagens e descrições de erros, consulte [Códigos de erro](#errorcode).

#### InvalidUrl: URL inválido do COS

O erro InvalidUrl indica que um URL incorreto do COS foi inserido. As possíveis causas são:
* O URL da imagem que você inseriu não é um URL de imagem do [Cloud Object Storage](https://console.cloud.tencent.com/cos4/index).
* A permissão do URL do COS não é de leitura pública e gravação privada.
* A permissão de acesso do arquivo do COS é de leitura privada, mas a assinatura expirou.
>! O URL do COS com a assinatura só pode ser acessado uma vez.
>
* Foi inserido um URL do COS de outra região.
>! O serviço de importação de imagens acessa o servidor do COS na região local por meio da rede privada.
>
* O arquivo de imagem do usuário foi excluído.
* Foi usado um URL do COS com a assinatura.
Se você receber a mensagem de erro sobre um URL inválido do COS, solucione o problema com base nos motivos acima.

#### InvalidFormatSize: formato ou tamanho inválido

O erro InvalidFormatSize indica que o formato ou o tamanho de uma imagem a ser importada não atende aos seguintes requisitos do Tencent Cloud:
* Os formatos de arquivo de imagem aceitos são `qcow2`,` vhd`, `vmdk` e `raw`.
* O tamanho de um arquivo de imagem a ser importado não pode exceder 50 GB (com base no tamanho no formato qcow2).
* O tamanho do disco do sistema para o qual a imagem é importada não pode exceder 500 GB.

Se você receber uma mensagem de erro informando que o formato ou o tamanho da imagem é inválido:
- Converta o arquivo de imagem em um formato apropriado de acordo com a [Criação de imagens no Linux](https://intl.cloud.tencent.com/document/product/213/17814), reduza o conteúdo da imagem para atender aos requisitos de tamanho e depois importe-o novamente.
- Também é possível usar a funcionalidade [migração de instância offline](https://console.cloud.tencent.com/csm/importOfflineCvm) para migrar a instância. Essa funcionalidade aceita a migração de arquivos de imagem de até 500 GB.

#### VirtioNotInstall: driver Virtio não instalado

O erro VirtioNotInstall indica que a imagem a ser importada não tem o driver Virtio instalado. O Tencent Cloud usa a tecnologia de virtualização KVM e requer que os usuários instalem o driver Virtio na imagem a ser importada. Exceto por alguns sistemas operacionais Linux personalizados, a maioria dos sistemas operacionais Linux tem o driver Virtio instalado. Nos sistemas operacionais Windows, os usuários precisam instalar manualmente o driver Virtio:
- Para importação de imagens do Linux, consulte [Verificação de drivers Virtio no Linux](https://intl.cloud.tencent.com/document/product/213/9929).
- Para importação de imagens do Windows, consulte [Criação de imagens no Windows](https://intl.cloud.tencent.com/document/product/213/17815) para instalar o driver Virtio.

#### CloudInitNotInstalled: programa cloud-init não instalado

O erro CloudInitNotInstalled indica que a imagem a ser importada não tem o cloud-init instalado. O Tencent Cloud usa o software livre cloud-init para inicializar o CVM. Se o cloud-init não estiver instalado, a inicialização do CVM falhará.
* Para importação de imagens do Linux, consulte [Instalação do Cloud-Init no Linux](https://intl.cloud.tencent.com/document/product/213/12587).
* Para importação de imagens do Windows, consulte [Instalação do Cloudbase-Init no Windows](https://intl.cloud.tencent.com/document/product/213/32364).
* Após a instalação do cloud-init ou do cloudbase-init, substitua o arquivo de configuração com base no documento correspondente para que o CVM possa extrair os dados da fonte de dados correta na inicialização.

#### PartitionNotPresent: informações de partição não encontradas

O erro PartitionNotPresent indica que a imagem importada está incompleta. Verifique se a partição de inicialização foi incluída quando a imagem foi criada.

#### RootPartitionNotFound: partição raiz não encontrada

O erro RootPartitionNotFound indica que não foi possível detectar a partição raiz na imagem a ser importada. Verifique o arquivo de imagem. As possíveis causas são:
* O pacote de instalação foi carregado.
* A imagem do disco de dados foi carregada.
* A imagem da partição de inicialização foi carregada.
* Um arquivo incorreto foi carregado.

#### InternalError: erro desconhecido

O erro InternalError indica que a causa do erro ainda não foi registrada. Entre em contato com o atendimento ao cliente para nossa equipe técnica ajudar a resolver o problema.

<a id="errorcode"></a>
## Códigos de erro
 
| Código de erro | Motivo | Solução recomendada |
|-----|-----|-----|
| InvalidUrl | Link inválido do COS. | Verifique se o URL do COS é o mesmo que o URL da imagem importada. |
| InvalidFormatSize | O formato ou o tamanho não atende aos requisitos. | As imagens devem atender aos requisitos de `formato de imagem` e `tamanho da imagem` em [Preparações](#PreparationsforImport). |
| VirtioNotInstall | O driver Virtio não está instalado. | Instale o driver Virtio na imagem consultando a seção `Driver` em [Preparações](#PreparationsforImport). |
| PartitionNotPresent | Informações de partição não encontradas. | A imagem está corrompida possivelmente devido a um método de criação de imagem incorreto. |
| CloudInitNotInstalled | O software cloud-init não está instalado. | Instale o cloud-init na imagem do Linux consultando a seção `Driver` em [Preparações](#PreparationsforImport). |
| RootPartitionNotFound | Partição raiz não encontrada. | A imagem está corrompida possivelmente devido a um método de criação de imagem incorreto. |
| InternalError | Outros erros. | Entre em contato com o atendimento ao cliente. |

