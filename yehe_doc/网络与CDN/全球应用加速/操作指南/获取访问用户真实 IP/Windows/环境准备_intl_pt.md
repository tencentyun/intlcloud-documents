### Download de arquivos
Clique [aqui](https://main.qcloudimg.com/raw/037dee0e98e30eb15055645ff0a48694.zip) para baixar o arquivo.

## Versão geral
### Descrição dos arquivos

| Arquivo | Descrição |
| ----------------- | ------------------------------------------------------------ |
| WinPcap_4_1_3.exe | Driver WinPcap, consulte [Documentação do WinPcap](https://www.winpcap.org/) para obter detalhes |
| lib_toa.lib | Biblioteca estática do TOA |
| toa_fetcher.h | Arquivo de cabeçalho do qual a biblioteca estática depende |
| pcap.h | Arquivo de cabeçalho do qual a biblioteca estática depende |

### Preparação do ambiente
1. Clique duas vezes em WinPcap_4_1_3.exe para instalar o driver WinPcap (não é necessário reiniciar).
2. Adicione lib_toa.lib ao caminho da biblioteca .lib do projeto.
3. Adicione toa_fetcher.h e pcap.h ao arquivo de cabeçalho do projeto.

## Versão de Go
### Descrição dos arquivos

| Arquivo | Descrição |
| ------------------- | ------------------------------------------------------------ |
| WinPcap_4_1_3.exe | Driver WinPcap, consulte [Documentação do WinPcap](https://www.winpcap.org/) para obter detalhes |
| toa_win.exe | Programa TOA para Windows Server |
| toa_win.conf | Arquivo de configuração do programa TOA para Windows Server |
| program_auto_up.bat | Script bat para Windows Server |
| demo.go | Um programa de amostra escrito na linguagem Go, usado para acessar os serviços do TOA |

### Etapas de implantação
1. Modifique o arquivo toa_win.conf conforme as instruções abaixo:
<table>
<tr>
<th>Parâmetro</th><th>Obrigatório</th><th>Descrição</th>
</tr>
<tr>
<td>ToaWinPort</td><td>Sim</td><td>A porta de serviço de toa_win.exe, usada para se comunicar com o cliente do TOA, o padrão é 9999.</td>
</tr>
<tr>
<td>NetworkCardIP</td><td>Sim</td><td>Usado para identificar o endereço IP da interface de rede, por exemplo, 10.75.132.39. Este é o NIC que se comunica com o cliente.</td>
</tr>
<tr>
<td>ServerListenIP</td><td>Sim</td><td>O endereço IP do servidor, por exemplo, 10.75.132.39. É usado na filtragem de fluxos do TCP.</td>
</tr>
<tr>
<td>ServerListenPortList</td><td>Não</td><td>A lista de portas do servidor. É usado na filtragem de fluxos do TCP. É possível adicionar três portas, no máximo.<br><b>ServerListenPortList ou PortRange deve ser configurado.</b></td>
</tr>
<tr>
<td>PortRange</td><td>Não</td><td>O intervalo de portas do servidor. É usado na filtragem de fluxos do TCP. É possível adicionar três intervalos de portas, no máximo.<br><b>ServerListenPortList ou PortRange deve ser configurado.</b></td>
</tr>
<tr>
<td>CacheSeconds</td><td>Não</td><td>A duração do tempo de cache, com unidade em segundos. O padrão é 15 segundos. </td>
</tr>
</table>

 >!O arquivo de configuração deve ser colocado no mesmo diretório que toa_win.exe.
 
 ![](https://main.qcloudimg.com/raw/d53c1cb161f45c9ad75789ac1c832af6.png)
2. Modificação de program_auto_up.bat.
Modifique o caminho para o diretório onde o programa está localizado. Adicione o script à tarefa programada e execute-o periodicamente. O script é usado para monitorar o programa toa_win.exe e ativá-lo automaticamente ao fechar.
![](https://main.qcloudimg.com/raw/046bbd4282aa51f85baa6879de8586d4.png)
3. Execute o programa toa_win.exe. O log é salvo em toa_win.log no mesmo diretório. Agora, você pode obter o endereço IP real dos serviços do TOA por meio da comunicação UDP. Para obter mais detalhes, consulte [Como usar](https://cloud.tencent.com/document/product/608/17670).
