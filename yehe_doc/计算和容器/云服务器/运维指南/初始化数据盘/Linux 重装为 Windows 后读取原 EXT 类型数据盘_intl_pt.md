
## Cenário
O Windows emprega dois sistemas de arquivos principais, NTFS ou FAT32, já o EXT é o sistema de arquivos de fator do Linux. Quando um sistema operacional é alterado de Linux para Windows após a reinstalação, o disco de dados permanece em seu formato original. Portanto, o sistema pode não conseguir acessar o sistema de arquivos do disco de dados. Nesses casos, será necessário usar um conversor de formato para ler o disco de dados. 

Este documento descreve como ler um disco de dados quando o sistema operacional foi [reinstalado](https://intl.cloud.tencent.com/document/product/213/4933) do Linux para o Windows.


## Pré-requisitos
- O DiskInternals Linux Reader foi instalado no CVM do Windows reinstalado.
Baixe o DiskInternals Linux Reader: `http://www.diskinternals.com/download/Linux_Reader.exe `
- Suponha que o disco de dados montado no CVM do Linux antes da reinstalação tenha duas partições, vdb1 e vdb2, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/ef515a31c27e5ea96993af60dfc9ab55.png)

## Instruções
### Montagem de um disco de dados

> Se um disco de dados foi montado, ignore esta etapa.
>
1. Faça login no [Console do CVM do Tencent Cloud](https://console.cloud.tencent.com/cvm/).
2. Clique em **Cloud Block Storage** na barra lateral esquerda para acessar a página de gerenciamento dele.
3. Localize a instância com o sistema reinstalado e clique em **More (Mais)** > **Mount (Montar)** à direita, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/a3100055adb58330591e277c4e7f72eb.png)
4. Na janela pop-up, selecione o CVM do Windows reinstalado e clique em **Submit (Enviar)**.

### Exibição das informações do disco de dados 
1. Execute o DiskInternals Linux Reader para exibir as informações do disco de dados recém-montado. `/root/mnt` e `/root/mnt1` correspondem a vdb1 e vdb2 respectivamente, que são as duas partições de disco de dados no CVM do Linux antes da reinstalação, conforme mostrado abaixo:
> Observe que o disco de dados do Linux é somente leitura neste momento. Para realizar operações de leitura e gravação no disco de dados como você faz em um do Windows, faça backup dos arquivos necessários e reformate o disco em um sistema de arquivos padrão com compatibilidade com o Windows. Para obter mais informações, consulte [Partição de disco de dados e formatação de CVMs do Windows](https://intl.cloud.tencent.com/document/product/213/2158).
>
![](https://main.qcloudimg.com/raw/490428b0668dcd61c4c60bcb75121462.png)
2. Clique duas vezes para acessar o diretório `/root/mnt`, clique com o botão direito do mouse no arquivo que deseja copiar e selecione **Save (Salvar)** como mostrado abaixo:
![](https://main.qcloudimg.com/raw/f36cbf32a7b423b8800e1fda6ba1c038.png)




