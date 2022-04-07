## Descrição do erro
O CVM do Linux encontra problemas de memória, como velocidade de resposta de serviço lenta, falha de login do CVM ou falta de memória (OOM, na sigla em inglês).

## Possíveis causas
Esses problemas podem ser causados pela alta utilização de memória da instância, ou seja, a utilização de memória geralmente fica acima de 90%.


## Abordagens de solução de problemas
1. Realize o [procedimento de solução de problemas](#ProcessingSteps) para verificar se a utilização da memória está muito alta.
2. Consulte a [análise de problemas de memória](#OtherProcessingSteps) para encontrar as causas dos problemas.

## Procedimento de solução de problemas[](id:ProcessingSteps)
1. Siga as [instruções](#RelatedOperations) para verificar se a utilização da memória está muito alta.
 - Se estiver, prossiga para a próxima etapa.
 - Se não estiver, consulte a [análise de problemas de memória](#OtherProcessingSteps) para encontrar as causas dos problemas.
2. Faça login no CVM, execute o comando `top` e pressione **M** para verificar se há processos nas colunas “RES” e “SHR” usando muita memória.
  - Se não houver, prossiga para a próxima etapa.
  - Se houver, realize as operações descritas em [análise de processo](https://intl.cloud.tencent.com/document/product/213/32387) de acordo com o tipo de processo.
3. Execute o comando a seguir para verificar a utilização da memória compartilhada.
```
cat /proc/meminfo | grep -i shmem
```
As seguintes informações serão exibidas:
![](https://main.qcloudimg.com/raw/269ca888f6f0232a63705b6f9fd578a8.png)
4. Execute o comando a seguir para verificar a utilização de memória slab não recuperável.
```
cat /proc/meminfo | grep -i SUnreclaim
```
As seguintes informações serão exibidas:
![](https://main.qcloudimg.com/raw/9e6c84eb5bfb0be315fc39d1b768d168.png)
5. Execute o comando a seguir para verificar se existem huge pages.
```
cat /proc/meminfo | grep -iE "HugePages_Total|Hugepagesize"
```
As seguintes informações serão exibidas:
![](https://main.qcloudimg.com/raw/aae7ce06f7034c123c26ef92265b82ea.png)
 - Se a saída de `HugePages_Total` for `0`, consulte a [análise de problemas de memória](#OtherProcessingSteps) para encontrar as causas dos problemas.
 - Se a saída de `HugePages_Total` não for zero `0`, existem huge pages (páginas enormes). O tamanho da huge page equivale a `HugePages_Total * Hugepagesize`. Verifique se as huge pages foram configuradas por um programa mal-intencionado, ou caso elas sejam desnecessárias, você pode converter o item de configuração `vm.nr_hugepage` no arquivo `/etc/sysctl.conf` em comentário, e então executar o comando `sysctl -p` para abandonar as huge pages.

## Instruções[](id:RelatedOperations)
### Exibição da utilização da memória
A saída do comando `free` pode variar com as distribuições do Linux, o que não é confiável para calcular a utilização de memória. Realize as etapas a seguir para exibir a utilização da memória na página **Monitoring (Monitoramento)** do console do CVM.
1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm/index) e acesse a página **Instances (Instâncias)**.
2. Clique no **ID/Name (ID/Nome)** da instância para acessar a página de detalhes. Selecione a guia **Monitoring (Monitoramento)**.
3. Exiba a utilização da memória na seção **Memory Monitor (Monitor de memória)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/4f9f423e6d9d460d1413ff0ead6c7e96.png)

### Cálculo da utilização da memória
O uso de memória é a razão da memória usada pela total, excluindo o buffer e o cache do sistema. A fórmula de cálculo é a seguinte:
= `(Total - available)100% / Total`
= `(Total - (Free + Buffers + Cached + SReclaimable - Shmem)) * 100% / Total`
= `(Total - Free - Buffers - Cached - SReclaimable + Shmem) * 100% / Total`

Os parâmetros obrigatórios `Total`, `Free`, `Buffer`, `Cached`, `SReclaimable`, e `Shmem` podem ser obtidos em `/proc/meminfo`. Veja abaixo um exemplo de `/proc/meminfo`.
```plaintext
1. [root@VM_0_113_centos test]# cat /proc/meminfo 
2. MemTotal: 16265592 kB
3. MemFree: 1880084 kB
4. ......
5. Buffers: 194384 kB
6. Cached: 13647556 kB
7. ......
8. Shmem: 7727752 kB
9. Slab: 328864 kB
10. SReclaimable: 306500 kB
11. SUnreclaim: 22364 kB
12. ......
13. HugePages_Total: 0
14. Hugepagesize: 2048 kB
```
Os parâmetros são descritos a seguir:
<table>
<tr>
<th>Parâmetro</th>
<th>Descrição</th>
</tr>
<tr>
<td><code>MemTotal</code></td>
<td>Memória total do sistema</td>
</tr>
<tr>
<td><code>MemFree</code></td>
<td>Memória livre</td>
</tr>
<tr>
<td><code>Buffers</code></td>
<td>Página em cache usada por dispositivos de bloco para leitura/gravação e metadados do sistema de arquivos (como SuperBlock)</td>
</tr>
<tr>
<td><code>Cached</code></td>
<td>Cache de página, incluindo <code>memória compartilhada POSIX/SysV</code> e <code>mmap anônimo compartilhado</code> de tmpfs
</td>
</tr>
<tr>
<td><code>Shmem</code></td>
<td>Incluindo memória compartilhada, tmpfs etc.
</td>
</tr>
<tr>
<td><code>Slab</code></td>
<td>Memória alocada pelo alocador de memória slab do kernel, que pode ser exibida usando o comando <code>slabtop</code>
</td>
</tr>
<tr>
<td><code>SReclaimable</code></td>
<td>Slabs recuperáveis</td>
</tr>
<tr>
<td><code>SUnreclaim</code></td>
<td>Slabs não recuperáveis</td>
</tr>
<tr>
<td><code>HugePages_Total</code></td>
<td>Quantidade total de huge pages</td>
</tr>
<tr>
<td><code>Hugepagesize</code></td>
<td>Tamanho de uma huge page</td>
</tr>
</table>

### Análise de problemas de memória[](id:OtherProcessingSteps)
Se o problema persistir, ou caso receba os erros abaixo durante o uso do CVM, consulte as soluções correspondentes:
- [Erro de log “fork: Cannot allocate memory” (fork: Não é possível alocar memória)](https://intl.cloud.tencent.com/document/product/213/40502)
- [Erro de login VNC “Cannot allocate memory” (Não é possível alocar memória)](https://intl.cloud.tencent.com/document/product/213/40503)
- [Ativando o Out of Memory (memória esgotada) quando há espaço disponível](https://intl.cloud.tencent.com/document/product/213/40504) 
