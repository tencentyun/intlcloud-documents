## Visão geral
Expandir um disco de dados pelo console apenas aumenta o espaço de armazenamento dele. É preciso estender a partição ou o sistema de arquivos do disco em nuvem para um tamanho maior. Este documento descreve como estender partições e sistemas de arquivos online.

## Pré-requisitos
- Antes de estender a partição ou o sistema de arquivos, crie um snapshot do disco em nuvem para fazer backup dos dados. Para obter mais informações, consulte a [Criação de snapshots](https://intl.cloud.tencent.com/document/product/362/5755).
Essa prática ajuda a reverter o snapshot para recuperar dados em caso de perda de dados devido a operações incorretas.
- O disco em nuvem foi expandido e montado em um CVM pelo console. Para obter mais informações, consulte [Expansão da capacidade de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/5747).
- O kernel do CVM do Linux deve ser a versão 3.6.0 ou posterior. É possível usar o comando `uname -a` para verificar a versão do kernel.
Se a versão do kernel for anterior a 3.6.0, consulte [Extensão de partições e sistemas de arquivos (Linux)](https://intl.cloud.tencent.com/document/product/362/39995).

## Ambiente operacional
<table>
<tr>
<th>Recurso</th><th>Descrição</th>
</tr>
<tr>
<td>Sistema operacional</td>
<td>CentOS 8.0 64 bits</td>
</tr>
<tr>
<td>Disco em nuvem (disco de dados)</td>
<td>
<ul style="margin-bottom:0px">
<li><code>/dev/vdb</code>: usa a partição MBR e o sistema de arquivos EXT4 e expande de 50 GB para 60 GB pelo console.</li>
<li><code>/dev/vdc</code>: usa a partição GPT e o sistema de arquivos XFS e expande de 50 GB para 60 GB pelo console.</li>
</ul>
</td>
</tr>
</table>

## Instruções
### Visualização de partições do disco em nuvem
1. [Faça login em uma instância do Linux usando o método de login padrão](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute o seguinte comando para consultar as partições do disco em nuvem.
```
fdisk -l
```
As seguintes informações serão exibidas:
![](https://main.qcloudimg.com/raw/19d4f0ab6be5e332022efe9247069f35.png)
Conforme mostrado na figura,
 - O disco de dados `/dev/vdb` de 60 GB contém uma partição MBR de 50 GB `/dev/vdb1`.
 - O disco de dados `/dev/vdc` de 60 GB contém uma partição GPT de 50 GB `/dev/vdc1`.
3. [](id:Step3)Execute o seguinte comando para determinar o tipo de sistema de arquivos das partições existentes.
```
df -TH
```
As seguintes informações serão exibidas:
![](https://main.qcloudimg.com/raw/384bd9556f09e973504ab93dbb6aa900.png)
Conforme mostrado na figura,
 - A partição `/dev/vdb1` está em um sistema de arquivos EXT4 que foi montado em `/mnt/disk1`.
 - A partição `/dev/vdc1` está em um sistema de arquivos EXT4 que foi montado em `/mnt/disk2`.

### Extensão de uma partição
1. Use o comando conforme necessário para instalar a ferramenta gdisk.
 - Para uma partição MBR, pule essa etapa.
 - Para uma partição GPT, execute o seguinte comando de acordo com o sistema operacional do CVM.

<dx-tabs>
::: CentOS
```
yum install gdisk -y
```
:::

::: Ubuntu\sor\sDebian
```
apt-get install gdisk -y
```
:::
</dx-tabs>
2. Execute o seguinte comando para instalar a ferramenta growpart de acordo com o sistema operacional do CVM.
<dx-tabs>
::: CentOS
```
yum install -y cloud-utils-growpart
```
:::
::: Ubuntu\sor\sDebian
```
apt-get install -y cloud-guest-utils
```
:::
</dx-tabs>

3. Execute o seguinte comando para estender as partições usando a growpart.
Considere a extensão da partição `/dev/vdb1` como exemplo. Observe que há um espaço entre `/dev/vdb` e `1` no comando. Substitua por seus valores reais.
```
growpart /dev/vdb 1
```
Se as informações semelhantes às mostradas abaixo forem retornadas, a partição foi estendida.
![](https://main.qcloudimg.com/raw/bc67dd4e8116510ea2cea5484529cdf1.png)

### Extensão de um sistema de arquivos
1. Use o comando específico do sistema de arquivos para redimensionar um sistema de arquivos com base no tipo obtido na [etapa 3](#Step3).
<dx-tabs>
::: Extending\san\sEXT\sfile\ssystem

Execute o seguinte comando para estender o sistema de arquivos EXT.

```
resize2fs /dev/vdb1 
```

As seguintes informações serão exibidas:
![](https://main.qcloudimg.com/raw/5bd3a9bba754bf21256e792860c6d799.png)
:::
::: Extending\san\sXFS\sfile\ssystem

Execute o seguinte comando para estender o sistema de arquivos XFS.

```
xfs_growfs <Mount point>
```

Considere a montagem do sistema de arquivos `/dev/vdc1` em `/mnt/disk2` como exemplo e execute o seguinte comando:

```
xfs_growfs /mnt/disk2
```

As seguintes informações serão exibidas:
![](https://main.qcloudimg.com/raw/6e76842b419bb054c9cae9f96fa0250b.png)
:::
</dx-tabs>
2. Execute o seguinte comando para exibir o resultado.
```
df -TH
```
Se as informações semelhantes às mostradas abaixo forem retornadas, o sistema de arquivos foi estendido.
![](https://main.qcloudimg.com/raw/45bc319770858880a6b3cf35505bce46.png)

3. Verifique a integridade dos dados e o status de execução do CVM após a expansão.
É possível reverter o snapshot para recuperar os dados em caso de exceções. Para obter mais informações, consulte [Reversão de snapshots](https://intl.cloud.tencent.com/document/product/362/5756).

