## Visão geral
Este documento descreve como liberar espaço de disco em um Tencent Cloud CVM baseado no Windows Server 2012 R2 quando o espaço em disco é insuficiente. Também descreve como realizar a manutenção de rotina em disco.

## Instruções

### Liberar espaço em disco
É possível excluir [arquivos grandes](#deleteLargerFiles) ou [arquivos obsoletos](#deleteObsoleteFiles) para liberar espaço em disco. Se o espaço em disco ainda for insuficiente após a exclusão de arquivos grandes e obsoletos, você pode expandir o espaço em disco. Para fazer isso, consulte [Cenários de expansão de disco em nuvem](https://intl.cloud.tencent.com/document/product/362/31600).
<span id="deleteLargerFiles"></span>
#### Excluir arquivos grandes
1. Faça login em uma instância do Windows usando [o arquivo RDP (recomendado)](https://intl.cloud.tencent.com/document/product/213/5435) ou [a área de trabalho remota](https://intl.cloud.tencent.com/document/product/213/32498).
2. Clique em <img src="https://main.qcloudimg.com/raw/dcdf8e1ebc35bd6db1edaceff6784db2.png" style="margin:-5px 0px"> na barra de ferramentas inferior e abra a janela "This PC (Este PC)".
3. Selecione o disco no qual deseja liberar espaço e pressione **Crtl + F** para abrir a ferramenta de pesquisa.
4. Selecione **Search (Pesquisar)** -> **Size (Tamanho)** e filtre os arquivos pelas opções de tamanho definidas pelo sistema, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/48a1033c6b978dfe6de1b2dc6d8bcdd3.png)
>?Você também pode inserir um tamanho na caixa de pesquisa no canto superior direito da janela **This PC (Este PC)**. Por exemplo:
> - Digite "Size: > 500 MB" para pesquisar no disco arquivos com mais de 500 MB.
> - Digite "Size: > 100 MB < 500 MB" para pesquisar o disco em busca de arquivos maiores que 100 MB, mas menores que 500 MB.
>

<span id="deleteObsoleteFiles"></span>
#### Excluindo arquivos obsoletos
1. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin:-5px 0px"> para abrir o **Server Manager (Gerenciador do servidor)**.
2. Clique em **Add Roles and Features (Adicionar funções e recursos)** em **Manage (Gerenciar)**.
3. Na janela pop-up, clique em **Next (Avançar)**.
4. Selecione **Role-based or feature-based installation (Instalação baseada em função ou recurso)** e clique em **Next (Avançar)** duas vezes, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/d25dc913281f8cb5c688dd9cc62b8d73.png)
5. Na página **Select features (Selecionar recursos)**, marque **Ink and Handwriting Services (Serviços de tinta e manuscrito)** e **Desktop Experience (Experiência de área de trabalho)**, conforme mostrado abaixo. Clique em **OK** na caixa de diálogo pop-up.
![](https://main.qcloudimg.com/raw/f1bf18c4598597ef86428bd4bbd77c15.png)
6. Clique em **Next (Avançar)** e em **Install (Instalar)**. Aguarde a conclusão da instalação e reinicie o CVM quando solicitado.
7. Selecione <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-5px 0px"> e clique em <img src="https://main.qcloudimg.com/raw/4851c97390178d2d8ae2e6385756eb3b.png" style="margin:-5px 0px"> no canto superior direito. Digite **Disk Management (Gerenciamento de disco)** e pesquise.
8. Na janela pop-up **Disk Cleanup (Limpeza de disco)**, selecione o disco de destino e inicie a limpeza, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/69e2c653c6304a450463cdf07bf5a3ef.png)

### Manutenção de rotina do disco
#### Remover programas regularmente
Selecione **Control Panel (Painel de controle)** -> **Programs and Features (Programas e recursos)** -> **Uninstall or change a program (Desinstalar ou alterar um programa)** para remover programas obsoletos regularmente, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/b9294f1e79429dbdb8a7800cfdb6d6b4.png)


#### Visualizar o uso do disco no console
O recurso Cloud Monitor é ativado automaticamente assim que uma instância CVM é criada. É possível visualizar o uso do disco seguindo as etapas abaixo:
1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm/instance/index) e acesse a página **Instances (Instâncias)**.
2. Selecione o ID/Nome da instância de destino para acessar a página de detalhes.
3. Selecione a guia **Monitoring (Monitoramento)** para visualizar o uso do disco da instância, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/19f00a883ed73ba1c636830f06d3f00d.png)
