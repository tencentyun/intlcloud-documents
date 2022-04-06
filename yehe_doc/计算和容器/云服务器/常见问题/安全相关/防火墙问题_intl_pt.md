### Como devo configurar o software de firewall iptables em um sistema operacional Linux?
> **Observações:**
> O iptables varia muito entre as versões anteriores e posteriores ao CentOS 7.
> - Nas versões anteriores ao CentOS 7, o serviço iptables é usado como firewall por padrão. Após executar o comando `service iptables stop`, o serviço iptables primeiro limpará as regras e então descarregará o módulo iptables. Quando o serviço iptables for reiniciado, ele carregará as regras do arquivo de configuração. Você pode parar o serviço iptables para testar se as restrições do firewall foram aplicadas.
>[](https://main.qcloudimg.com/raw/4a404e0187b0ee677034c0df82468e4a.png)
> - Nas versões posteriores ao CentOS 7, o serviço de firewall é usado como firewall por padrão, e o módulo iptables_filter é carregado para garantir a compatibilidade. Você pode usar o comando iptables para adicionar regras. No entanto, o serviço iptables fica desativado por padrão. Após confirmar que o módulo iptable_filter foi carregado, as regras entrarão em vigor.

Para definir o firewall, execute `iptables -nvL` para exibir as regras. 
Os dois cenários a seguir descrevem como configurar o programa de software de firewall iptables. 
#### Cenário 1
Em um sistema operacional Ubuntu 14, o grupo de segurança e a porta de listening (estado de espera) estão ativos, mas a conexão do Telnet falha.
Regras de entrada do grupo de segurança:
![](https://main.qcloudimg.com/raw/4a6a1c7eca94a76ddbce457dbe28affa.png)
Regras de saída do grupo de segurança:
![](https://main.qcloudimg.com/raw/90914e729ba27a6a9253e719bf4a9703.png)
Falha de conexão do Telnet:
![](https://main.qcloudimg.com/raw/74c521a97d4b9dab64b85ce62ab2cf86.png)
#### Solução
1. Capture os pacotes na CVM para verificar se eles foram enviados à CVM.
 - Se não tiverem sido enviados, os pacotes podem ter sido bloqueados pelo grupo de segurança, pelo TGW superior ou pelo ISP.
 - Se tiverem sido enviados, mas a CVM não responde, esse problema pode ser causado pela política do iptables da CVM. Conforme mostrado na figura a seguir, a CVM não gera os pacotes TCP para 64.11 depois que a conexão do Telnet é estabelecida.
![](https://main.qcloudimg.com/raw/1052893022c8786a9b7b0166a57ce16d.png)  

2. Após confirmar que o problema é causado pela política do iptables, execute `iptables –nvL` para verificar se a política abriu a porta 8081. Neste exemplo, a porta 8081 está fechada. 
![](https://main.qcloudimg.com/raw/f214d470f1d40ed7061ea155de756bca.jpg) 
3. Execute o seguinte comando para abrir a porta 8081:
```
iptables -I INPUT 5 -p tcp  --dport 8081 -j ACCEPT
```
4. Verifique se a porta 8081 está aberta. Se estiver, o problema foi resolvido.  


#### Cenário 2
Com base na configuração do iptables, a política foi ativada, mas ainda não é possível executar ping do servidor de destino.
![](https://main.qcloudimg.com/raw/46fdf4e20187c5b366c7773d73eb1cee.png)
#### Solução
Se as informações mostradas abaixo forem exibidas,
![](https://main.qcloudimg.com/raw/babfa7fcfe9dd7536ba011c3fbaab7bc.jpg)
execute o seguinte comando para excluir a primeira regra de saída:
```
iptabels –D OUTPUT 1
```
Teste para verificar se o problema foi resolvido.

### Como remover um firewall?
#### Instâncias do Windows:
1. Após fazer login na instância, selecione **Start (Iniciar)** > **Control Panel (Painel de Controle)** > **Firewall Settings (Configurações do Firewall)**, para acessar a página “Firewall Settings (Configurações do Firewall)”.

2. Verifique se o firewall e outros softwares de segurança, como o safedog, foram ativados. Se sim, desative-os.

#### Instâncias do Linux:
1. Execute o comando a seguir para verificar se a política de firewall foi ativada. Se não tiver sido ativada, pule a etapa 2 e vá para a etapa 3.
```
iptables -vnL
```

2. Se a política de firewall foi ativada, execute o seguinte comando para fazer backup da política de firewall:
```
iptables-save
```

3. Execute o seguinte comando para limpar a política de firewall:
```
iptables -F
```

### O firewall interceptará uma CVM que não é do CDN da Tencent Cloud?
Não. Se estiver preocupado que o firewall possa atrapalhar os negócios, você pode desativá-lo.
