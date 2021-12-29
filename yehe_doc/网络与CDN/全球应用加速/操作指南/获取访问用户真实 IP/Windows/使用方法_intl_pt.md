## Versão geral
### Estrutura de dados e descrição da função
- **class ToaFetcher**
Uma classe de assunto que é usada para gerenciar a aquisição e liberação do TOA.
- **InitUpToaFetcher**
 1. Descrição da função 
Esta função é usada para inicializar o TOA fetcher.
```
bool InitUpToaFetcher(char *ncard_ip_str, char *svr_ip_str, u_short svr_port[], u_short svr_port_num, u_short cache_secs=TIMER_CACHE_SECS)
```
 2. Descrição dos parâmetros de entrada
    - ncard_ip_str: usado para identificar a string do endereço IP da interface de rede, por exemplo, 10.75.132.39. Este é o NIC que se comunica com o NIC do cliente.
- svr_ip_str: a string do endereço IP do servidor, por exemplo, 10.75.132.39. É usado na filtragem de fluxos do TCP.
    - svr_port: a lista de portas do servidor. É usado na filtragem de fluxos do TCP. É possível adicionar três portas, no máximo. Deve ser configurado o `svr_port` ou o `port_range_ptr`.
    - svr_port_num: a quantidade de portas do servidor.
    - port_range_ptr: os ponteiros da matriz do intervalo de portas do servidor, em que os elementos são ponteiros que apontam para strings. O formato da string do intervalo de portas é 10001 - 10005; é possível adicionar três intervalos, no máximo. É usado na filtragem de fluxos do TCP. Deve ser configurado o `svr_port` ou o `port_range_ptr`.
    - port_range_num: a quantidade de intervalos de portas do servidor.
    - cache_secs: a duração do cache em segundos. Por padrão, 15 segundos. Para obter mais detalhes, consulte `toa_fetcher.h: TIMER_CACHE_SECS`. O TOA não será mais salvo depois que o cache expirar.
 3. Valores de retorno
    - TRUE: foi criada uma thread adicional para obter o TOA
    - FALSE: falha na criação de uma thread adicional para obter o TOA
- **FetchToaValue**
 1. Descrição da função
Esta função é usada para obter o valor do TOA. Se o pacote tcp-syn interagiu, o TOA pode ser obtido depois de aguardar por até 1 ms. Normalmente, o handshake triplo leva mais de 1 ms.
```
bool FetchToaValue(u_long fake_client_ip_addr, u_short fake_client_port, u_long &real_client_ip_addr, u_short &real_client_port)
```
 2. Descrição dos parâmetros de entrada
    - fake_client_ip_addr: o endereço IP falso do cliente armazenado na ordem de bytes da rede e que pode ser obtido a partir do endereço do par que é retornado pela função `accept` do servidor.
    - fake_client_port: o número de porta falso do cliente armazenado na ordem de bytes da rede e que pode ser obtido a partir do endereço do par que é retornado pela função `accept` do servidor.
    - real_client_ip_addr: o endereço IP real do cliente armazenado na ordem de bytes da rede e que pode ser obtido no TOA.
    - real_client_port: o número de porta real do cliente armazenado na ordem de bytes da rede e que pode ser obtido no TOA.
 3. Valores de retorno
    - TRUE: o TOA foi obtido.
    - FALSE: falha na obtenção do TOA. Um motivo comum pode ser que o TOA esteja limpo porque o tempo de cache foi excedido.
- **StopToaFetcher**
 1. Descrição da função
Esta função é usada para interromper o TOA fetcher.
```
void StopToaFetcher()
```
 2. Descrição dos parâmetros de entrada
Nenhuma
 3. Valores de retorno
Nenhuma
- **GetFetcherStatus**
 1. Descrição da função
Esta função é usada para obter o status do Fetcher.
```
int GetFetcherStatus()
```
 2. Descrição dos parâmetros de entrada
Nenhuma
 3. Valores de retorno
    - 0: indica o status inicial. A instância estará com esse status depois de ser iniciada. Na inicialização do Fetcher, o status inicial permanece inalterado. Quando ocorre um erro, -1 é retornado e, quando é executado com êxito, 1 é retornado.
    - -1: indica uma exceção.
    - 1: indica funcionamento normal.
- **FetchThreadHandler**
 1. Descrição da função
Esta função é usada para obter o manipulador de thread adicional do TOA.
```
HANDLE FetchThreadHandler()
```
 2. Descrição dos parâmetros de entrada
Nenhuma
 3. Valores de retorno
O manipulador de thread adicional do TOA. Quando a instância do ToaFetcher for encerrada, o manipulador será fechado.
- **FetchErrorInfo**
 1. Descrição da função
Esta função é usada para obter o código de erro.
```
bool FetchErrorInfo(int* err_code_ptr, char* err_msg_ptr)
```
 2. Descrição dos parâmetros de entrada
    - err_code_ptr: um ponteiro de número inteiro que aponta para o código de erro e é usado para retornar o código de erro.
    - err_msg_ptr: um ponteiro de caractere que aponta para um buffer de string. Tem pelo menos 50 bytes e é usado para retornar uma mensagem de erro.
 3. Valores de retorno
    - TRUE: foi obtido.
    - FALSE: falha na obtenção.

### Códigos de erro

| Código | Mensagem | Descrição |
|---------|---------|---------|
| 0	       | Ok	| Normal |
| -1001|Excedeu a quantidade máxima de portas do servidor |A quantidade máxima de portas foi excedida. Verifique `InitUpToaFetcher: svr_port_num`. |
| -1002	| Endereço IP inválido	| Endereço IPv4 inválido. |
| -1003| Sem interface de rede adequada| Nenhuma interface de rede adequada foi encontrada |
| -1004| Erro do sistema: erro ao procurar dev| Erro do sistema: `dev` não encontrado. Entre em contato com o desenvolvedor de lib. |
| -1005	| Erro do sistema: erro ao iniciar o temporizador	|Erro do sistema: erro de inicialização do temporizador. Entre em contato com o desenvolvedor de lib. |
| -1006| Erro do sistema: erro ao compilar o filtro| Erro do sistema: erro de compilação da regra de filtro. Entre em contato com o desenvolvedor de lib. |
| -1007	| Erro do sistema: erro ao definir o filtro	| Erro do sistema: erro de configuração da regra de filtro. Entre em contato com o desenvolvedor de lib. |
| -1008	| Erro do sistema: erro ao abrir o pcap |	Erro do sistema: erro de ativação de ‘dev’. Entre em contato com o desenvolvedor de lib. |
| -1009	| Erro do sistema: erro ao iniciar o pcap	|Erro do sistema: erro de ativação de escuta. Entre em contato com o desenvolvedor de lib. |
| -1010	| Erro do sistema: erro ao iniciar a thread	| Erro do sistema: erro de ativação da thread. Entre em contato com o desenvolvedor de lib. |
| -1999	| Erro desconhecido	| Erro desconhecido. Entre em contato com o desenvolvedor de lib. |

### Exemplo
- **Inicializar ToaFetcher:**
```
char ncard_ip_str[] = "1.1.1.1";
char svr_ip_str[] = "1.1.1.1";
char port_range[3][100] = {"10001-10005", "20001-20005", "30001-30005"};
char* port_range_ptr[3] = {port_range[0], port_range[1], port_range[2]};
        u_short svr_port_list[3] = {1111, 2222, 3333};
        ToaFetcher inst = ToaFetcher();
        inst.InitUpToaFetcher((char*)ncard_ip_str, (char*)svr_ip_str, svr_port_list, 3);
```
- **Obter TOA:**
```
void GetToa(SOCKADDR_IN client_addr, ToaFetcher * toa_fetcher_ptr)
{
	u_long fake_client_ip_addr = 0;
	u_short fake_client_port = 0;
	u_long real_client_ip_addr = 0;
	u_short real_client_port = 0;
	memcpy(&fake_client_ip_addr, &client_addr.sin_addr, 4);
	memcpy(&fake_client_port, &client_addr.sin_port, 2);
	bool ret = toa_fetcher_ptr->FetchToaValue(fake_client_ip_addr, fake_client_port, real_client_ip_addr, real_client_port);
	if(ret == FALSE){
		printf("No toa found\n");
	}else{
    	//fpp: Função de impressão personalizada
		fpp("real_client_ip_addr", &real_client_ip_addr, 4);	
　　fpp("real_client_port", &real_client_port, 2);
	}
}
```

## Versão de Go
O programa de obtenção do TOA obtém o endereço IP real de toa_win.exe por meio da comunicação UDP.
### Formato do protocolo
- ** Solicitação:** `| ID（4Bytes）|  FakeIPAddress（4Bytes）| FakePort（2Bytes）|`
 **Os campos são descritos da seguinte maneira:**
 - ID: 4 bytes. ID exclusivo da solicitação. Ele será retornado na resposta da forma que estiver.
 - FakeIPAddrss: 4 bytes. o endereço IP falso do cliente armazenado na ordem de bytes da rede e que pode ser obtido a partir do endereço do par que é retornado pela função `accept` do servidor.
 - FakePort: 2 bytes. o número de porta falso do cliente armazenado na ordem de bytes da rede e que pode ser obtido a partir do endereço do par que é retornado pela função `accept` do servidor.

- **Resposta:** `| ID（4Bytes）| Code（1Byte）| RealIPAddress（4Bytes）| RealPort（2Bytes）|`
**Os campos são descritos da seguinte maneira:**
 - ID: 4 bytes. ID exclusivo de uma solicitação; é igual ao da string de solicitação.
 - Code: 1 byte. 0: IP real e porta obtidos. 1: falha na obtenção.
 - RealIPAddress: 4 bytes. Ordem de bytes da rede. Quando Code = 0, indica o endereço IP real do cliente.
 - RealPort: 2 bytes. Ordem de bytes da rede. Quando Code = 0, indica a porta real do cliente.

### Exemplos
Para obter mais detalhes, consulte demo.go. Você pode desenvolver um cliente de obtenção de TOA ou pode usar a função `queryTOA` em demo.go para obter o TOA.
1. **Descrição da função**
```
func queryToa(serverAddr string, fakeIp string, fakePort uint16)(int32, string, uint16)
```
2. **Descrição dos parâmetros de entrada**
 - serverAddr: Tipo de string, o endereço de comunicação do serviço de toa_win.exe. Formato: 127.0.0.1:9999.
 - fakeIp: Tipo de string, o endereço IP falso. Formato: 1.2.3.4.
 - fakePort: tipo uint16, porta falsa. Formato: 8899.
3. **Valores de retorno**
 - O primeiro valor de retorno: tipo int32. Usado para indicar o código de erro.
    - 0: foi obtido.
    - -1: falha na obtenção do TOA. Isso pode acontecer se `fakeIP` e `fakePort` estiverem incorretos ou se o cache expirar.
    - -2: Falha de exceção de comunicação de rede.
 - O segundo valor de retorno: o tipo de string. Retorna o IP real quando o TOA é obtido; caso contrário, é uma string vazia.
 - O terceiro valor de retorno: tipo uint16. Retorna a porta real quando o TOA é obtido. Caso contrário, é 0.
