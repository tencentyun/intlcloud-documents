## Descrição do problema
Assim que um CVM com o sistema operacional CentOS 6.x é reiniciado ou executa o comando `service network restart`, seus nomes de domínio não podem ser definidos. Além disso, as informações de DNS no arquivo de configuração `/etc/resolv.conf` foram limpas.

## Possíveis causas
No sistema operacional CentOS 6.x, os scripts de inicialização (initscripts) com versões anteriores a 9.03.49-1 apresentam um defeito devido a diferentes versões do grep.

## Solução
Atualize os scripts de inicialização para a versão mais recente e gere as informações de DNS novamente.

## Instruções
1. Faça login no CVM.
2. Execute o comando a seguir para consultar a versão dos scripts de inicialização, e confirme se existe algum erro caso a versão dos scripts seja anterior à 9.03.49-1.
```
rpm -q initscripts
```
Você receberá a seguinte mensagem abaixo:
```
initscripts-9.03.40-2.e16.centos.x86_64
```
De acordo com o exemplo acima, a versão dos scripts de inicialização do initscripts-9.03.40-2 é mais antiga do que a versão initscripts-9.03.49-1 que apresentou falhas. Existe o risco de perda das informações de DNS.
3. Execute o comando a seguir para atualizar os scripts de inicialização para a versão mais recente e gerar as informações de DNS novamente.
```
yum makecache
yum -y update initscripts
service network restart
```
4. Após concluir a atualização, execute o comando a seguir para verificar os dados de versão dos scripts de inicialização, e confirmar se a atualização foi bem-sucedida.
```
rpm -q initscripts
```
Você receberá a seguinte mensagem abaixo:
```
initscripts-9.03.58-1.el6.centos.2.x86_64
```
Conforme mostrado acima, a versão vigente é diferente da anterior e é mais recente que o initscripts-9.03.49-1. Isso demonstra que os scripts de inicialização foram atualizados.
