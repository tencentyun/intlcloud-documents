É possível usar um disco em nuvem elástico como disco de dados e montá-lo em qualquer CVM na mesma zona de disponibilidade. Pode-se montar até 20 discos de dados em cada CVM. É possível usar os seguintes métodos para montar um disco em nuvem.
- Ao iniciar um novo CVM, especifique a imagem personalizada correspondente e o snapshot do disco de dados.
Após a montagem automática, as leituras e gravações no disco de dados podem ser realizadas diretamente sem operações de inicialização do disco, como particionamento e formatação.
- Ao adquirir um disco em nuvem elástico, monte-o manualmente em uma instância do CVM existente na mesma zona de disponibilidade pelo console ou por API.
 - Criação de um disco em nuvem diretamente
 Após a montagem manual, é preciso inicializar o disco em nuvem formatando e particionando-o. Para obter mais informações, consulte [Inicialização de discos em nuvem (menores que 2 TB)](https://intl.cloud.tencent.com/document/product/362/31597) ou [Inicialização de discos em nuvem (maiores que 2 TB)](https://intl.cloud.tencent.com/document/product/362/31598).
 - Criação de um disco em nuvem de um snapshot
    Se a capacidade do disco em nuvem for igual ao tamanho do snapshot, é possível ler e gravar diretamente no disco em nuvem sem operações de inicialização do disco, como particionamento e formatação.
	Se a capacidade do disco em nuvem for maior que o tamanho do snapshot, será preciso estender o sistema de arquivos ou converter o formato da partição.

 >?Alguns CVMs do Linux podem não reconhecer um disco em nuvem elástico. Primeiro, é necessário habilitar a funcionalidade de permutação a quente de disco no CVM. Para obter mais informações, consulte [Ativação da funcionalidade de permutação a quente de disco](#modprobeacpiphp).

## Montagem automática
### Montagem de discos de dados (Windows)
Se você usar uma imagem personalizada para criar uma instância do CVM do Windows, o disco em nuvem criado a partir do snapshot do disco de dados correspondente será montado automaticamente. A imagem personalizada e o snapshot do disco de dados devem atender aos seguintes requisitos:
- O disco de dados **deve** ser formatado para `ntfs` ou `fat32` antes de você criar um snapshot.
- A política de SAN na imagem personalizada é `onlineAll`.
 >?O Tencent Cloud fornece imagens públicas pré-configuradas para Windows por padrão, mas ainda recomendamos que você execute as seguintes etapas para verificar as configurações antes de criar uma imagem personalizada.
![](https://main.qcloudimg.com/raw/edac7337395de380c0ec801646e0a627.png)


### Montagem de disco de dados (Linux)
Se você usar uma imagem personalizada para criar uma instância do CVM do Linux, o disco em nuvem criado a partir do snapshot do disco de dados correspondente será montado automaticamente. A imagem personalizada e o snapshot do disco de dados devem atender aos seguintes requisitos:
- O disco de dados **deve** ser formatado e montado com êxito no CVM de origem antes que o snapshot seja criado.
- Adicione os seguintes comandos ao arquivo `/etc/rc.local` para configurar o ponto de montagem do disco de dados antes de criar um disco do sistema no disco do sistema.
 ```
 mkdir -p <mount-point>
 mount <device-id> <mount-point>
 ```
>?
> - Substitua `<mount-point>` pelo ponto de montagem do sistema de arquivos, como `/mydata`.
> - Substitua `<device-id>` pelo caminho da partição do sistema de arquivos. Por exemplo, digite `/dev/vdb` se o sistema de arquivos não tiver partição e `/dev/vdb1` se o sistema de arquivos tiver partições.

## Montagem manual

### Uso do console para montar discos em nuvem
1. Faça login no [Console do CBS](https://console.cloud.tencent.com/cvm/cbs).
2. Na página de lista de discos em nuvem, é possível usar os seguintes métodos para montar discos em nuvem.
 a. Selecione um disco em nuvem com o status **to be mounted (a ser montado)** e clique em **More (Mais)** > **Mount (Montar)** na coluna **Operation (Operação)**.
 b. Selecione vários discos em nuvem com o status **to be mounted (a ser montado)** e clique em **Mount (Montar)** no topo da lista de discos em nuvem.
3. Na caixa pop-up, selecione a instância do CVM de destino e clique em **OK**.
4. Atualize a lista de discos em nuvem.
 Se o status desses discos em nuvem mudar para **Mounted (Montado)**, isso indica que a montagem obteve êxito.
5. Execute as operações subsequentes conforme mostrado abaixo para tornar o disco em nuvem utilizável.
 <table>
 <tr>
 <th>Modo de criação</th>
 <th>Capacidade do disco em nuvem</th>
 <th>Operações subsequentes</th>
 </tr>
 <tr>
 <td  rowspan="2">Criar diretamente</td>
 <td>Capacidade do disco em nuvem < 2 TB</td>
 <td><a href="https://intl.cloud.tencent.com/document/product/362/31597">Inicialização de discos em nuvem (< 2 TB)</a></td>
 </tr>
 <tr>
  <td>Capacidade do disco em nuvem ≥ 2 TB</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/362/31598">Inicialização de discos em nuvem (≥ 2 TB)</a></td>
 </tr>
  <tr>
	<td  rowspan="3">Criar a partir de um snapshot</td>
	<td>Capacidade do disco em nuvem = Capacidade do snapshot</td>
	<td><ul><li>Montagem em um CVM do Windows: depois de fazer login na instância, coloque o disco online por meio de **Server Management (Gerenciamento do servidor)** > **Storage (Armazenamento)** > **Disk Management (Gerenciamento do disco)**.</li>
		<li>Montagem em um CVM do Linux: depois de fazer login na instância, execute o comando <code>mount <disk partition> <mount point></code>, como <code>mount /dev/vdb /mnt</code>.</li>
		</ul>
	</li></td>
 </tr>
 </tr>
 <tr>
 <td nowrap="nowrap">Capacidade do snapshot < capacidade do disco em nuvem ≤ 2 TB <br/>ou<br/>2 TB < capacidade do snapshot < capacidade do disco em nuvem</td>
<td><ul><li>Montagem em um CVM do Windows: <a href="https://intl.cloud.tencent.com/document/product/362/31601">extensão de partições e sistemas de arquivos (Windows)</a></li><li>Montagem em um CVM do Linux: <a href="https://intl.cloud.tencent.com/document/product/362/31602">extensão de partições e sistemas de arquivos (Linux)</a></li></ul></td>
 </tr> 
 <tr>
 <td>Capacidade do snapshot ≤ 2 TB < capacidade do disco em nuvem</td>
<td nowrap="nowrap"><ul><li>Se o snapshot usar o formato de partição MBR:</li>consulte <a href="https://intl.cloud.tencent.com/document/product/362/31598">Inicialização de discos em nuvem (maiores que 2 TB)</a> para usar a partição GPT em vez disso.<b>Essa operação excluirá os dados originais.</b><li>Se o snapshot usar o formato de partição GPT:<ul><li>Montagem em um CVM do Windows:<a href="https://intl.cloud.tencent.com/document/product/362/31601">extensão de partições e sistemas de arquivos (Windows)</a></li><li>Montagem em um CVM do Linux:<a href="https://intl.cloud.tencent.com/document/product/362/31602">extensão de partições e sistemas de arquivos (Linux)</a></li></ul></td>
 </tr> 
 </table>

### Uso de API para montar discos em nuvem
É possível usar a API `AttachDisks` para montar um disco em nuvem. Para obter mais informações, consulte [AttachDisks](https://intl.cloud.tencent.com/document/product/362/16313).

[](id:modprobeacpiphp)
### Ativação da funcionalidade de permutação a quente de disco
Todas as imagens existentes já são compatíveis com a montagem e desmontagem de discos em nuvem elásticos. **Para desmontar um disco em nuvem, primeiro é necessário executar o comando `umount` no CVM do Linux ou realizar operações offline no CVM do Windows. Caso contrário, o disco em nuvem elástico remontado pode não ser reconhecido.**
No entanto, se você deseja montar um disco em nuvem elástico em um CVM com os sistemas operacionais a seguir, recomendamos que primeiro você adicione drivers e ative a funcionalidade de permutação a quente no CVM.
<table>
<tbody>
<tr><th>Sistema operacional do CVM</th><th>Versão</th>
<tr><td rowspan="4">CentOS</td><td>5.11 64 bits</td>
<tr><td>5.11 32 bits</td>
<tr><td>5.8 64 bits</td>
<tr><td>5.8 32 bits</td>
<tr><td >Debian</td><td>6.0.3 32 bits</td>
<tr><td rowspan="2">Ubuntu</td><td>10.04 64 bits</td>
<tr><td>10.04 32 bits</td>
<tr><td rowspan="2">openSUSE</td><td>12.3 64 bits</td>
<tr><td>12.3 32 bits</td>
</tbody>
</table>

1. [Faça login no CVM do Linux](https://intl.cloud.tencent.com/document/product/213/5436) como o usuário raiz.
2. Execute o seguinte comando para adicionar o driver.
```
modprobe acpiphp
```
>?Se você ainda precisa carregar o módulo `acpiphp` depois de desligar ou reiniciar o CVM, recomendamos que você execute a [Etapa 3](#step3) para definir o módulo `acpiphp` para carregamento automático.
<span id="step3"></span> 
3. (Opcional) Execute o seguinte comando de acordo com o sistema operacional para definir o módulo `acpiphp` para carregamento automático:
 - **CentOS 5 Series**
 a. Execute o seguinte comando para criar e abrir o arquivo `acpiphp.modules`.
```
vi /etc/sysconfig/modules/acpiphp.modules
```
b. Adicione o seguinte conteúdo ao arquivo e salve.
```
 #!/bin/bash
 modprobe acpiphp >& /dev/null
```
c. Execute o seguinte comando para conceder permissões de execução no arquivo.
```
chmod a+x /etc/sysconfig/modules/acpiphp.modules
```
 - **Série Debian 6, série Ubuntu 10.04**
 a. Execute o seguinte comando para modificar o arquivo.
```
vi /etc/modules
```
b. Adicione o seguinte conteúdo ao arquivo e salve.
```
acpiphp
```
 - **Série openSUSE 12.3**
 a. Execute o seguinte comando para modificar o arquivo.
```
vi /etc/sysconfig/kernel
```
b. Adicione o seguinte conteúdo ao arquivo e salve.
```
MODULES_LOADED_ON_BOOT="acpiphp"
```
