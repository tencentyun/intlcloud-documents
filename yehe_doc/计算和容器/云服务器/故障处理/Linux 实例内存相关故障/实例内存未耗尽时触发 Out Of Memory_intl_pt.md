## Descrição do erro
O CVM do Linux não excede o consumo de memória e aciona OOM (Out of Memory, Memória Insuficiente) conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/72cbd63ac445a1caa8d82fa1e55ba5a5.png)

## Possíveis causas
Este problema pode ser causado pela configuração `min_free_kbytes`. Ela especifica a memória ociosa mínima do sistema Linux (em kilobytes). Quando a memória disponível do sistema ficar abaixo do valor definido de `min_free_kbytes`, o sistema acionará o oom-killer ou reiniciará de forma forçada dependendo do parâmetro do kernel `vm.panic_on_oom`:
 - Se estiver definido como `vm.panic_on_oom=0`, o sistema exibe OOM e invoca o oom-killer para encerrar o processo usando mais memória.
 - Se estiver definido como `vm.panic_on_oom =1`, o sistema reiniciará automaticamente.

## Soluções
1. Siga o [procedimento de solução de problemas] para verificar o consumo de memória e a quantidade total de threads.
2. Corrija a configuração de `min_free_kbytes`.


## Procedimento de solução de problemas[](id:ProcessingSteps)
1. Verifique o consumo de memória conforme indicado em [Alto consumo de memória](https://intl.cloud.tencent.com/document/product/213/40501). Se o consumo de memória estiver normal, siga para a próxima etapa.
2. Verifique se a quantidade de threads excede o limite conforme indicado em [Erro de log “fork: Cannot allocate memory (fork: Não é possível alocar memória)”](https://intl.cloud.tencent.com/document/product/213/40502). Se a quantidade de threads estiver dentro do limite, siga para a próxima etapa.
3. Faça login no CVM e execute o comando abaixo para acessar a configuração de `min_free_kbytes`.
```
sysctl -a | grep min_free
```
O valor de `min_free_kbytes` está em kbytes. Por exemplo, o `min_free_kbytes = 1024000` mostrado abaixo representa 1 GB.
![](https://main.qcloudimg.com/raw/18ac6c04962abfbf67132eab1a604167.png)
4. Execute o comando a seguir para abrir o arquivo de configuração `/etc/sysctl.conf` com o editor VIM.
```
vim /etc/sysctl.conf
```
5. Pressione **i** para entrar no modo de edição e modifique o a configuração `vm.min_free_kbytes`.
>? Recomendamos alterar o valor de `vm.min_free_kbytes` para não mais que 1% da memória total.
>
6. Pressione **Esc**, digite **:wq**, e pressione **Enter** para salvar as configurações e sair do editor VIM.
7. Execute o comando a seguir para que a configuração entre em vigor.
```
sysctl -p
```
