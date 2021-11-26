## Cenário
Este documento usa os discos em nuvem com capacidade maior ou igual a 2 TB como exemplo para fornecer orientação sobre a inicialização de discos. Para obter mais informações, consulte os [Cenários de inicialização](https://intl.cloud.tencent.com/document/product/362/31596).
MBR é compatível com disco com capacidade máxima de 2 TB. Ao particionar um disco com capacidade maior que 2 TB, recomendamos que você use o formato de partição GPT. Quando se usa GPT no sistema operacional Linux, não é mais possível usar o fdisk e deve-se usar a ferramenta parted.

## Pré-requisitos
Ter [montado um disco em nuvem](https://intl.cloud.tencent.com/document/product/362/32401) no seu CVM.

## Observações
- Para proteger dados importantes, consulte as [Perguntas frequentes de uso](https://intl.cloud.tencent.com/document/product/362/32409) antes de operar nos seus discos em nuvem.
- A formatação de um disco de dados apagará todos os dados. Certifique-se de que o disco não contenha dados ou de que foi feito backup dos dados importantes.
- Para evitar exceções, verifique antes de formatar se o CVM interrompeu os serviços externos.

## Instruções

<dx-tabs>
:::sInicialização\sde\sdiscos\sem\snuvem\s(Windows) [](id:2TBWindows2013)
Este documento usa o sistema operacional Windows Server 2012 como exemplo. A operação de formatação varia de acordo com o sistema operacional. As informações abaixo são apenas para referência.

1. [Faça login no Cloud Virtual Machine do Windows](https://intl.cloud.tencent.com/document/product/213/5435).
2. Na área de trabalho do CVM, clique em <img src="https://main.qcloudimg.com/raw/0a02193a82217974f650bbcaf4e1ed2d.png"  style="margin:0;"> para acessar a página **Server Manager (Gerenciador do servidor)**.
3. Na árvore de navegação à esquerda, clique em **File and Storage Services (Serviços de arquivos e armazenamento)**.
4. Na árvore de navegação à esquerda, selecione **Volumes** > **Disks (Discos)**.

Se o disco recém-adicionado estiver com o status offline (conforme exibido na figura acima), realize a [Etapa 5](#online) antes da [Etapa 6](#initialize) para inicializar. Caso contrário, você pode realizar diretamente a [Etapa 6](#initialize).

<span id="online"></span>
5. Os discos são listados no painel do lado direito. Clique com o botão direito na linha onde o 1 está localizado e selecione **Online** para que ele fique online. O status do 1 muda de **Offline** para **Online**.

<span id="initialize"></span>
6. Clique com o botão direito na linha onde o 1 está localizado e selecione **Initialize (Inicializar)** no menu.
7. Siga as instruções na interface e clique em **Yes (Sim)**.
8. Após a inicialização, a partição do 1 muda de **Unknown (Desconhecido)** para **GPT**. Clique com o botão direito na linha onde o 1 está localizado e selecione **New Simple Volume (Novo volume simples)** no menu.
9. Na caixa de diálogo pop-up **New Volume Wizard (Assistente do novo volume)**, siga as instruções na interface e clique em **Next (Avançar)**.
10. Selecione o servidor e o disco e clique em **Next (Avançar)**.
11. Especifique o tamanho do volume conforme necessário, que é o valor máximo por padrão. Clique em **Next (Avançar)**.
12. Atribua uma letra de unidade e clique em **Next (Avançar)**.
13. Selecione **Format this volume with the following settings (Formatar este volume com as seguintes configurações)**, configure os parâmetros conforme necessário, formate a partição e clique em **Next (Avançar)** para concluir a criação da partição.
14. Confirme as informações e clique em **Create (Criar)**.
15. Aguarde até que o sistema conclua a criação do novo volume e clique em **Finish (Concluir)**.
 Após concluir a inicialização, acesse a interface **My Computer (Meu computador)** para exibir o novo disco.

:::
:::Inicialização\sde\sdiscos\sem\snuvem\s(Linux) [](id:2TBLinux)

Selecione o método de inicialização de acordo com seus cenários de uso reais:
- Se todo o disco for apresentado como uma partição independente (ou seja, não há discos lógicos como vdb1 e vdb2), recomendamos fortemente que você não use a partição e [crie diretamente o sistema de arquivos em dispositivos vazios](#CreateFileSystemOnBareDevice).
- Se todo o disco for apresentado como várias partições lógicas (ou seja, há vários discos lógicos), é necessário executar a operação de partição primeiro e, em seguida, [criar o sistema de arquivos em uma partição](#CreateFileSystemOnPartition).

<span id="CreateFileSystemOnBareDevice"></span>
#### Criação de sistemas de arquivos em dispositivos vazios

1. [Faça login no Cloud Virtual Machine do Linux](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute o seguinte comando como usuário raiz para exibir o nome do disco.
 ```
fdisk -l
 ```
 Se informações semelhantes às exibidas abaixo forem retornadas, o CVM atual tem dois discos, em que “/dev/vda” é o disco do sistema e “/dev/vdb” é o disco de dados recém-adicionado.
 ![](https://main.qcloudimg.com/raw/aad842b12fec3ca583790bff609c9fb7.png)
3. Execute o seguinte comando para criar um sistema de arquivos no dispositivo “/dev/vdb” vazio.
```
mkfs -t <File system format> /dev/vdb
```
O tamanho da partição suportado por diferentes sistemas de arquivos varia. Selecione um sistema de arquivos apropriado conforme necessário. O exemplo a seguir usa o `EXT4` como sistema de arquivos:
```
mkfs -t ext4 /dev/vdb
```
> A formatação demora um pouco. Preste atenção ao status de execução do sistema e não feche.
4. Execute o seguinte comando para criar um novo ponto de montagem.
```
mkdir <Mount point>
```
Considere a criação de um novo ponto de montagem `/data` como exemplo:
```
mkdir /data
```
5. Execute o seguinte comando para montar a partição recém-criada no ponto de montagem recém-criado.
```
mount /dev/vdb <Mount point>
```
Considere o ponto de montagem recém-criado `/data` como exemplo:
```
mount /dev/vdb /data
```
6. Execute o seguinte comando para exibir o resultado da montagem.
```
df -TH
```
>Se não for preciso configurar a montagem automática de discos na inicialização, pule as etapas a seguir.
7. Confirme o método de montagem e obtenha as informações correspondentes.
Com base nas necessidades empresariais, é possível usar o soft link de um disco em nuvem elástico, o UUID do sistema de arquivos (identificador exclusivo universal) ou o nome do dispositivo para montar um disco automaticamente. As descrições e os métodos de aquisição de informações são os seguintes:
<table>
 <tr>
     <th>Método de montagem</th>
		 <th>Vantagens e desvantagens</th>
		 <th>Método de aquisição de informações</th>
 </tr>
 <tr>
     <td nowrap="nowrap">Use o soft link do disco em nuvem elástico<b>(recomendado)</b></td>
		 <td><b>Vantagens:</b>o soft link de um disco em nuvem elástico é fixo e único. Ele não muda com operações como montagem, desmontagem e formatação de partições.</br><b>Desvantagens:</b>apenas um disco em nuvem elástico pode usar o soft link, que opera de forma transparente para a operação de formatação da partição.</td>
		 <td nowrap="nowrap">Execute o seguinte comando para exibir o soft link do disco em nuvem elástico.</br><pre>ls -l /dev/disk/by-id</pre></td>
 </tr>
 <tr>
     <td nowrap="nowrap">Use o UUID do sistema de arquivos</td>
		 <td>A configuração de montagem automática pode falhar devido a mudanças no UUID de um sistema de arquivos.</br>Por exemplo, reformatar um sistema de arquivos mudará seu UUID.</td>
		 <td nowrap="nowrap">Execute o seguinte comando para exibir o UUID do sistema de arquivos.</br><pre>blkid /dev/vdb</pre></td>
 </tr>
 <tr>
     <td nowrap="nowrap">Use o nome do dispositivo</td>
		 <td>A configuração da montagem automática pode falhar devido a mudanças no nome do dispositivo.</br>Por exemplo, se um disco em nuvem elástico no CVM for desmontado e depois remontado, o nome do dispositivo pode mudar quando o sistema operacional reconhecer o sistema de arquivos novamente.</td>
		 <td nowrap="nowrap">Execute o seguinte comando para exibir o nome do dispositivo.</br><pre>fdisk -l</pre></td>
	</tr>
</table>
8. Execute o seguinte comando para fazer backup do arquivo `/etc/fstab` para o diretório `/home`, por exemplo:
```
cp -r /etc/fstab /home
```
9. Execute o seguinte comando para usar o editor VI para abrir o arquivo `/etc/fstab`.
```
vi /etc/fstab
```
10. Pressione **i** para entrar no modo de edição.
11. Mova o cursor para o final do arquivo, pressione **Enter** e adicione o seguinte conteúdo.
```
<Device information> <Mount point> <File system format> <File system installation option> <File system dump frequency> <File system check sequence at launch>
```
 - **(Recomendado)** Considere a montagem automática usando o soft link de um disco em nuvem elástico como exemplo. Adicione o seguinte ao exemplo anterior:
```
/dev/disk/by-id/virtio-disk-drkhklpe /data ext4 defaults 0 0
```
 - Considere a montagem automática usando o UUID da partição do disco como exemplo. Adicione o seguinte ao exemplo anterior:
```
UUID=d489ca1c-5057-4536-81cb-ceb2847f9954 /data  ext4 defaults     0   0
```
 - Considere a montagem automática usando o nome do dispositivo como exemplo. Adicione o seguinte ao exemplo anterior:
```
/dev/vdb /data   ext4 defaults     0   0
```
12. Pressione **Esc**, digite **:wq** e pressione **Enter**.
Salve a configuração e feche o editor.
13. Execute o seguinte comando para verificar se o arquivo `/etc/fstab` foi gravado com êxito.
```
mount -a 
```
Se o comando for executado com êxito, o arquivo foi gravado. O sistema de arquivos recém-criado será montado automaticamente quando o sistema operacional for iniciado.

<span id="CreateFileSystemOnPartition"></span>
#### Criação de um sistema de arquivos em uma partição

Este exemplo usa a ferramenta de partição parted no sistema operacional CentOS 7.5 para configurar o disco de dados `/dev/vdc` como a partição principal. GPT foi usado como o formato de partição padrão, o formato EXT4 como o sistema de arquivos, `/data/newpart2` como o ponto de montagem e a montagem automática na inicialização foi configurada. A operação de formatação varia de acordo com o sistema operacional. As informações abaixo são apenas para referência.

1. [Faça login no Cloud Virtual Machine do Linux](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute o seguinte comando como usuário raiz para exibir o nome do disco.
 ```
lsblk
 ```
Se informações semelhantes às exibidas abaixo forem retornadas, o CVM atual tem dois discos, em que “/dev/vda” é o disco do sistema e “/dev/vdc” é o disco de dados recém-adicionado.
	![](https://main.qcloudimg.com/raw/72a7a48c59c13a44958a6b1aa0407ac2.png)
3. Execute o seguinte comando para abrir a ferramenta de partição parted e executar a operação de partição no disco de dados recém-adicionado.
```
parted <Newly added data disk>
```
Considere o disco de dados recém-montado `/dev/vdc` como exemplo:
```
parted /dev/vdc
```
As informações retornadas são semelhantes às exibidas abaixo:
![](https://main.qcloudimg.com/raw/0b2c9164f9fec125a72dee8861b7327d.png)
4. Digite `p` e pressione Enter para exibir o formato de partição do disco atual.
 As informações retornadas são semelhantes às exibidas abaixo:
 ![](https://main.qcloudimg.com/raw/af906521dd6a7f3b948cfad42745aaba.png)
 **Partition Table: unknown (Tabela de partições: desconhecido)** indica que o formato da partição do disco é desconhecido.
5. Execute o seguinte comando para configurar o formato da partição do disco.
```
mklabel <Disk partition format>
```
Se a capacidade do disco for maior ou igual a 2 TB, apenas o formato de partição GPT pode ser usado:
```
mklabel gpt
```
6. Digite `p` e pressione Enter para verificar se o formato de partição do disco foi configurado com êxito.
 As informações retornadas são semelhantes às exibidas abaixo:
	![](https://main.qcloudimg.com/raw/3dfec9aba75cd3cb6dcfb06729f5ff26.png)
 **Partition Table: gpt (Tabela de partições: gpt)** indica que o formato da partição do disco é GPT.
7. Digite `unit s` e pressione Enter para configurar a unidade de medida do disco como setor.
8. Considere a criação de uma partição para todo o disco como exemplo, digite `mkpart opt 2048s 100%` e pressione Enter.
 2048s indica a capacidade inicial do disco e 100% indica a capacidade final do disco. Essas informações são apenas para referência. É possível escolher o número de partições de disco e suas capacidades com base nas suas necessidades empresariais.
9. Digite `p` e pressione Enter para exibir as informações sobre a partição recém-criada.
    As informações retornadas são semelhantes às exibidas abaixo:
 ![](https://main.qcloudimg.com/raw/ee406e75c689f48d59e863adc768aa36.png)
 Isso indica as informações detalhadas da partição recém-criada `/dev/vdc1`.
10. Digite `q` e pressione Enter para fechar a ferramenta de partição parted.
11. Execute o seguinte comando para exibir o nome do disco.
 ```
lsblk
 ```
As informações retornadas são semelhantes às exibidas abaixo. Agora você pode ver a nova partição “/dev/vdc1”.
![](https://main.qcloudimg.com/raw/f95f599f11f88b8bcb89d4f02bb41292.png)
12. Execute o seguinte comando para configurar o sistema de arquivos da partição recém-criada para o que é exigido pelo sistema.
```
mkfs -t <File system format> /dev/vdc1
```
O tamanho da partição suportado por diferentes sistemas de arquivos varia. Selecione um sistema de arquivos apropriado conforme necessário. O exemplo a seguir usa o `EXT4` como sistema de arquivos:
```
mkfs -t ext4 /dev/vdc1
```
 As informações retornadas são semelhantes às exibidas abaixo:
 ![](https://main.qcloudimg.com/raw/3cd6bbd019dd9bdc85ad4ed11ba64f0b.png)
 A formatação demora um pouco. Preste atenção ao status de execução do sistema e não feche.
13. Execute o seguinte comando para criar um novo ponto de montagem.
```
mkdir <Mount point>
```
Considere a criação de um novo ponto de montagem `/data/newpart2` como exemplo:
```
mkdir /data/newpart2
```
14. Execute o seguinte comando para montar a partição recém-criada no ponto de montagem recém-criado.
```
mount /dev/vdc1 <Mount point>
```
Considere o ponto de montagem recém-criado `/data/newpart2` como exemplo:
```
mount /dev/vdc1 /data/newpart2
```
15. Execute o seguinte comando para exibir o resultado da montagem.
```
df -TH
```
 As informações retornadas são semelhantes às exibidas abaixo:
 ![](https://main.qcloudimg.com/raw/774c2d9ff266634c4836df6456b9dd4d.png)
 Isso indica que a partição recém-criada `/dev/vdc1` foi montada em `/data/newpart2`.

Se não for preciso configurar a montagem automática de discos na inicialização, pule as etapas a seguir.

16. Confirme o método de montagem e obtenha as informações correspondentes.
 Com base nas necessidades empresariais, é possível usar o soft link de um disco em nuvem elástico, o UUID do sistema de arquivos (identificador exclusivo universal) ou o nome do dispositivo para montar um disco automaticamente. As descrições e os métodos de aquisição de informações são os seguintes:
 <table>
     <tr>
         <th>Método de montagem</th>  
         <th>Vantagens e desvantagens</th>  
         <th>Método de aquisição de informações</th>  
     </tr>
	   <tr>      
         <td nowrap="nowrap">Use o soft link do disco em nuvem elástico<b>(recomendado)</b></td>   
	       <td><b>Vantagens:</b>o soft link de um disco em nuvem elástico é fixo e único. Ele não muda com operações como montagem, desmontagem e formatação de partições.</br><b>Desvantagens:</b>apenas um disco em nuvem elástico pode usar o soft link, que opera de forma transparente para a operação de formatação da partição.</td>
	       <td nowrap="nowrap">Execute o seguinte comando para exibir o soft link do disco em nuvem elástico.</br><pre>ls -l /dev/disk/by-id</pre></td>
     </tr> 
	   <tr>      
         <td nowrap="nowrap">Use o UUID do sistema de arquivos</td>   
	       <td>A configuração de montagem automática pode falhar devido a mudanças no UUID de um sistema de arquivos.</br>Por exemplo, reformatar um sistema de arquivos mudará seu UUID.</td>
	       <td nowrap="nowrap">Execute o seguinte comando para exibir o UUID do sistema de arquivos.</br><pre>blkid /dev/vdc1</pre></td>
     </tr> 
	   <tr>      
         <td nowrap="nowrap">Use o nome do dispositivo</td>   
	       <td>A configuração da montagem automática pode falhar devido a mudanças no nome do dispositivo.</br>Por exemplo, se um disco em nuvem elástico no CVM for desmontado e depois remontado, o nome do dispositivo pode mudar quando o sistema operacional reconhecer o sistema de arquivos novamente.</td>
	       <td>Execute o seguinte comando para exibir o nome do dispositivo.</br><pre>fdisk -l</pre></td>
     </tr> 
</table>
17. Execute o seguinte comando para fazer backup do arquivo `/etc/fstab` para o diretório `/home`, por exemplo:
```
cp -r /etc/fstab /home
```
18. Execute o seguinte comando para usar o editor VI para abrir o arquivo `/etc/fstab`.
 ```
vi /etc/fstab
 ```
19. Pressione **i** para entrar no modo de edição. 
20. Mova o cursor para o final do arquivo, pressione **Enter** e adicione o seguinte conteúdo.
 ```
<Device information> <Mount point> <File system format> <File system installation option> <File system dump frequency> <File system check sequence at launch>
 ```
 - **(Recomendado)** Considere a montagem automática usando o soft link de um disco em nuvem elástico como exemplo. Adicione o seguinte ao exemplo anterior:
 ```
/dev/disk/by-id/virtio-disk-bm42ztpm-part1 /data/newpart2   ext4 defaults     0   2
 ```
 - Considere a montagem automática usando o UUID da partição do disco como exemplo. Adicione o seguinte ao exemplo anterior:
```
UUID=fc3f42cc-2093-49c7-b4fd-c616ba6165f4 /data/newpart2   ext4 defaults     0   2
```
 - Considere a montagem automática usando o nome do dispositivo como exemplo. Adicione o seguinte ao exemplo anterior:
```
/dev/vdc1 /data/newpart2   ext4 defaults     0   2
```
20. Pressione **Esc**, digite **:wq** e pressione **Enter**.
 Salve a configuração e feche o editor.
21. Execute o seguinte comando para verificar se o arquivo `/etc/fstab` foi gravado com êxito.
```
 mount -a 
```
Se o comando for executado com êxito, o arquivo foi gravado. O sistema de arquivos recém-criado será montado automaticamente quando o sistema operacional for iniciado.
:::
</dx-tabs>

## Operações relacionadas
 [Inicialização de discos em nuvem (menores que 2 TB)](https://intl.cloud.tencent.com/document/product/362/31597).


