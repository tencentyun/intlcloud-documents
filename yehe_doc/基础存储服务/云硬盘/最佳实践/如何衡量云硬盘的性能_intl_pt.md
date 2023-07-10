## Métricas
Os dispositivos do CBS do Tencent Cloud têm desempenho e preços diferentes conforme o tipo. Para obter mais informações, consulte [Tipos de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/31636). Como aplicativos diferentes têm cargas de trabalho diferentes, se a quantidade de solicitações de E/S for baixa, o disco em nuvem poderá não apresentar o desempenho máximo.
As métricas a seguir costumam ser usadas para medir o desempenho de um disco em nuvem:

- IOPS: contagem de leitura/gravação por segundo. O IOPS varia de acordo com o tipo de unidade subjacente do dispositivo de armazenamento.
- Taxa de transferência: volume de dados lidos/gravados por segundo, com unidade em MB/s.
- Latência: tempo decorrido desde o envio de uma operação de E/S até o recebimento da confirmação (em segundos).

## Ferramenta de teste
A FIO é uma ferramenta para teste de desempenho do disco. Ela é usada para realizar teste de estresse e verificação no hardware. Este documento usa a FIO como exemplo.
Nós recomendamos que você use a FIO junto com o mecanismo de E/S do libaio para realizar o teste. Instale a FIO e o libaio consultando [Instalação de ferramentas](#toolInstallation).

>
>- **Para evitar danos em arquivos importantes do sistema, não realize o teste FIO no disco do sistema**.
>- **Para evitar corrompimento dos dados causado pelo corrompimento de metadados do sistema de arquivos de base, não realize o teste em um disco de dados empresarial. **
>- Confira se o arquivo `/etc/fstab` **NÃO contém** a configuração de montagem do disco a ser testado. Caso contrário, poderá não ser possível inicializar o CVM.

## Objetos de teste recomendados
- Nós recomendados que você realize o teste FIO em discos vazios que não armazenam dados importantes e recrie o sistema de arquivos após a conclusão do teste.
- Ao testar o desempenho do disco, recomendados que você teste diretamente discos de dados brutos (como /dev/vdb).
- Ao testar o desempenho do sistema de arquivos, recomendamos que você especifique o teste do arquivo (como /data/file).
<span id="toolInstallation"></span>
## Instalação de ferramentas
1. Faça login no CVM conforme indicado em [Faça login em instância do Linux usando o método de login padrão](https://intl.cloud.tencent.com/document/product/213/5436). Aqui, use como exemplo o CVM que está executando o sistema operacional CentOS 7.6.
2. Execute o seguinte comando para verificar se o disco em nuvem está alinhado com 4KiB.
```
fdisk -lu
```
Conforme mostrado abaixo, se o valor inicial na saída do comando for divisível por 8, significa que o disco está alinhado com 4KiB. Caso contrário, realize o alinhamento com 4KiB antes do teste.
![](https://main.qcloudimg.com/raw/d5726510ea6408a36e11fc21da453137.png)
3. Execute os comandos a seguir em sequência para instalar as ferramentas de teste, FIO e libaio.
```
yum install libaio -y
```
```
yum install libaio-devel -y
```
```
yum install fio -y
```
Após concluído, inicie o teste de desempenho do disco em nuvem conforme indicado no exemplo de teste abaixo.

## Exemplo de teste
As fórmulas de teste para diferentes cenários são basicamente as mesmas, exceto os parâmetros `rw`, `iodepth` e `bs` (tamanho do bloco). Por exemplo, o `iodepth` ideal para cada carga de trabalho é diferente, já que depende da sensibilidade do seu aplicativo ao IOPS e à latência.

Descrição do parâmetro:

<table>
     <tr>
         <th nowrap="nowrap">Parâmetro</th>   
		 <th>Observações</th>
         <th nowrap="nowrap">Valor de amostra</th> 
     </tr>
	 <tr>
         <td>bs</td>
		 <td>Tamanho do bloco por solicitação. Valores válidos incluem 4k, 8k e 16k.</td>
         <td>4k</td>
     </tr>
	 <tr>
         <td>ioengine</td>
		 <td>Mecanismo de E/S. Nós recomendamos que você use o mecanismo de E/S assíncrono do Linux.</td>
         <td>libaio</td>
     </tr>
	 <tr>
         <td>iodepth</td>
		 <td>Profundidade enfileirada de uma solicitação de E/S.</td>
         <td>1</td>
     </tr>
	 <tr>
         <td>direct</td>
		 <td>Especifica o modo direto.<ul><li>True (1) indica que o identificador O_DIRECT é especificado, o cache de E/S será ignorado e os dados serão gravados diretamente.</li><li>False (0) indica que o identificador O_DIRECT não é especificado.</li></ul>O padrão é True (1).</td>
         <td>1</td>
     </tr>
	 <tr>
         <td>rw</td>
		 <td>Modo de leitura e gravação. Valores válidos incluem read, write, randread, randwrite, randrw e rw, readwrite.</td>
         <td>read</td>
     </tr>
	 <tr>
         <td>time_based</td>
		 <td>Especifica que o modo de tempo está sendo usado. Contanto que a FIO seja executada com base no tempo, não é necessário definir esse parâmetro.</td>
         <td>N/A</td>
     </tr>
	 <tr>
         <td>runtime</td>
		 <td>Especifica a duração do teste, que é o tempo de execução da FIO.</td>
         <td>600</td>
     </tr>
	 <tr>
         <td>refill_buffers</td>
		 <td>A FIO vai preencher novamente o buffer de E/S a cada envio. A configuração padrão é preencher o buffer de E/S apenas no início e reutilizar os dados.</td>
         <td>N/A</td>
     </tr>
         <td>norandommap</td>
		 <td>Ao realizar operações de E/S aleatórias, a FIO sobrescreve cada bloco do arquivo. Se este parâmetro estiver definido, uma nova compensação será selecionada sem visualizar o histórico de E/S.</td>
         <td>N/A</td>
     </tr>
	 <tr>
         <td>randrepeat</td>
		 <td>Especifica se a sequência aleatória é repetível. True (1) indica que a sequência aleatória é repetível. False (0) indica que a sequência aleatória não é repetível. O valor padrão é True (1).</td>
         <td>0</td>
     </tr>
         <td>group_reporting</td>
		 <td>Quando vários jobs são simultâneos, as estatísticas do group todo são impressas.</td>
         <td>N/A</td>
     </tr>
	 <tr>
         <td>name</td>
		 <td>Nome do job.</td>
         <td>fio-read</td>
     </tr>
         <td>size</td>
		 <td>Espaço de endereço do teste de E/S.</td>
         <td>100 GB</td>
     </tr>
	 <tr>
         <td>filename</td>
		 <td>Objeto de teste, que é o nome do disco a ser testado.</td>
         <td>/dev/sdb</td>
     </tr>
</table>

Alguns casos de uso comuns são:
- **bs=4k iodepth=1**: teste de leitura/gravação aleatória, que pode refletir o desempenho de latência de um disco.
Execute o comando a seguir para testar a latência de leitura aleatória do disco:
```
fio -bs=4k -ioengine=libaio -iodepth=1 -direct=1 -rw=randread -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-randread-lat --size=10G -filename=/dev/vdb
```
Execute o comando a seguir para testar a latência de gravação aleatória do disco:
```
fio -bs=4k -ioengine=libaio -iodepth=1 -direct=1 -rw=randwrite -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-randwrite-lat --size=10G -filename=/dev/vdb
```
Execute o comando a seguir para testar o desempenho de latência de leitura e gravação aleatória híbrida de um disco em nuvem SSD:
```
fio --bs=4k --ioengine=libaio --iodepth=1 --direct=1 --rw=randrw --time_based --runtime=100 --refill_buffers --norandommap --randrepeat=0 --group_reporting --name=fio-read --size=1G --filename=/dev/vdb 
```
A figura a seguir mostra a saída do comando:
![](https://main.qcloudimg.com/raw/39ffdf41ca9bd28808792b35482fafd0.png)

- **bs=128k iodepth=32**: teste de leitura/gravação sequencial, que pode refletir o desempenho da taxa de transferência do disco.
Execute o comando a seguir para testar a largura de banda da taxa de transferência de leitura sequencial:
```
fio -bs=128k -ioengine=libaio -iodepth=32 -direct=1 -rw=read -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-read-throughput --size=10G -filename=/dev/vdb
```
Execute o comando a seguir para testar a largura de banda da taxa de transferência de gravação sequencial:
```
fio -bs=128k -ioengine=libaio -iodepth=32 -direct=1 -rw=write -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-write-throughput --size=10G -filename=/dev/vdb
```
Execute o comando a seguir para testar o desempenho da taxa de transferência de leitura sequencial de um disco em nuvem SSD:
```
fio --bs=128k --ioengine=libaio --iodepth=32 --direct=1 --rw=read --time_based --runtime=100 --refill_buffers --norandommap --randrepeat=0 --group_reporting --name=fio-rw --size=1G --filename=/dev/vdb
```
A figura a seguir mostra a saída do comando:
![](https://main.qcloudimg.com/raw/f21de73d7c20d32396d43b11dd756c26.png)

- **bs=4k iodepth=32**: teste de leitura/gravação aleatória, que pode refletir o desempenho de IOPS do disco rígido.
Execute o comando a seguir para testar o IOPS de leitura aleatória do disco:
```
fio -bs=4k -ioengine=libaio -iodepth=32 -direct=1 -rw=randread -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-randread-iops --size=10G -filename=/dev/vdb
```
Execute o comando a seguir para testar o IOPS de gravação aleatória do disco:
```
fio -bs=4k -ioengine=libaio -iodepth=32 -direct=1 -rw=randwrite -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-randwrite-iops --size=10G -filename=/dev/vdb
```
Teste o desempenho do IOPS de leitura aleatória do disco em nuvem SSD. Isso é mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/b6aaf207adffdb85ba7da487b4fd2ce9.png)
