## 1. Qual é a média de carga do servidor Linux?

A carga é usada para medir a carga de trabalho de um servidor; ou seja, o comprimento da fila de tarefas a serem executadas pela CPU. Quanto maior o valor, mais processos estão em execução ou aguardando para serem executados.

## 2. Como posso verificar a carga do servidor Linux?

Você pode executar os comandos `w`, `top`, `uptime` e `procinfo` ou acessar o arquivo `/proc/loadavg` para exibir a carga.
Consulte "Instalação de software no ambiente Linux" para obter instruções sobre como instalar a ferramenta procinfo. 

## 3. O que devo fazer quando a carga do servidor estiver muito alta?

A carga/média da carga do servidor é exibida com base no comprimento da fila de processos. Uma alta carga do servidor (recomendamos referenciar a média de 15 minutos) pode ser causada por recursos insuficientes da CPU, gargalos de leitura/gravação de E/S, recursos de memória insuficientes ou tarefas de computação intensivas. Recomendamos que você execute os comandos `vmstat`, `iostat` e `top` para identificar o motivo da alta carga e otimizar os processos. 

## 4. Como verifico o uso de memória do servidor?

Você pode verificar o uso de memória do servidor executando os comandos `free`, `top` (após a execução, você pode pressionar `shift+m` para classificar a memória), `vmstat` e `procinfo` ou acessando o arquivo `/proc/meminfo`. 

## 5. Como verifico o uso de memória de um único processo?

Você pode verificar o uso de memória de um único processo executando os comandos `top -p PID`, `pmap -x PID` e `ps aux|grep PID` ou acessando o arquivo `/proc/$process_id (process PID) /status` (por exemplo, o arquivo `/proc/7159/status`). 

## 6. Como verifico os serviços e as portas que estão em uso no momento?

Você pode verificar os serviços e as portas que estão em uso no momento executando os comandos `netstat -tunlp`, `netstat -antup` e `lsof -i:PORT`. 

## 7. Como posso verificar as informações de processos do servidor?

Você pode verificar as informações de processos do servidor executando os comandos `ps auxww|grep PID`, `ps -ef`, `lsof -p PID` e `top -p PID`. 

## 8. Como faço para parar um processo?

Você pode executar `kill -9 PID` (PID indica o ID do processo) e `killall program name` (por exemplo, killall cron) para parar um processo.
Para parar um processo zombie, é necessário encerrar o processo pai executando `kill -9 ppid` (ppid indica o ID do processo pai, que pode ser consultado executando `ps -o ppid PID` (por exemplo, ps -o ppid 32535)). 

## 9. Como faço para localizar um processo zombie?

Você pode executar `top` para exibir o total de processos zombie e executar `ps -ef | grep defunct | grep -v grep` para localizar um processo zombie específico. 

## 10. Por que não consigo ativar a porta do servidor?

Você precisa verificar o sistema operacional e o aplicativo para garantir que uma porta esteja ativada.
Apenas o usuário `root` pode ativar portas abaixo de 1024 no sistema operacional Linux. Execute `sudo su -` para obter permissões de raiz antes de ativar a porta do servidor.
Para problemas em aplicativos, como conflitos de porta ou problemas de configuração, use os logs de inicialização do aplicativo para solucioná-los. O sistema do servidor Tencent usa a porta 36000. 

## 11. Quais são os comandos comumente usados para verificar o desempenho de um servidor Linux?
<table class="t">
<tbody><tr>
<th width="100"><b>Nome do comando</b>
</th><th> <b>Descrição</b>
</th></tr>
<tr>
<td>top
</td><td>top é um programa gerenciador de tarefas que monitora o desempenho geral do sistema.<br>
<p>Esse comando pode ser usado para exibir informações como a carga do sistema, o processo, a CPU, a memória e a paginação. Use `shift+m` e `shift+p` para classificar os processos por uso de memória e uso de CPU.
</p>
</td></tr>
<tr>
<td>vmstat
</td><td>vmstat é uma ferramenta de monitoramento de sistema de computador usada principalmente para memória virtual que coleta e exibe informações resumidas sobre a CPU, os processos, a paginação de memória e a E/S.<br>
<p>Por exemplo, vmstat 3 10 gera resultados a cada três segundos e é executado dez vezes.
</p>
</td></tr>
<tr>
<td>iostat
</td><td>iostat é uma ferramenta de monitoramento de sistema de computador que coleta e exibe estatísticas sobre a CPU e a E/S.<br>
<p>Por exemplo, iostat -dxmt 10 gera informações detalhadas sobre E/S em MB a cada dez segundos.
</p>
</td></tr>
<tr>
<td>df
</td><td>df é um comando usado para exibir a quantidade de espaço disponível em disco.<br>
<p>Por exemplo: df -m exibe o uso de espaço em disco em MB.
</p>
</td></tr>
<tr>
<td>lsof
</td><td>lsof relata uma lista de todos os arquivos abertos, o que é muito útil para o gerenciamento de sistemas Linux.<br>
<p>Por exemplo:<br>
lsof -i: 36000 exibe os processos usando a porta 36000.
<br>
lsof -u root exibe os programas executados por raiz.
<br>
lsof -c php-fpm exibe os arquivos abertos pelo processo php-fpm.
<br>
lsof php.ini exibe os processos para os quais o php.ini foi aberto.
</p>
</td></tr>
<tr>
<td>ps
</td><td>ps é um comando de consulta de processos que exibe informações relacionadas a eles.<br>
<p>As combinações de parâmetros de comando comumente usadas são `ps -ef` e `ps aux`. Use `ps -A -o` para gerar campos personalizados. <br>
Por exemplo:<br>
`ps -A -o pid,stat,uname,%cpu,%mem,rss,args,lstart,etime |sort -k6,6 -rn` gera resultados de acordo com os campos listados e os classifica usando o 6º campo.
<br>
`ps -A -o comm |sort -k1 |uniq -c|sort -k1 -rn|head` lista o processo com a maior quantidade de instâncias em execução.
</p>
</td></tr></tbody></table>

Outros comandos e arquivos comumente usados: `free -m`, `du`, `uptime`, `w`, `/proc/stat`, `/proc/cpuinfo` e `/proc/meminfo`. 

## 12. O que fazer quando o Cron não funcionar?
Siga as etapas abaixo para solucionar esse problema:
1. Verifique se o crontab está funcionando normalmente.
 1. Execute `crontab -e` para adicionar o item de teste a seguir.
```
 \*/1 \* \* \* \* /bin/date >> /tmp/crontest 2>&1 &
```
 2. Verifique o arquivo `/tmp/crontest`. 
Se houver algum problema, execute `ps aux|grep cron` para localizar o pid do cron, execute `kill -9 PID` para encerrar o processo do cron e, em seguida, execute `/etc/init.d/cron start` para reiniciar o cron. 
2. Verifique se o caminho do script na entrada do cron é um caminho absoluto.
3. Verifique se você usou a conta certa para executar o cron. Além disso, verifique se a conta está incluída em `/etc/cron.deny`.
4. Verifique a permissão de execução do script, o diretório do script e a permissão do arquivo de log.
5. Recomendamos que você execute o script em segundo plano, adicionando um "&" no final da entrada do script. Por exemplo, `\*/1 \* \* \* \* /bin/date >> /tmp/crontest 2>&1 &`.

## 13. Como faço para configurar uma tarefa de inicialização para minha instância do CVM?

A sequência de inicialização do kernel do Linux é a seguinte:
1. Inicie o processo `/sbin/init`.
2. Em seguida, execute os scripts iniciais do init.
3. Execute o script de nível `/etc/rc.d/rc\*.d`, em que o valor de \* significa o modo de execução, que pode ser consultado em `/etc/inittab`.
4. Execute `/etc/rc.d/rc.local`.

>? A tarefa de inicialização pode ser configurada em `/etc/rc.d/rc.local` ou no arquivo `S\*\*rclocal` em `/etc/rc.d/rc\*.d`. 

## 14. Por que o disco do servidor é somente leitura?

Os motivos comuns para um disco de servidor somente leitura são os seguintes:
- O espaço em disco está cheio
Você pode executar `df -m` para verificar o uso do disco e, em seguida, excluir arquivos desnecessários para liberar espaço em disco. (Não recomendamos que você exclua arquivos que não sejam de terceiros. Verifique os arquivos antes de excluí-los). 
- Os recursos do inode do disco estão todos ocupados
Você pode executar `df -i` para exibir e confirmar processos relevantes. 
- Há uma falha de hardware

Se nenhuma das opções acima funcionar, ligue para a linha principal ou envie um tíquete. 

## 15. Como posso exibir os logs do sistema Linux?

- O caminho de armazenamento para arquivos de log em nível de sistema é `/var/log`.
- O log do sistema comumente usado é `/var/log/messages`.

## 16. Como encontro arquivos grandes no sistema de arquivos?

Você pode encontrá-los seguindo as etapas abaixo:
1. Execute `df` para consultar o uso da partição do disco (por exemplo, `df -m`).
2. Execute `du` para consultar o tamanho de uma pasta específica (por exemplo, `du -sh ./\*`, `du -h --max-depth=1|head -10`).
3. Execute `ls` para listar os arquivos e tamanhos de arquivo (por exemplo, `ls -lSh`).
Você também pode verificar diretamente o tamanho dos arquivos em um diretório específico usando o comando `find` (por exemplo, `find / -type f -size +10M -exec ls -lrt {} \`).

## 17. Como faço para verificar a versão do sistema operacional de um servidor?

Você pode executar os seguintes comandos para verificar a versão do sistema operacional de um servidor:
- uname -a
- cat /proc/version
- cat /etc/issue 

## 18. Por que os caracteres chineses são exibidos como código ininteligível no terminal Linux?

O próprio servidor não impõe restrições ao idioma de exibição. Portanto, é mais provável que seja um problema do cliente. Se você estiver usando secureCRT, tente alterar as configurações em **Options (Opções)** -> **Session Options (Opções de sessão)** -> **Appearance (Aparência)**. Se você estiver usando outro software de terminal, pesquise soluções no Google.
Se este problema aparecer em um shell Linux puro, execute `export` para verificar as variáveis de ambiente do usuário, como LANG e LC_CTYPE.

## 19. Como configuro um tempo limite de conexão usando o SecureCRT?

Você pode definir as seguintes configurações para que a conexão à sua instância do CVM permaneça estável ao se conectar ao CVM pelo SecureCRT:
1. Abra o SecureCRT e selecione **Options (Opções)**.
2. Selecione **Session Options (Opções de sessão)** e clique em **Terminal**.
3. Selecione **Send protocol NO-OP (Enviar protocolo NO-OP)** na caixa **Anti-idle (Anti-inatividade)** à direita e defina o tempo como "every 120 seconds (a cada 120 segundos)". 

## 20. Por que o espaço em disco em um servidor Linux não é liberado depois que um arquivo é excluído?

**Causa:**

Após fazer login em sua instância do CVM do Linux e excluir um arquivo usando `rm`, você notará que o espaço em disco disponível não aumenta quando você usa `df` para verificar o espaço em disco. Isso ocorre porque, quando o arquivo é excluído, se outro processo o estiver acessando, o espaço ocupado pelo arquivo excluído não será liberado imediatamente no momento em que você verificar o espaço em disco.

**Solução:**

1. Execute `lsof |grep deleted` usando a permissão de raiz e encontre o PID do processo que está usando o arquivo excluído.
2. Encerre o processo usando `kill -9 PID`. 


## 21. Como excluo arquivos em um servidor Linux?
Você pode executar `rm` para excluir arquivos. Os arquivos excluídos com esse comando não podem ser recuperados. Portanto, use-o com cuidado.
Formato de `rm`: `rm (option) (parameter)`.
- Opções:
**-d**: exclui todos os dados conectados diretamente e contidos no diretório a ser excluído e, em seguida, exclui o próprio diretório.
**-f**: exclui à força um arquivo ou diretório.
**-i**: pergunta ao usuário antes de excluir um arquivo ou diretório existente.
**-r** ou **-R**: exclui todos os arquivos e subdiretórios em um diretório específico usando o processamento recursivo.
**--preserve-root**: não implementa operações recursivas no diretório raiz.
**-v**: exibe os processos de execução detalhados dos comandos.
- Parameter (Parâmetro): especifica o arquivo ou lista de arquivos a ser excluído. Se o parâmetro contém um diretório, adicione a opção `-r` ou `-R`.
- Exemplo:
	- Execute `rm test.txt` para excluir o arquivo `test.txt`.
	- Execute `rm -r test` para excluir o diretório `test`.
	- Execute `rm -r *` para excluir todos os arquivos e subdiretórios do diretório atual.
