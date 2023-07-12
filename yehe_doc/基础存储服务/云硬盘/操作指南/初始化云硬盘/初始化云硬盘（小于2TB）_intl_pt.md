## Visão geral
Este documento usa os discos em nuvem com capacidade inferior a 2 TB como exemplo para fornecer orientação sobre a inicialização de discos. Para obter mais informações, consulte os [Cenários de inicialização](https://intl.cloud.tencent.com/document/product/362/31596).


## Pré-requisitos
Ter [montado um disco em nuvem](https://intl.cloud.tencent.com/document/product/362/32401) no seu CVM.

## Observações
- Para proteger dados importantes, consulte as [Perguntas frequentes de uso](https://intl.cloud.tencent.com/document/product/362/32409) antes de operar nos seus discos em nuvem.
- A formatação de um disco de dados apagará todos os dados. Certifique-se de que o disco não contenha dados ou de que foi feito backup dos dados importantes.
- Para evitar exceções, verifique antes de formatar se o CVM interrompeu os serviços externos.

## Instruções


<dx-tabs>
:::Inicialização\sde\sdiscos\sem\snuvem\s(Windows) [](id:Windows2008)
>Este artigo usa o sistema operacional Windows Server 2012 R2 como exemplo. A operação de formatação varia de acordo com o sistema operacional. As informações abaixo são apenas para referência.
>
1. [Faça login no Cloud Virtual Machine do Windows](https://intl.cloud.tencent.com/document/product/213/5435).
2. Na área de trabalho do CVM, clique com o botão direito no ícone na parte inferior direita <img src="https://main.qcloudimg.com/raw/3d815ac1c196b47b2eea7c3a516c3d88.png" style="margin:-6px 0px">.
3. Selecione **Disk Management (Gerenciamento do disco)** no menu pop-up para abrir a janela **Disk Management (Gerenciamento do disco)**.
>Se o disco recém-adicionado estiver com o status offline (conforme exibido na figura acima), realize a [Etapa 4](#online) antes da [Etapa 5](#initialize) para inicializar. Caso contrário, você pode realizar diretamente a [Etapa 5](#initialize).
4. <span id="online"></span>Os discos são listados no painel do lado direito. Clique com o botão direito na área do disco 1 e selecione **Online** para que ele fique online. O status do disco 1 muda de **Offline** para **Not Initialized (Não inicializado)**.

5. <span id="initialize"></span>Clique com o botão direito na área do disco 1 e selecione **Initialize Disk (Inicializar disco)** no menu.

6. Na caixa de diálogo **Initialize Disk (Inicializar disco)**, o disco que você precisa inicializar é exibido. Selecione **MBR** ou **GPT** e clique em **OK**.
Se o formato da partição do disco for alterado após o disco ser colocado em uso, os dados originais do disco serão apagados. Selecione um formato de partição apropriado com base nas suas necessidades reais.

7. Clique com o botão direito no espaço não alocado do disco e selecione **New Simple Volume (Novo volume simples)**.
8. Na caixa de diálogo pop-up **New Simple Volume Wizard (Assistente do novo volume simples)**, siga as instruções na interface e clique em **Next (Avançar)**.
9. Especifique o tamanho do volume conforme necessário, que é o valor máximo por padrão. Clique em **Next (Avançar)**.
10. Atribua uma letra de unidade e clique em **Next (Avançar)**.
11. Selecione **Format this volume with the following settings (Formatar este volume com as seguintes configurações)**, configure os parâmetros conforme necessário, formate a partição e clique em **Next (Avançar)** para concluir a criação da partição.
12. Clique em **Complete (Concluir)** para concluir o assistente. Aguarde até que o sistema conclua a operação de inicialização. Quando o status do volume se torna **Healthy (Em bom funcionamento)**, a inicialização do disco obteve êxito.
    Após concluir a inicialização com êxito, acesse a interface **Computer (Computador)** para exibir o novo disco.

:::
:::Inicialização\sde\sdiscos\sem\snuvem\s(Linux)  [](id:Linux)

Selecione o método de inicialização de acordo com seus casos de uso reais:
- Se todo o disco for apresentado como uma partição independente (não há disco lógico como vdb1 e vdb2), recomendamos fortemente que você não use a partição e [crie diretamente o sistema de arquivos em dispositivos vazios](#CreateFileSystemOnBareDevice).
- Se todo o disco precisar ser apresentado como várias partições lógicas (há vários discos lógicos), é necessário executar a operação de partição primeiro e, em seguida, [criar o sistema de arquivos em uma partição](#CreateFileSystemOnPartition).

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
mkdir <mount point>
```
Considere a criação de um novo ponto de montagem `/data` como exemplo:
```
mkdir /data
```
5. Execute o seguinte comando para montar a partição recém-criada no ponto de montagem recém-criado.
```
mount /dev/vdb <mount point>
```
Considere a criação de um novo ponto de montagem `/data` como exemplo:
```
mount /dev/vdb /data
```
6. Execute o seguinte comando para exibir o resultado da montagem.
```
df -TH
```
> Se não for preciso configurar a montagem automática de discos na inicialização, pule as etapas a seguir.
7.Confirme o método de montagem e obtenha as informações correspondentes.
Com base nas necessidades empresariais, é possível usar o soft link de um disco em nuvem elástico, o UUID do sistema de arquivos (identificador exclusivo universal) ou o nome do dispositivo para montar um disco automaticamente. As descrições e os métodos de aquisição de informações são os seguintes:
<table>
 <tr>
      <th>Método de montagem</th>
      <th>Vantagens e desvantagens</th>
      <th>Método de aquisição de informações</th>
 </tr>
 <tr>
     <td nowrap="nowrap">Use o soft link do disco em nuvem elástico<b>(Recomendado)</b></td>
     <td><b>Vantagens:</b>o soft link de um disco em nuvem elástico é fixo e único. Ele não muda com operações como montagem, desmontagem e formatação de partições.</br><b>Desvantagens:</b>apenas um disco em nuvem elástico pode usar o soft link, que opera imperceptivelmente para a operação de formatação da partição.</td>
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
13. Execute o seguinte comando para verificar se o arquivo **/etc/fstab** foi gravado com êxito.
```
mount -a 
```
Se o comando for executado com êxito, o arquivo foi gravado. O sistema de arquivos recém-criado será montado automaticamente quando o sistema operacional for iniciado.

<span id="CreateFileSystemOnPartition"></span>
#### Criação de um sistema de arquivos em uma partição

>Este exemplo usa a ferramenta de partição fdisk no sistema operacional CentOS 7.5 para configurar o disco de dados `/dev/vdc` como a partição principal. MBR foi usado como formato de partição padrão, o formato EXT4 como o sistema de arquivos, `/data/newpart` como o ponto de montagem e a montagem automática na inicialização foi configurada. A operação de formatação varia de acordo com o sistema operacional. As informações abaixo são apenas para referência.


1. [Faça login no Cloud Virtual Machine do Linux](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute o seguinte comando como usuário raiz para exibir o nome do disco.
 ```
fdisk -l
 ```
 Se informações semelhantes às exibidas abaixo forem retornadas, o CVM atual tem dois discos, em que `/dev/vda` é o disco do sistema e `/dev/vdb` é o disco de dados recém-adicionado.
 ![](https://main.qcloudimg.com/raw/aad842b12fec3ca583790bff609c9fb7.png)
3. Execute o seguinte comando para abrir a ferramenta de partição fdisk e executar as operações de particionamento no disco de dados recém-adicionado.
 ```
fdisk <Newly added data disk>
 ```
 Considere o disco de dados recém-montado `/dev/vdb` como exemplo:
 ```
fdisk /dev/vdb
 ```
 As informações retornadas são semelhantes às exibidas abaixo:
 ![](https://main.qcloudimg.com/raw/db1fe212e2559ac635c52e5e397e7531.png)
4. Digite `n` e pressione **Enter** para começar a criar a nova partição.
 As informações retornadas são semelhantes às exibidas abaixo:
 ![](https://main.qcloudimg.com/raw/c89b572c0ac2af1302189f8e7e1a849e.png)
 Isso indica que o disco tem dois tipos de partições:
  - **p** indica a partição principal.
  - **e** indica a partição estendida.
5. Considere a criação de uma partição principal como exemplo. Digite `p` e pressione **Enter** para começar a criar uma nova partição principal.
 As informações retornadas são semelhantes às exibidas abaixo:
 ![](https://main.qcloudimg.com/raw/efb65b60631d95e9b0213e6fd6125bbb.png)
 O **Partition number (Número da partição)** indica o número da partição principal. Você pode escolher de 1 a 4.
6. Considere a seleção de número da partição 1 como exemplo. Digite o número da partição principal `1` e pressione **Enter**.
 As informações retornadas são semelhantes às exibidas abaixo:
 ![](https://main.qcloudimg.com/raw/e1a1a7755a3bb392ec6d623e6774c315.png)
 **First sector (Primeiro setor)** indica o setor inicial. Você pode escolher de 2048 a 20971519. O valor padrão é 2048.
7. Considere a seleção de número 2048 padrão para o setor inicial como exemplo. Pressione **Enter**.
 As informações retornadas são semelhantes às exibidas abaixo:
 ![](https://main.qcloudimg.com/raw/58a8202531b239a73fd3182d0ea0cf34.png)
 **Last sector (Último setor)** indica o setor final. Você pode escolher de 2048 a 20971519. O valor padrão é 20971519.
8. Considere a seleção de número 20971519 padrão para o setor final como exemplo. Pressione **Enter**.
 As informações retornadas são semelhantes às exibidas abaixo:
 ![](https://main.qcloudimg.com/raw/ad3a6459a6eaf154aed578b37dfc89d0.png)
 Isso indica que o particionamento foi concluído. Uma nova partição foi criada no disco de dados de 60 GB.
9. Digite `p` e pressione **Enter** para exibir as informações sobre a partição recém-criada.
 As informações retornadas são semelhantes às exibidas abaixo:
 ![](https://main.qcloudimg.com/raw/98427c11e0a181e02eb23a95fc1e908c.png)
 Isso indica as informações detalhadas da partição recém-criada `/dev/vdb1`.

>Se a operação de particionamento acima apresentar um erro, digite `q` para fechar a ferramenta de partição fdisk, e o resultado da partição anterior não será mantido.

10. Digite `w` e pressione **Enter** para gravar o resultado da partição na tabela de partição.
 Se as informações retornadas forem semelhantes às exibidas abaixo, a partição foi criada.
 ![](https://main.qcloudimg.com/raw/7011369be260150fcddf272b4a4ab2fa.png)
11. Execute o seguinte comando para sincronizar a tabela de partições com o sistema operacional.
 ```
partprobe
 ```
12. Execute o seguinte comando para configurar o sistema de arquivos da partição recém-criada para o que é exigido pelo sistema.
 ```
mkfs -t <File system format> /dev/vdb1
 ```
 O tamanho da partição suportado por diferentes sistemas de arquivos varia. Selecione um sistema de arquivos apropriado conforme necessário. O exemplo a seguir usa o `EXT4` como sistema de arquivos:
 ```
mkfs -t ext4 /dev/vdb1
 ```
 As informações retornadas são semelhantes às exibidas abaixo:
 ![](https://main.qcloudimg.com/raw/6de097cea77634f8847816dd795292a7.png)
 A formatação demora um pouco. Preste atenção ao status de execução do sistema e não feche.
13. Execute o seguinte comando para criar um novo ponto de montagem.
 ```
mkdir <mount point>
 ```
 Considere a criação de um novo ponto de montagem `/data/newpart` como exemplo:
 ```
mkdir /data/newpart
 ```
14. Execute o seguinte comando para montar a partição recém-criada no ponto de montagem recém-criado.
 ```
mount /dev/vdb1 <Mount point>
 ```
 Considere a criação de um novo ponto de montagem `/data/newpart` como exemplo:
 ```
mount /dev/vdb1 /data/newpart
 ```
15. Execute o seguinte comando para exibir o resultado da montagem.
 ```
df -TH
 ```
 As informações retornadas são semelhantes às exibidas abaixo:
 ![](https://main.qcloudimg.com/raw/b7e5501fed8d7d648b48dc66685baf94.png)
 Isso indica que a partição recém-criada `/dev/vdb1` foi montada em `/data/newpart`.

>Se não for preciso configurar a montagem automática de discos na inicialização, pule as etapas a seguir.
>
16. Confirme o método de montagem e obtenha as informações correspondentes.
 Com base nas necessidades empresariais, é possível usar o soft link de um disco em nuvem elástico, o UUID do sistema de arquivos (identificador exclusivo universal) ou o nome do dispositivo para montar um disco automaticamente. As descrições e os métodos de aquisição de informações são os seguintes:
 <table>
     <tr>
         <th>Método de montagem</th>  
         <th>Vantagens e desvantagens</th>  
         <th>Método de aquisição de informações</th>  
     </tr>
	   <tr>      
         <td nowrap="nowrap">Use o soft link do disco em nuvem elástico<b>(Recomendado)</b></td>   
	       <td><b>Vantagens:</b>o soft link de um disco em nuvem elástico é fixo e único. Ele não muda com operações como montagem, desmontagem e formatação de partições.</br><b>Desvantagens:</b>apenas um disco em nuvem elástico pode usar o soft link, que opera imperceptivelmente para a operação de formatação da partição.</td>
	       <td nowrap="nowrap">Execute o seguinte comando para exibir o soft link do disco em nuvem elástico.</br><pre>ls -l /dev/disk/by-id</pre></td>
     </tr> 
	   <tr>      
         <td nowrap="nowrap">Use o UUID do sistema de arquivos</td>   
	       <td>A configuração de montagem automática pode falhar devido a mudanças no UUID de um sistema de arquivos.</br>Por exemplo, reformatar um sistema de arquivos mudará seu UUID.</td>
	       <td nowrap="nowrap">Execute o seguinte comando para exibir o UUID do sistema de arquivos.</br><pre>blkid /dev/vdb1</pre></td>
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
/dev/disk/by-id/virtio-disk-drkhklpe-part1 /data/newpart   ext4 defaults     0   2
 ```
 - Considere a montagem automática usando o UUID da partição do disco como exemplo. Adicione o seguinte ao exemplo anterior:
```
UUID=d489ca1c-5057-4536-81cb-ceb2847f9954 /data/newpart   ext4 defaults     0   2
```
 - Considere a montagem automática usando o nome do dispositivo como exemplo. Adicione o seguinte ao exemplo anterior:
```
/dev/vdb1 /data/newpart   ext4 defaults     0   2
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
[Inicialização de discos em nuvem (maiores ou iguais a 2 TB)](https://intl.cloud.tencent.com/document/product/362/31598).


