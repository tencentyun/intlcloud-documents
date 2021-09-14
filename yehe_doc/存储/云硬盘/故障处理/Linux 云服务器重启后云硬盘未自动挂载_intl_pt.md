## Descrição do erro
O sistema de arquivos foi criado e configurado para montar automaticamente o disco em nuvem em um CVM do Linux, mas ocorre uma falha na montagem automática ao reiniciar o CVM.

## Motivos possíveis
- **Motivo 1**: a montagem automática do disco em nuvem não está configurada no arquivo de configuração `fstab` do CVM.
- **Motivo 2**: configuração incorreta do arquivo de configuração `fstab`.
Por exemplo, se o nome do dispositivo for usado para a montagem automática e ele for alterado ao reiniciar o CVM, ocorrerá falha na inicialização.

#### Soluções
- **Solução do motivo 1**:
Consulte o método a seguir para reconfigurar o arquivo `/etc/fstab` para que os discos em nuvem sejam montados automaticamente após a reinicialização de um CVM:
	- Usando um soft link do disco (recomendado)
	- Usando um identificador exclusivo universal (UUID) do sistema de arquivos
	- Usando o nome do dispositivo (não recomendado)
	Para ver instruções detalhadas, consulte [Configuração do arquivo `/etc/fstab`](#ConfigurationFile).
- **Solução do motivo 2**:
Faça login no CVM do Linux usando VNC e acesse o modo de usuário único. Nesse modo, corrija e reconfigure o arquivo de configuração `/etc/fstab`. Para ver instruções detalhadas, consulte [Correção do arquivo `/etc/fstab`](#RepairConfiguration).


## Procedimento de solução de problemas


### Configuração do arquivo `/etc/fstab`[](id:ConfigurationFile)
1. [Faça login em uma instância do Linux usando o método de login padrão](https://intl.cloud.tencent.com/document/product/213/5436).
2. Escolha um método de configuração para obter informações.[](id:Step2)

<dx-tabs>
::: Usando o soft link dos discos em nuvem elásticos (recomendado)
#### Análise do método de configuração
- **Vantagens**: o soft link de um disco em nuvem elástico é fixo e único. Ele não muda com as operações, como montagem, desmontagem e formatação de partições.
- **Desvantagens**: apenas um disco em nuvem elástico pode usar o soft link, o qual age de forma imperceptível na operação de formatação da partição.

#### Obtenção de informações
Execute o comando a seguir para ver o soft link do disco em nuvem elástico.
```
plaintext
ls -l /dev/disk/by-id
```
As seguintes informações serão exibidas:
![](https://main.qcloudimg.com/raw/99c7d8362b4313a0366adace46563bb7.png)
:::
::: Usando o UUID do sistema de arquivos

#### Análise do método de configuração
Poderá ocorrer falha na configuração de montagem automática devido a alterações no UUID de um sistema de arquivos.
Por exemplo, reformatar um sistema de arquivos alterará seu UUID.

#### Obtenção de informações
Execute o comando a seguir para exibir o UUID do sistema de arquivos.
```
blkid /dev/vdb1
```
As seguintes informações serão exibidas:
![](https://main.qcloudimg.com/raw/a1f6204b8f95f71609571612ff45aa42.png)
:::
::: Usando o nome do dispositivo (não recomendado)

#### Análise do método de configuração
Poderá ocorrer falha na configuração de montagem automática devido a alterações no nome do dispositivo.
Por exemplo, se um disco em nuvem elástico do CVM for desmontado e depois remontado, o nome do dispositivo poderá ser alterado quando o sistema operacional reconhecer o sistema de arquivos novamente.

#### Obtenção de informações
Execute o seguinte comando para exibir o nome do dispositivo.
```
fdisk -l
```
As seguintes informações serão exibidas:
![](https://main.qcloudimg.com/raw/1d09eba0c658fed0e9f5303e273b5539.png)
:::
</dx-tabs>
3. Execute o seguinte comando para fazer backup do arquivo `/etc/fstab` para o diretório `/home`, por exemplo:
```
cp /etc/fstab /home
```
4. Execute o comando a seguir no editor VI para abrir o arquivo `/etc/fstab`.
```
vi /etc/fstab
```
5. Pressione **i** para acessar o modo de edição e insira o conteúdo a seguir na linha posterior à última linha do arquivo.
```
<Device information> <Mount point> <File system format> <File system installation option> <File system dump frequency> <File system check sequence at launch>
```
Consulte os exemplos a seguir de acordo com o método de configuração selecionado na [Etapa 2](#Step2).
 - (Recomendado) Use o soft link de um disco em nuvem elástico como exemplo. Adicione o conteúdo a seguir:
```
/dev/disk/by-id/virtio-disk-drkhklpe-part1 /data/newpart   ext4 defaults     0   2
```
 - Use o UUID do sistema de arquivos como exemplo. Adicione o conteúdo a seguir:
```
UUID=d489ca1c-5057-4536-81cb-ceb2847f9954 /data/newpart   ext4 defaults     0   2
```
 - (Não recomendado) Use o nome do dispositivo como exemplo. Adicione o conteúdo a seguir:
```
/dev/vdb1 /data/newpart   ext4 defaults     0   2
```
6. Pressione **ESC**, insira **:wq** e pressione **Enter** para salvar a configuração e sair do editor.
7. Execute o comando a seguir para verificar se o arquivo `/etc/fstab` foi gravado com êxito.
```
mount -a 
```
Se as informações semelhantes às mostradas abaixo forem retornadas, significa que o arquivo foi gravado. O sistema de arquivos será montado automaticamente quando o sistema operacional for iniciado. Você pode reiniciar o CVM para verificar o resultado.
![](https://main.qcloudimg.com/raw/4289f335d3373074d7fc799863fba498.png)

[](id:RepairConfiguration)
### Correção do arquivo `/etc/fstab` 
1. [Faça login em uma instância do Linux usando VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Acesse o modo de usuário único. Para ver instruções detalhadas, consulte [Configuração do CVM do Linux para inicializar o modo de usuário único](https://intl.cloud.tencent.com/document/product/213/34819).
3. Execute o seguinte comando para fazer backup do arquivo `/etc/fstab` para o diretório `/home`, por exemplo:
```
cp /etc/fstab /home
```
4. Execute o comando a seguir no editor VI para abrir o arquivo `/etc/fstab`.
```
vi /etc/fstab
```
5. Pressione **i** para entrar no modo de edição. Mova o cursor para o início da linha de erro e insira `#` para remover essa configuração, conforme mostrado abaixo.
>?Esta linha configura a montagem automática do disco de dados. Entretanto, devido a um erro de configuração, o disco em nuvem talvez não seja montado quando o CVM for reiniciado.
>
 ![](https://main.qcloudimg.com/raw/2e6106588877801aa38fbe4af3dc52a6.png)
6. Pressione **ESC**, insira **:wq** e pressione **Enter** para salvar a configuração e sair do editor.
7. Digite `exit` para sair do modo de usuário único.
8. Aguarde até a conclusão da reinicialização. Faça login no CVM.
9. Reconfigure o arquivo conforme indicado em [Configuração do arquivo `/etc/fstab`](#ConfigurationFile).
