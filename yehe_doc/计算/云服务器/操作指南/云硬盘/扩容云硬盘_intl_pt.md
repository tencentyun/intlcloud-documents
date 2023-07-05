## Visão geral
Um disco em nuvem é um dispositivo de armazenamento expansível na nuvem. Depois que um disco em nuvem é criado, é possível expandir sua capacidade a qualquer momento para aumentar sua capacidade de armazenamento sem perder nenhum dado nele.
Depois que um disco em nuvem é expandido, é necessário atribuir sua capacidade expandida a uma partição existente ou formatá-lo em uma nova partição independente. Para obter mais informações, consulte [Extensão de partições e sistemas de arquivos (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) ou [Extensão de partições e sistemas de arquivos (Linux)](https://intl.cloud.tencent.com/document/product/362/31602).
>! A partição MBR é compatível com disco com capacidade máxima de 2 TB. Ao particionar o disco com capacidade superior a 2 TB, recomendamos que você crie e monte um novo disco de dados e use o formato de partição GPT para copiar os dados.

## Expansão de discos de dados
Se o disco em nuvem for um disco de dados, é possível expandi-lo usando os três métodos a seguir.
>!Se vários discos em nuvem da mesma capacidade e tipo forem montados no CVM, é possível distingui-los de acordo com o método mostrado em [Distinção de discos de dados](#distinguish). Selecione um disco de dados e expanda sua capacidade das seguintes formas.


#### Expansão de discos de dados pelo console do CVM (recomendado)
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Localize o CVM no qual deseja expandir o disco de dados e selecione **More (Mais)** > **Resource Adjustment (Ajuste de recursos)** > **Expand Data Disk (Expandir disco de dados)** na coluna **Operation (Operação)**.
3. Selecione o disco de dados a ser expandido na janela pop-up e clique em **Next (Avançar)**.
4. Selecione uma nova capacidade (deve ser maior ou igual à capacidade atual) e clique em **Next (Avançar)**.
5. Leia as observações e clique em **Adjust Now (Ajustar agora)**.
6. Atribua sua capacidade expandida a uma partição existente ou formate-a em uma nova partição independente. Dependendo do sistema operacional do CVM, consulte [Extensão de partições e sistemas de arquivos (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) ou [Extensão de partições e sistemas de arquivos (Linux)](https://intl.cloud.tencent.com/document/product/362/31602).

#### Expansão de discos de dados pelo console do CBS
1. Faça login no [Console do CBS](https://console.cloud.tencent.com/cvm/cbs).
2. Localize o disco em nuvem a ser expandido e selecione **More (Mais)** > **Expand (Expandir)** na coluna **Operation (Operação)**.
3. Selecione uma nova capacidade. Deve ser maior ou igual à capacidade atual.
4. Conclua o pagamento.
5. Atribua sua capacidade expandida a uma partição existente ou formate-a em uma nova partição independente. Dependendo do sistema operacional do CVM, consulte [Extensão de partições e sistemas de arquivos (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) ou [Extensão de partições e sistemas de arquivos (Linux)](https://intl.cloud.tencent.com/document/product/362/31602).

#### Expansão de discos de dados por API
É possível usar a API `ResizeDisk` para expandir os discos em nuvem especificados. Para obter mais informações, consulte [ResizeDisk](https://intl.cloud.tencent.com/document/product/362/16310).




## Expansão de discos do sistema
Se o disco em nuvem funcionar como um disco do sistema, é possível expandi-lo usando os dois métodos a seguir.

#### Expansão de discos do sistema pelo console do CVM (recomendado)
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index). Localize o CVM no qual deseja expandir o disco do sistema e selecione **More (Mais)** > **Resource Adjustment (Ajuste de recursos)** > **Expand System Disk (Expandir disco do sistema)** na coluna **Operation (Operação)**.
2. Selecione o disco do sistema a ser expandido na janela pop-up e clique em **Next (Avançar)**.
3. Selecione uma nova capacidade (deve ser maior ou igual à capacidade atual) e clique em **Next (Avançar)**.
4. Leia as observações, selecione **Agree to a forced shutdown (Concordar com um desligamento forçado)** e clique em **Adjust Now (Ajustar agora)**.
5. Após a expansão ser concluída no console, verifique a configuração do cloudinit para as [instâncias do Linux](#confirmLinuxConfig) ou as [instâncias do Windows](#confirmwindowsConfig) de acordo com o sistema operacional do CVM. Depois, estenda as partições e os sistemas de arquivos conforme necessário.

#### Expansão de discos do sistema reinstalando o sistema
Também é possível expandir o disco do sistema [reinstalando o sistema](https://intl.cloud.tencent.com/document/product/213/4933)



## Operações
[](id:distinguish)
### Distinção de discos de dados
Verifique os discos em nuvem de acordo com o sistema operacional do CVM.

#### Linux
1. [Faça login em uma instância do Linux](https://intl.cloud.tencent.com/document/product/213/5436)
2. Execute o seguinte comando para visualizar a relação entre os discos em nuvem elásticos e o nome do dispositivo.

```
ls -l /dev/disk/by-id
```
As seguintes informações são exibidas:
![](https://main.qcloudimg.com/raw/66b6a19695ef4ba21b74ce0cd96503db.png)
`disk-xxxx` é o ID de um disco em nuvem. É possível usá-lo para visualizar os detalhes do disco em nuvem no [console do CBS](https://console.cloud.tencent.com/cvm/cbs).

#### Windows
1. [Faça login em uma instância do Windows](https://intl.cloud.tencent.com/document/product/213/5435).
2. Clique com o botão direito do mouse em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-6px 0px"> e selecione **Run (Executar)**.
3. Insira `cmd` na janela pop-up e pressione **Enter**.
4. Execute o seguinte comando para visualizar a relação entre os discos em nuvem elásticos e o nome do dispositivo.

```
wmic diskdrive get caption,deviceid,serialnumber
```
Também é possível executar o seguinte comando
```
wmic path win32_physicalmedia get SerialNumber,Tag
```
As seguintes informações são exibidas:
![](https://main.qcloudimg.com/raw/e91aa2f938ddda304844d7ac28840859.png)
`disk-xxxx` é o ID de um disco em nuvem. É possível usá-lo para visualizar os detalhes do disco em nuvem no [console do CBS](https://console.cloud.tencent.com/cvm/cbs).


### Verificação da configuração do cloudinit
Verifique a configuração do cloudinit de acordo com o sistema operacional do CVM.

[](id:confirmLinuxConfig)
#### Verificação da configuração do cloudinit para instâncias do Linux
Depois que o disco do sistema for expandido, [faça login na instância do Linux](https://intl.cloud.tencent.com/document/product/213/5436) e verifique se o arquivo `/etc/cloud/cloud.cfg` contém os itens de configuração `growpart` e `resizefs`.
 - Se sim, ignore as outras operações.
![](https://main.qcloudimg.com/raw/03d38f34651d317176c50f1ed3a03f30.png)
    - **growpart**: expande a partição para o tamanho do disco.
    - **resizefs**: expande ou ajusta o sistema de arquivos da partição `/` ao tamanho da partição.
 - Se não, [estenda manualmente as partições e os sistemas de arquivos (Linux)](https://intl.cloud.tencent.com/document/product/362/31602) de acordo com o sistema operacional, e atribua sua capacidade expandida a uma partição existente ou formate-a em uma nova partição independente.

[](id:confirmwindowsConfig)

#### Verificação da configuração do cloudinit para instâncias do Windows
Depois que o disco do sistema for expandido, [faça login na instância do Windows](https://intl.cloud.tencent.com/document/product/213/5435) e verifique se o item de configuração `ExtendVolumesPlugin` existe em `plugin` em `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf\cloudbase-init.conf`.
 - Se sim, ignore as outras operações.
 Se não, [estenda manualmente as partições e os sistemas de arquivos (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) de acordo com o sistema operacional, e atribua sua capacidade expandida a uma partição existente ou formate-a em uma nova partição independente.

