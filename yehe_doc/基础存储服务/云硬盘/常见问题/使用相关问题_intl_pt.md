### Os discos em nuvem são ideais para quais situações?
- Você pode [adquirir](https://intl.cloud.tencent.com/document/product/362/5744) e [montar](https://intl.cloud.tencent.com/document/product/362/32401) discos em nuvem elásticos para usá-los como discos de dados quando o espaço em disco do seu CVM for insuficiente.
- Você pode adquirir e montar discos em nuvem elásticos para usá-los como discos de dados quando você adquirir um CVM sem discos de dados adicionais.
- Quando você tem 10 GB de dados importantes armazenados em um disco em nuvem elástico em um CVM A e precisa compartilhar os dados com o CVM B. Você pode [desmontar](https://intl.cloud.tencent.com/document/product/362/32400) diretamente o disco do CVM A e [montá-lo](https://intl.cloud.tencent.com/document/product/362/32401) no CVM B.
- Quando um disco em nuvem único de tamanho máximo não atender a seus requisitos de armazenamento, você pode adquirir vários discos em nuvem com capacidade igual e configurar volumes lógicos de LVM para fornecer uma capacidade de disco maior.
- Quando o desempenho de E/S de um único disco não atender às suas necessidades empresariais, você pode adquirir vários discos em nuvem e configurar RAID 0, RIAD 10 etc. para ampliar o desempenho de E/S.

Para obter mais informações, consulte [Casos de uso](https://intl.cloud.tencent.com/document/product/362/3065).

### Como eu escolho um disco em nuvem?
Determine seus casos de uso antes de escolher um tipo de disco.
- Para casos de uso em geral, inclusive aplicativos móveis e da Web, processamento lógico e sites de pequeno e médio porte, nós recomendamos que você escolha o Premium Cloud Storage, pois é a solução mais econômica.
- Para bancos de dados de médio porte e usuários de processamento de imagens, nós recomendamos o SSD para um desempenho melhor.
- Para casos de uso com requisitos mais elevados de cargas de trabalho e desempenho, inclusive bancos de dados maiores, negócios por vídeo, NoSQL e Elasticsearch, nós recomendados que você escolha o Enhanced SSD para ter o desempenho ideal e uma latência de armazenamento mínima.


### Quais aspectos eu devo considerar ao usar um disco em nuvem?
- Para um disco em nuvem adquirido de forma independente, use o UUID do sistema de arquivos ou rotule como o ID do sistema de arquivos quando configurar as informações do sistema de arquivos estático `fstab`. Isso garantirá a consistência do nome do kernel do disco no CVM quando algum disco em nuvem for desmontado e remontado. 
- Se o disco em nuvem expirar antes do CVM, o disco em nuvem será limitado, desmontado ou até mesmo retomado durante determinado período. Para evitar a interrupção dos negócios, confira a data de expiração do disco em nuvem e renove-o rapidamente.
- Pense em usar a opção `nofail` ao configurar `fstab` se a desmontagem de um disco em nuvem do seu CVM não afetar profundamente seus negócios centrais. Isso evita que o CVM relate um erro ao ser reiniciado após a desmontagem do disco em nuvem.
- Nós recomendamos que você execute `san policy=OnlineAll` em `diskpart` antes de usar o disco em nuvem no Windows.
- Ao desmontar um disco em nuvem do Windows, nós recomendamos que você primeiramente interrompa as operações de leitura/gravação do disco e realize a operação `offline`.

### Se uma imagem personalizada e um snapshot do disco de dados forem usados, como eu monto automaticamente o disco de dados ao iniciar uma nova instância?
Para obter mais informações, consulte a seção “Montagem automática” em [Montagem de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/32401).

### Como eu adquiro um disco em nuvem?
Você pode adquirir um disco em nuvem criando um pelo console ou por uma API. Para obter mais informações, consulte [Criação de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/5744).

### Como eu vejo os detalhes do disco em nuvem?
1. Faça login no [Console do CBS](https://console.cloud.tencent.com/cvm/cbs/index).
2. Na parte superior da página **Cloud Block Storage**, selecione a região onde está o disco que você quer visualizar.
3. Localize o disco na lista e visualize suas informações.
Para ver mais informações, clique no ID/Nome do disco para acessar a página de detalhes.


### Como eu vejo o uso do disco em nuvem no console?

O Cloud Monitor será ativado automaticamente após uma instância do CVM ser criada. Você pode visualizar o uso de um disco em nuvem inicializado, que está montado em um CVM, seguindo as etapas abaixo:
1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm/instance/index) e acesse a página **Instances (Instâncias)**.
2. Selecione o ID/Nome da instância de destino para acessar a página de detalhes.
3. Clique na guia **Monitoring (Monitoramento)** para exibir o uso de disco da instância.

### Quais são as operações mais comuns do disco em nuvem?
Para obter mais informações, consulte [Visão geral das operações](https://intl.cloud.tencent.com/document/product/362/33140).


### Por que eu não consigo localizar o CVM no qual quero montar um disco em nuvem?
Os discos em nuvem não podem ser montados em zonas de disponibilidade diferentes. Confira se a instância do CVM que você quer usar não foi liberada e se está na mesma região e zona de disponibilidade que seu disco em nuvem.

### Por que eu não consigo ver a capacidade do novo disco em nuvem que eu montei em uma instância do CVM?
Alguns CVMs do Linux talvez não reconheçam um disco em nuvem elástico. Primeiramente, você deve ativar a função de permutação a quente do disco no CVM. Para obter mais informações, consulte [Ativação da função de permutação a quente do disco](https://intl.cloud.tencent.com/document/product/362/32401#modprobeacpiphp).

Após a montagem manual de um disco em nuvem, você deve realizar as operações subsequentes mostradas abaixo para que ele possa ser usado.
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
	<td><ul class="params"><li>Montagem em um CVM do Windows: depois de fazer login na instância, coloque o disco online por meio de **Server Management (Gerenciamento do servidor)** > **Storage (Armazenamento)** > **Disk Management (Gerenciamento do disco)**.</li>
		<li>Montagem em um CVM do Linux: depois de fazer login na instância, execute o comando <code>mount <disk partition> <mount point></code>, como <code>mount /dev/vdb /mnt</code>.</li>
		</ul>
	</li></td>
 </tr>
 </tr>
 <tr>
 <td nowrap="nowrap">Capacidade do snapshot < Capacidade do disco em nuvem ≤ 2 TB <br/>ou<br/>2 TB < Capacidade do snapshot < Capacidade do disco em nuvem</td>
<td><ul class="params"><li>Montagem em um CVM do Windows: <a href="https://intl.cloud.tencent.com/document/product/362/31601">extensão de partições e sistemas de arquivos (Windows)</a></li><li>Montagem em um CVM do Linux: <a href="https://intl.cloud.tencent.com/document/product/362/31602">extensão de partições e sistemas de arquivos (Linux)</a></li></ul></td>
 </tr> 
 <tr>
 <td>Capacidade do snapshot ≤ 2 TB < Capacidade do disco em nuvem</td>
<td nowrap="nowrap"><ul class="params"><li>Se o snapshot usar o formato de partição MBR:</li>Consulte <a href="https://intl.cloud.tencent.com/document/product/362/31598">Inicialização de discos em nuvem (maiores que 2 TB)</a> para usar a partição GPT em vez disso.<b>Essa operação excluirá os dados originais.</b><li>Se o snapshot usar o formato de partição GPT:<ul><li>Montagem em um CVM do Windows:<a href="https://intl.cloud.tencent.com/document/product/362/31601">extensão de partições e sistemas de arquivos (Windows)</a></li><li>Montagem em um CVM do Linux:<a href="https://intl.cloud.tencent.com/document/product/362/31602">extensão de partições e sistemas de arquivos (Linux)</a></li></ul></td>
 </tr> 
 </table>

 <style>
	.params{margin-bottom:0px !important;}
</style>


### Como eu particiono e formato discos em nuvem montados?
Para obter mais informações, consulte [Inicialização de discos em nuvem (menores que 2TB)](https://intl.cloud.tencent.com/document/product/362/31597) ou [Inicialização de discos em nuvem (maiores que 2 TB)](https://intl.cloud.tencent.com/document/product/362/31598).

### Qual é a relação entre a gravação de dados e a formatação de partições?
Um novo disco de dados ou uma partição de disco de dados devem ser formatados antes do uso. O disco também deve ser gravado com a estrutura dos dados. Formatar o disco estabelece um sistema de arquivos no disco de dados para a gravação de dados. O tamanho dos dados de gravação varia dependendo dos sistemas de arquivos:
- Para Windows:
   - Formatação rápida: atribui o sistema de arquivos apenas a partições e regrava a tabela do diretório com pouco uso da capacidade do seu disco.
   - Formatação padrão: além de realizar as tarefas da formatação rápida, a formatação normal escaneia as partições setor por setor para identificar e marcar setores com problemas e preenche blocos vazios do disco em nuvem, o que significa que ela basicamente grava dados em todo o disco. Portanto, a capacidade do primeiro snapshot é próxima à do disco em nuvem.
- Para Linux: após o disco em nuvem ser formatado e antes de haver a gravação dos dados na instância, a capacidade do primeiro snapshot depende do formato do sistema de arquivos do disco.

### É possível agregar a capacidade do disco de dados e a capacidade do disco do sistema?
Não. Para aumentar a capacidade de armazenamento, é necessário [expandir o disco de dados ou o disco do sistema](https://intl.cloud.tencent.com/document/product/362/5747).

### Depois de expandir meu disco em nuvem, eu preciso desmontar as partições existentes ao criar uma partição nova e independente no Linux? 
Sim. Para fazer isso, siga as etapas abaixo:
1. Execute o seguinte comando para desmontar o disco de dados.
```
umount <Mount point>
```
Se o ponto de montagem for `/data`, execute o comando a seguir:
```
umount /data
```
2. Desmonte os sistemas de arquivos de todas as partições do disco em nuvem e realize as operações subsequentes. Você pode executar o comando novamente para confirmar que a operação de desmontagem foi bem-sucedida.
```
mount | grep '<Disk path>'
```
Se o valor retornado for nulo, significa que todos os sistemas de arquivos foram desmontados das partições do disco em nuvem.


### É possível que vários CVMs acessem um disco em nuvem?
Não. Você pode montar até 20 discos em nuvem no mesmo CVM, mas não pode montar o mesmo disco em nuvem em vários CVMs. Só é possível compartilhar dados [desmontando o disco de dados](https://intl.cloud.tencent.com/document/product/362/32400) do CVM A e depois [montando-o](https://intl.cloud.tencent.com/document/product/362/32401) no CVM B.

### Como eu identifico discos em nuvem do mesmo tamanho e tipo montados no mesmo CVM?
- No Linux, você pode ver a relação entre os discos em nuvem elásticos e o nome do dispositivo executando o comando a seguir:
```
ls -l /dev/disk/by-id
```
![](https://main.qcloudimg.com/raw/66b6a19695ef4ba21b74ce0cd96503db.png)
- No Windows, você pode ver a relação executando o comando a seguir:
```
wmic diskdrive get caption,deviceid,serialnumber
```
Ou
```
wmic path win32_physicalmedia get SerialNumber,Tag
```
![](https://main.qcloudimg.com/raw/e91aa2f938ddda304844d7ac28840859.png)

### Eu posso alterar um disco do sistema do CVM de um disco local para um disco em nuvem?
Sim. Para fazer isso, siga as etapas abaixo:
>!Consulte [Criação de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4942) e [Criação de snapshots](https://intl.cloud.tencent.com/document/product/362/5755) para fazer backup dos dados antes de realizar operações para garantir a segurança dos dados.
>

1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm/instance/index) e acesse a página **Instances (Instâncias)**.
2. Localize a instância cujo disco você deseja alterar, selecione **More (Mais)** > **Instance Status (Status da instância)** > **Shutdown (Desligar)** na coluna **Operation (Operação)** para desligar a instância selecionada.
3. Após a instância ser encerrada, selecione **More (Mais)** > **Resource Adjustment (Ajuste de recursos)** > **Change Disk Media Type (Alterar tipo de mídia do disco)**.
4. Na janela pop-up, selecione um tipo de disco em nuvem de destino, marque **I have read and agreed to Rules for Changing Disk Media Type (Li e concordo com as regras de alteração do tipo de mídia do disco)** e clique em **Change Now (Alterar agora)**.
5. Verifique novamente as informações, efetue o pagamento, se aplicável, e aguarde a conclusão do processo.
>?
>
>- Para obter mais informações, consulte [Alteração do tipo de mídia do disco](https://intl.cloud.tencent.com/document/product/213/32365).


### Eu posso desmontar o disco de dados que veio com o CVM?
Desde novembro de 2017, os discos de dados adquiridos com os CVMs podem ser desmontados e remontados. Os discos de dados remontados em CVMs com datas de expiração diferentes podem causar problemas de gerenciamento de ciclo de vida útil. Nós disponibilizamos várias opções, como alinhamento de data de expiração e configuração de renovação automática, para que você gerencie melhor os problemas do ciclo de vida útil do disco de dados. Nós recomendamos que você selecione cuidadosamente a opção adequada para evitar perda de dados causada pela expiração do disco.

### Por que o disco em nuvem à parte que eu criei foi liberado junto com minha instância?
Ao montar um disco em nuvem, você pode decidir se ele deve ser liberado com a instância automaticamente. Isso pode ser configurado pelo [Console do CBS](https://console.cloud.tencent.com/cvm/cbs/index) ou pela API [ModifyDiskAttributes](https://intl.cloud.tencent.com/document/product/362/15659).


### O que devo fazer se eu perder meus dados depois de reiniciar minha instância do Linux?
Siga as etapas abaixo se você perdeu todos os dados de um diretório (como /data) depois de reiniciar devido a partições de disco de dados não montadas:
1. Execute o comando `fdisk -l` para visualizar as partições não montadas.
2. Execute o comando `mount /dev/vdb /data` para montar as partições.
3. Execute o comando `df -h` para ver se elas foram montadas com êxito.
4. Conclua suas configurações de [montagem automática](https://intl.cloud.tencent.com/document/product/362/32401#.E6.8C.82.E8.BD.BD.E6.95.B0.E6.8D.AE.E7.9B.98.EF.BC.88linux.EF.BC.89). Então o disco em nuvem será montado automaticamente quando você iniciar sua instância do Linux.

### Quando eu desmontar um disco em nuvem, os dados serão perdidos?
Os dados em discos em nuvem não serão modificados durante a montagem e a desmontagem. Para garantir a consistência dos dados, é altamente recomendável que você siga as etapas abaixo: 
- No Linux, faça login na instância do CVM e execute o comando `umount` no disco em nuvem. Após o comando ser executado, faça login no console do CVM para desmontar o disco em nuvem.
- No Windows, interrompa todas as operações de leitura e gravação em todos os sistemas de arquivos do disco em nuvem antes de desmontá-lo. Caso contrário, os dados cuja leitura ou gravação não foi finalizada serão perdidos. 

### Como eu desmonto um disco em nuvem elástico?
Para obter mais informações, consulte [Desmontagem de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/32400).

### O que acontece com o sistema após a expiração do meu disco em nuvem?
As instruções a seguir se aplicam apenas a discos em nuvem elásticos que permitem a desmontagem. Discos em nuvem não elásticos que não permitem a desmontagem têm o mesmo ciclo de vida útil dos CVMs. Para obter mais informações, consulte [Pagamento em atraso](https://intl.cloud.tencent.com/document/product/213/2181).


- Disco em nuvem com pagamento conforme o uso:
 - Você pode continuar a usar o disco em nuvem com pagamento conforme o uso por 2 horas a partir do momento em que o saldo da sua conta ficar negativo. Você será faturado por esse período. Após 2 horas, os serviços serão suspensos e o disco em nuvem apenas armazenará dados. Até que os dados sejam completamente excluídos, você ainda será faturado de acordo com o faturamento padrão, mesmo que o saldo da conta esteja negativo.
 - Se sua conta do Tencent Cloud apresentar um saldo positivo dentro de 15 dias após a suspensão dos serviços do disco em nuvem, o disco poderá ser restaurado.
 - Se o saldo da conta permanecer negativo por mais de 15 dias após a suspensão dos serviços do disco em nuvem, o disco com pagamento conforme o uso será reavido. Todos os dados serão apagados e **não poderão ser recuperados**. Quando seu disco em nuvem for reavido, o criador da conta do Tencent Cloud e todos os colaboradores receberão uma notificação por e-mail, SMS e Centro de mensagens do console.

Ligue para 4009100100 se precisar de mais informações.

### Eu posso alterar o tipo de disco em nuvem após a conclusão de uma aquisição?
Não. Entretanto, você pode criar um snapshot para backup de dados e depois usar o snapshot para criar um disco em nuvem do tipo que precisar.

### Eu posso ajustar a capacidade do disco em nuvem após a conclusão de uma aquisição?
Sim. Os discos em nuvem permitem o ajuste de capacidade. A capacidade do disco em nuvem pode ser [expandida](https://intl.cloud.tencent.com/document/product/362/31600), mas não reduzida.

### Eu preciso encerrar a instância do CVM antes da expansão de um disco em nuvem?
Não. Você precisa atribuir a capacidade expandida a uma partição existente ou formatá-la em uma nova partição independente. Instruções sobre o sistema operacional do CVM: [Extensão de partições e sistemas de arquivos (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) ou [Extensão de partições e sistemas de arquivos (Linux)](https://intl.cloud.tencent.com/document/product/362/31602).

### Quais são os requisitos para a extensão do sistema de arquivos?
Apenas discos em nuvem permitem a expansão. Discos locais não podem ser expandidos. Para obter mais informações, consulte [Cenários de expansão de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/31600).
>!
> - É altamente recomendável que você crie um snapshot antes da expansão para garantir a segurança dos dados.
> - Se a capacidade máxima do disco em nuvem não conseguir atender às suas necessidades empresariais, tente [criar grupos RAID](https://intl.cloud.tencent.com/document/product/362/2932) ou [criar volumes lógicos de LVM com vários discos em nuvem elásticos](https://intl.cloud.tencent.com/document/product/362/2933).
>- A partição MBR é compatível com discos com capacidade máxima de 2 TB. Ao particionar o disco com capacidade superior a 2 TB, recomendamos que você crie e monte um novo disco de dados e use o formato de partição GPT para copiar os dados.

### Como eu expando um disco em nuvem?
Para obter mais informações sobre operações de expansão, consulte [Cenários de expansão de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/31600).

### Por que a capacidade parece continuar igual após eu ter expandido meu disco de dados?
A expansão pelo console apenas aumenta a capacidade de armazenamento do disco de dados. Você também precisa fazer login na sua instância do CVM e estender as partições e os sistemas de arquivos. Para obter mais informações, consulte:
 - [Extensão de partições e sistemas de arquivos (Windows)](https://intl.cloud.tencent.com/document/product/362/31601)
 - [Extensão de partições e sistemas de arquivos (Linux)](https://intl.cloud.tencent.com/document/product/362/31602)


### Os CVMs permitem a expansão de CPU/memória? 
Se o disco do sistema do CVM for um disco em nuvem, você poderá ajustar sua CPU e memória.

### O que devo fazer se o disco em nuvem for particionado no formato MBR e não puder ser expandido?
A partição MBR é compatível com disco com capacidade máxima de 2 TB. Ao particionar o disco com capacidade superior a 2 TB, recomendamos que você crie e monte um novo disco de dados e use o formato de partição GPT para copiar os dados.

### O que devo fazer se um disco em nuvem não conseguir atender às minhas necessidades empresariais mesmo na capacidade máxima?
Nós recomendamos que você [crie grupos RAID](https://intl.cloud.tencent.com/document/product/362/2932) ou [crie volumes lógicos de LVM com vários discos em nuvem elásticos](https://intl.cloud.tencent.com/document/product/362/2933).

### Como eu crio um grupo RAID usando vários discos em nuvem elásticos?
Para obter mais informações, consulte [Criação de grupos RAID](https://intl.cloud.tencent.com/document/product/362/2932).

### Como eu crio volumes lógicos de LVM usando vários discos em nuvem elásticos?
Para obter mais informações, consulte [Criação de volumes lógicos de LVM para vários discos em nuvem elásticos](https://intl.cloud.tencent.com/document/product/362/2933).

### Como eu exporto os dados de um disco em nuvem?
Você pode usar FTP para fazer upload e download dos dados. Para obter mais informações, consulte [Criação do serviço FTP (Windows)](https://intl.cloud.tencent.com/document/product/213/10414) e [Criação do serviço FTP (Linux)](https://intl.cloud.tencent.com/document/product/213/10912).

### O que acontece com os dados quando um CVM é encerrado?
- O ciclo de vida útil de um disco do sistema é igual ao do CVM. Quando um CVM é encerrado, os dados armazenados no disco do sistema também são encerrados.
- O ciclo de vida útil de um disco de dados (ou seja, de um disco em nuvem elástico) é independente do ciclo de um CVM. Você pode decidir se um disco em nuvem elástico e seus dados serão mantidos após a expiração de um CVM.

Portanto, nós recomendamos que você use discos em nuvem elásticos para armazenar dados que precisam ser salvos no longo prazo.
### Como discos em nuvem podem ser recuperados depois de serem formatados?
Os discos em nuvem não podem ser recuperados depois de serem formatados. Nós recomendados que você [crie um snapshot](https://intl.cloud.tencent.com/document/product/362/5755) antes da formatação.

### Como eu excluo um disco em nuvem?
- O ciclo de vida útil de um disco do sistema é igual ao do CVM. Ele só pode ser excluído quando a [instância do CVM for encerrada](https://intl.cloud.tencent.com/document/product/213/4930).
- O ciclo de vida útil de um disco de dados (ou seja, de um disco em nuvem elástico) é independente do ciclo do CVM. Ele pode ser excluído separadamente. Para obter mais informações, consulte [Encerramento de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/32399).

### Meu disco do sistema pode ser particionado?
Não.


### Como eu atualizo as informações de montagem no ponto de montagem?
O LinuxOS aceita o comando `systemd mount`, o qual vai gerar um arquivo de configuração de montagem sobre o arquivo .mount existente. A montagem no mesmo diretório `/run/systemd/generator/` será afetada por esse comando.
#### Problema
Considere que você montou o disco de dados vdb no diretório `/opt/apps` (execute o comando `mount -a` no arquivo fstab com base no disco uuid). Agora você deverá montar um novo disco de dados vdc no mesmo diretório e substituir o antigo. Se você montar o vdc diretamente no diretório, não será possível ler os dados.
#### Solução
1. Exclua a configuração do ponto de montagem correspondente (por exemplo, execute o comando `rm /run/systemd/generator/opt-apps.mount`).
2. Execute o comando `reload` (por exemplo, use `systemctl daemon-reload`).
3. Monte o disco de dados (por exemplo, execute o comando `mount /dev/vdc /opt/apps`).


