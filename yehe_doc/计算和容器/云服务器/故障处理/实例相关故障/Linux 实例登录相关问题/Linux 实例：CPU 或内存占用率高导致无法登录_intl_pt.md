## Cenário

Este documento descreve como investigar e resolver problemas, como falha ao fazer login em um CVM do Linux devido ao alto uso de CPU e memória.

## Instruções

### Login e exibição da carga do sistema

1. Faça login no CVM de diferentes maneiras, de acordo com suas necessidades em si.
	- Login remoto no CVM do Linux via software de terceiros.
	> Quando o CVM do Linux tem uma alta carga de CPU, o login pode falhar.
	>
	- Login no CVM via **VNC**.
	Faça login no [console do CVM](https://console.cloud.tencent.com/cvm) > clique em **Log in (Fazer login)** na coluna de operação à direita > faça login com métodos alternativos de login (VNC).
	> Quando o CVM do Linux tiver uma alta carga de CPU, você poderá fazer login normalmente pelo console.
	>
2. Execute o comando a seguir para exibir a carga do sistema. Observe a coluna `%CPU` e a coluna `%MEM`, e identifique quais processos consomem mais recursos.
```
top
```

### Encerramento de processos

1. Compare o consumo de recursos de diferentes processos e registre os PIDs daqueles que precisam ser encerrados.
2. Insira ` k `.
3. Insira o PID do processo que precisa ser encerrado, e pressione **Enter** para encerrá-lo conforme o exemplo abaixo:
Por exemplo, você precisa encerrar um processo cujo PID é 23.
![](//mc.qcloudimg.com/static/img/61cd74354cf2b4d2a80a83528a500f5c/image.png)
> Se `kill PID 23 with signal [15]:` for exibido após você pressionar **Enter**, pressione **Enter** novamente para manter as configurações padrões.
>
4. Se a operação for bem-sucedida, a mensagem ` Send PID 23 signal [15/sigterm] ` será exibida. Pressione **Enter** para confirmar o encerramento.

### Baixo uso de CPU, mas alta média de carga

### Descrição do problema

A média de carga é um indicador da carga de CPU. Uma alta média de carga indica uma longa fila de processos aguardando para serem executados.
Ao executar o comando `top` podemos observar um uso muito baixo de CPU, porém uma média de carga muito alta, conforme ilustrado abaixo.
![](//mc.qcloudimg.com/static/img/4ddf663a68ee602d8cf8075d88edccf6/image.png)
 
#### Solução
 
Execute o comando abaixo para exibir os estados do processo e verificar se há processos no estado D, conforme o exemplo a seguir:
```
ps -axjf
```
![](//mc.qcloudimg.com/static/img/32420d3fe022b57d85120c941705dbf6/image.png)
 > Os processos no estado D estão em suspensão ininterrupta. Os processos nesse estado não podem ser encerrados nem fechados automaticamente. Caso existam muitos processos no estado D, você poderá resolver o problema restaurando os recursos dos quais os processos dependem ou reiniciar o sistema.
 >


### O processo kswapd0 usa muita CPU

### Descrição do problema

O Linux gerencia a memória com o mecanismo de paginação e também reserva uma parte do disco para a memória virtual. O kswapd0 é o processo responsável pela substituição de páginas no gerenciamento de memória virtual do sistema Linux. Quando não há memória suficiente no sistema, o kswapd0 substitui as páginas a todo momento, o que é desgastante para a CPU. É por isso que o processo consome muita CPU.
 
#### Solução

1. Execute o comando a seguir para localizar o processo kswapd0.
```
top
```
2. Confira o estado do processo kswapd0.
Se o processo não estiver em suspensão, estiver em execução por muito tempo e estiver usando muita CPU, execute a [Etapa 3](#kswapd0_step3), para verificar a taxa de uso de memória.
3. <span id="kswapd0_step3">Execute os comandos `free`，`ps` para verificar quanta memória está sendo usada pelos processos no sistema.</span>
Reinicie o sistema ou encerre os processos que são seguros, porém desnecessários, com base na taxa de uso da memória.

Se o problema persistir, consulte [Alta taxa de uso da CPU (sistema Linux)](https://intl.cloud.tencent.com/document/product/213/14634) para mais detalhes.
