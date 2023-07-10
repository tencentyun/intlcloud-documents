## Visão geral
Este documento descreve como inicializar um disco em nuvem recém-montado em um CVM, criar um sistema de arquivos e gravar um arquivo chamado `qcloud.txt`.

<dx-alert infotype="explain" title="">
Para obter mais informações sobre a inicialização de discos em nuvem, consulte [Cenários de inicialização](https://intl.cloud.tencent.com/document/product/362/31596).
</dx-alert>

## Observações
Para proteger dados importantes, consulte [Perguntas frequentes sobre uso](https://intl.cloud.tencent.com/document/product/362/32409) antes de realizar qualquer operação nos seus discos em nuvem do CBS.

## Pré-requisitos
- Já ter montado o disco em nuvem `cbs-test` em um CVM. Para acessar orientações detalhadas, consulte [Etapa 2. Montagem de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/39991).

## Orientações
<dx-tabs>
::: Formatar,\scriar\sum\ssistema\sde\sarquivos\se\sgravar\sum\sarquivo\s(Windows)
<dx-alert infotype="explain" title="">
Este documento usa um CVM com Windows Server 2012 R2 DataCenter 64-bit chinês instalado como exemplo. As etapas podem ser diferentes dependendo da versão do sistema operacional. 
</dx-alert>
1. Faça login no CVM como administrador. Consulte [Login em uma instância do Windows usando RDP](https://intl.cloud.tencent.com/document/product/213/5435). 
2. Na área de trabalho, clique com o botão direito <img src="https://main.qcloudimg.com/raw/3d815ac1c196b47b2eea7c3a516c3d88.png" style="margin:-6px 0px"> no canto inferior esquerdo.
3. Selecione **Disk Management (Gerenciamento de disco)** no menu pop-up para abrir a janela **Disk Management**.
4. (Opcional) Clique com o botão direito no disco vazio necessário e selecione **Online**.
Quando o status do disco mudar para **Not Initialized (Não inicializado)**, significa que ele está online.
5. (Opcional) Clique com o botão direito no disco em nuvem que acabou de ficar online. Selecione **Initialize Disk (Inicializar disco)** e depois **Master Boot Record (Registro mestre de inicialização)** na janela pop-up **Initialize Disk** e clique em **OK**.
<dx-alert infotype="explain" title="">
- O formato de partição Master Boot Record (MBR) permite uma capacidade máxima de disco de 2 TB, e a GUID Partition Table (GPT) permite uma capacidade máxima de disco de 18 EB. Se você precisar de uma capacidade de disco maior do que 2 TB, selecione o formato de partição GPT.
- Se o formato de partição do disco for alterado após o disco ser colocado em funcionamento, os dados originais do disco serão excluídos. Selecione o formato de partição com cuidado quando inicializar o disco.
</dx-alert>
6. Clique com o botão direito no disco necessário, selecione **New Simple Volume (Novo volume simples)**e clique em **Next (Avançar)** na janela pop-up.
7. Insira o tamanho do volume simples e clique em **Next (Avançar)**.
8. Selecione uma letra ou caminho da unidade de disco e clique em **Next (Avançar)**. Neste exemplo, E é atribuído como a letra da unidade de disco.

9. Selecione o sistema de arquivos, faça uma formatação rápida e depois clique em **Next (Avançar)**.

10. Clique em **Finish (Concluir)**.
 O status do disco mudará para **Formatting (Formatando)**. Aguarde a conclusão da inicialização. Quando o status do volume mudar para **Healthy (Íntegro)**, significa que a inicialização do disco funcionou. Você pode visualizar o disco de dados recém-formatado na interface **PC**.
11. Insira o disco de dados recém-formatado, crie um arquivo chamado `qcloud.txt`, insira o conteúdo necessário e selecione **File (Arquivo)** > **Save (Salvar)**.
:::

::: Formatar,criar\sum\ssistema\sde\sarquivos\se\sgravar\sum\sarquivo\s(Linux)
<dx-alert infotype="notice" title="">
- Este documento usa um CVM com CentOS 7.8 instalado como exemplo. As etapas podem ser diferentes dependendo da versão do sistema operacional. 
- O sistema de arquivos EXT4 é usado neste exemplo.
- Quando o CVM Linux for reiniciado ou ligado, os discos de dados não serão automaticamente montados. Você pode consultar a [Etapa 9](#Step09) à [Etapa 14](#Step14) para configurar a montagem automática do disco no momento da inicialização.
</dx-alert>
1. [Faça login em uma instância CVM Linux](https://intl.cloud.tencent.com/document/product/213/5436) como o usuário-raiz.
2. Execute o comando a seguir para visualizar os nomes dos discos de dados anexados à instância.

```
fdisk -l
```
Se o resultado retornado for igual ao mostrado na figura a seguir, significa que o CVM atual tem dois discos, em que `/dev/vda` é o disco do sistema e `/dev/vdb` é o disco de dados recém-adicionado.
Neste exemplo, o disco anexado à instância é chamado `/dev/vdb`:
![](https://main.qcloudimg.com/raw/969d3ca3d95b16d47103886e11714868.png)

3. Execute o comando a seguir para formatar o disco.
```
mkfs.ext4 /dev/vdb
```
4. Execute o comando a seguir para montar este disco no ponto de montagem `/data`.
```
mount /dev/vdb /data
```
5. Execute os comandos a seguir para inserir o disco e criar um novo arquivo `qcloud.txt`.
```
cd /data
​``` 
```
vi qcloud.txt
```
6. Pressione **i** para entrar no modo de edição e digite **This is my first test**.
7. Pressione **Esc** para sair do modo de edição, digite **:wq** e pressione **Enter** para salvar e sair do arquivo.
8. Execute o comando `ls` e você verá que o arquivo `qcloud.txt` foi gravado no disco.
<dx-alert infotype="explain" title="">
Consulte a [Etapa 9](#Step09) à [Etapa 14](#Step14) para configurar a montagem automática do disco no momento da inicialização. Se você não precisar da montagem automática do disco na inicialização, pule as etapas a seguir.
</dx-alert>
9. [](id:Step09)Execute o seguinte comando para fazer backup do arquivo `/etc/fstab` no diretório `/home`, por exemplo:
```
cp -r /etc/fstab /home
```
10. Execute o seguinte comando para usar o editor VI para abrir o arquivo `/etc/fstab`.
```
vi /etc/fstab
```
11. Pressione **i** para entrar no modo de edição.
12. Mova o cursor até o final do arquivo, pressione **Enter** e adicione o conteúdo a seguir.
​```plaintext
<Device information> <Mount point> <File system format> <File system installation option> <File system dump frequency> 
<File system check sequence at startup>
```
Configure a montagem automática usando um link simbólico de um disco em nuvem elástico como exemplo. Adicione o conteúdo a seguir:
```
/dev/disk/by-id/virtio-disk-drkhklpe /data ext4 defaults 0 0
```
13. Pressione **Esc**, digite **:wq** e pressione **Enter**.
Salve a configuração e saia do editor.

14. [](id:Step14)Execute o comando a seguir para verificar se o arquivo `/etc/fstab` foi gravado com êxito.
```
mount -a 
``` 
Se o comando for executado com êxito, significa que o arquivo foi gravado. O sistema de arquivos recém-criado será montado automaticamente quando o sistema operacional for inicializado.
:::

</dx-tabs>

## Operações subsequentes
Um disco em nuvem é um dispositivo de armazenamento expansível em nuvem. Você pode expandir sua capacidade de acordo com seus negócios a qualquer momento sem perder nenhum dado salvo nele. Para acessar orientações detalhadas, consulte [Etapa 4. Expansão de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/31646).

