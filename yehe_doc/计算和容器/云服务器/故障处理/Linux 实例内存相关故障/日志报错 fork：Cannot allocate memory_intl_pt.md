## Descrição do erro
O log apresenta a mensagem de erro “fork: Cannot allocate memory (fork: Não é possível alocar memória)”.
![](https://main.qcloudimg.com/raw/db85a43e7495f1655a2b59063ffc33e3.png)

## Possíveis causas
Esse problema pode ser causado por threads excessivas. Se uma nova thread for criada após o valor de `pid_max` ser atingido, a mensagem de erro “fork: Cannot allocate memory (fork: Não é possível alocar memória)” será exibida.

## Soluções
1. Consulte o [procedimento de solução de problemas](#ProcessingSteps) para verificar o consumo de memória.
2. Verifique a quantidade de threads e modifique a configuração de `pid_max`. 



## Procedimento de solução de problemas[](id:ProcessingSteps)
1. Verifique o consumo de memória conforme indicado em [Alto consumo de memória](https://intl.cloud.tencent.com/document/product/213/40501). Se o consumo de memória estiver normal, vá para a próxima etapa.
2. Execute o comando a seguir para obter o valor de `pid_max`.
```
sysctl -a | grep pid_max
```
O valor padrão de `pid_max` é `32768`, conforme abaixo:
![](https://main.qcloudimg.com/raw/816a0bd183244aadf14e04c6ed200d68.png)
3. Execute o comando a seguir para exibir a quantidade total de threads.
```
pstree -p | wc -l
```
Quando a quantidade total de threads atingir `pid_max`, uma nova thread causará o erro “fork: Cannot allocate memory (fork: Não é possível alocar memória)”.
>?Você pode usar o comando `ps -efL` para localizar os programas para os quais muitas threads estão sendo executadas.
>
4. Altere o valor de `kernel.pid_max` no arquivo de configuração `/etc/sysctl.conf` para `65535`, para aumentar a quantidade de threads. O resultado deve ser o seguinte:
![](https://main.qcloudimg.com/raw/a4bbf49b3236b9f50988e914298adb31.png)
5. Execute o comando a seguir para a configuração entrar em vigor.
```
sysctl -p
```
