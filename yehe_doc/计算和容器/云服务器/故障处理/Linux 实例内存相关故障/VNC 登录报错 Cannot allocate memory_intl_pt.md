## Descrição do erro
Não consigo fazer login no CVM via VNC e recebo a mensagem de erro “Cannot allocate memory (Não é possível alocar memória)”.
![](https://main.qcloudimg.com/raw/0a31fdd909701c27c9923b2fff24668a.png)

## Possíveis causas[](id:PossibleCauses)
Esse problema pode ser causado por muitas huge pages. O tamanho de uma huge page padrão é 2048 KB. A quantidade de huge pages é indicada em `/etc/sysctl.conf`. Se houver 1280 huge pages (conforme mostrado abaixo), significa que 2,5 GB de memória estão ocupados. Em casos de baixa especificação de instância, a memória pode ser insuficiente para a executar o sistema adequadamente, e você não poderá entrar no sistema após reiniciá-lo.
![](https://main.qcloudimg.com/raw/1978a0b2a85fc828674f720c108c48a3.png)


## Soluções
1. Siga o [procedimento de solução de problemas](#ProcessingSteps) para verificar se a quantidade total de threads supera o limite. 
2. Modifique as configurações das huge pages conforme necessário.


## Procedimento de solução de problemas[](id:ProcessingSteps)
1. Verifique se a quantidade total de threads excede o limite conforme instruído em [Erro de log “fork: Cannot allocate memory (fork: Não é possível alocar memória)”](https://intl.cloud.tencent.com/document/product/213/40502). Se não exceder, prossiga para a próxima etapa.
2. Entre no modo de usuário único e faça login no CVM. Para mais instruções, consulte a seção [Inicialização no modo de usuário único do Linux](https://intl.cloud.tencent.com/document/product/213/34819).
3. Execute o comando a seguir para verificar as configurações de huge pages.
```
cat /etc/sysctl.conf | grep hugepages
```
Se houver muitas huge pages, siga as etapas a seguir para modificar as configurações.
4. Execute o comando a seguir para abrir o arquivo de configuração `/etc/sysctl.conf` com o editor VIM.
```
vim /etc/sysctl.conf
```
5. Pressione **i** para entrar no modo de edição e reduza o valor de `vm.nr_hugepages` conforme necessário.
6. Pressione **Esc**, digite **:wq**, e pressione **Enter** para salvar as configurações e sair do editor VIM.
7. Execute o comando a seguir para que a configuração entre em vigor.
```
sysctl -p
```
8. Depois, reinicie o CVM e você poderá fazer login normalmente.
