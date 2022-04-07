## Descrição do erro
O erro “Account locked due to XXX failed logins (Conta bloqueada devido a XXX logins com falha)” aparece antes de inserir a senha de login.
![](https://main.qcloudimg.com/raw/0dcc0c3b62a36ba0f269e629a3365564.png)

## Possíveis causas
Este problema pode ser causado pela configuração do `pam_tally2.so` no arquivo `/etc/pam.d/login`. Para fazer o login pelo VNC, o `/etc/pam.d/login` é utilizado na autenticação, já o `pam_tally2.so` assinala para bloquear temporariamente ou permanentemente a conta do usuário após a quantidade especificada de logins consecutivos com falha. Quando uma conta é bloqueada permanentemente, você precisa desbloqueá-la manualmente.

A conta de login será bloqueada quando a quantidade de logins consecutivos com falha exceder o valor configurado. Observe que a conta também pode ser bloqueada por quaisquer procedimentos forçados.
![](https://main.qcloudimg.com/raw/806c1d8ccded0746f5457320df479177.png)
Confira abaixo os parâmetros do módulo `pam_tally2`.
<table>
<tr>
<th>Parâmetro</th><th>Descrição</th>
</tr>
<tr>
<td><code>deny=n</code></td>
<td>Bloqueia a conta se a quantidade de logins consecutivos com falha for maior que <code>n</code>.</td>
</tr>
<tr>
<td><code>lock_time=n </code></td>
<td>Bloqueia a conta por <code>n</code> segundos quando a quantidade de logins consecutivos com falha exceder o limite</td>
</tr>
<tr>
<td><code>un lock_time=n</code></td>
<td>Desbloqueia a conta automaticamente após <code>n</code> depois</td>
</tr>
<tr>
<td><code>no_lock_time </code></td>
<td>Não usa o campo <code>.fail_locktime</code> no <code>/var/log/faillog</code></td>
</tr>
<tr>
<td><code>magic_root   </code></td>
<td>Se o módulo é executado por um usuário raiz (uid=0), o contador não é incrementado.</td>
</tr>
<tr>
<td><code>even_deny_root </code></td>
<td>O usuário raiz será bloqueado após <code>deny=n</code> logins com falha consecutivos.</td>
</tr>
<tr>
<td><code>root_unlock_time=n  </code></td>
<td>Esse parâmetro é obrigatório se <code>even_deny_root</code> estiver configurado. Ele indica por quanto tempo o usuário raiz permanece bloqueado quando a quantidade de logins consecutivos com falha excede o limite. </td>
</tr>
</table>

## Soluções
1. Consulte o [procedimento de solução de problemas](#ProcessingSteps), para acessar o arquivo de configuração de login e converter temporariamente a configuração do módulo `pam_limits.so`em comentário.
2. Descubra o motivo pelo qual sua conta está bloqueada e melhore sua política de segurança.

[](id:ProcessingSteps)

## Procedimento de solução de problemas

1. Tente [fazer login no CVM do Linux usando uma chave SSH](https://intl.cloud.tencent.com/document/product/213/32501).
	- Se o login for bem-sucedido, siga para a próxima etapa.
	- Se o login falhar, tente o modo de usuário único.
2. Execute o comando a seguir para exibir os logs.
```
vim /var/log/secure
```
Este arquivo registra as informações de segurança, principalmente os logs de login do CVM. Você pode verificar os logs de erros de `pam_tally2` como mostrado abaixo.
![](https://main.qcloudimg.com/raw/f45fb4564cfea44f0210a6e9b7124b73.png)
3. Execute os comandos a seguir em sequência para abrir o diretório `/etc/pam.d` e procurar `pam_tally2`.
```
cd /etc/pam.d
```
```
find . | xargs grep -ri "pam_tally2" -l
```
Se um resultado semelhante à figura abaixo for retornado, `pam_tally2` está incluído no arquivo `login`.
![](https://main.qcloudimg.com/raw/a5d272e11a88d4f9cee347244fb98441.png)
4. Execute o comando a seguir para converter as configurações `pam_tally2.so` em comentário temporariamente. Em seguida, faça o login normalmente.
```
sed -i "s/.*pam_tally.*/#&/" /etc/pam.d/login
```
5. Verifique se a conta está bloqueada devido a operações incorretas ou procedimentos forçados. Em último caso, recomenda-se fortalecer a política de segurança de acordo com os procedimentos abaixo:
 - Altere a senha do CVM para uma senha mais forte contendo de 12 a 16 caracteres, incluindo letras maiúsculas, letras minúsculas, caracteres especiais e números. Para mais informações, consulte a seção [Redefinição da senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).
 - Exclua as contas obsoletas de login do CVM.
 - Altere a porta ssh padrão 22 para uma porta menos comum entre 1024-65525. Para mais informações, consulte a seção [Modificação da porta remota padrão de um CVM](https://intl.cloud.tencent.com/document/product/213/35376).
 - Gerencie as regras do grupo de segurança associado para abrir apenas as portas e os protocolos necessários para a sua empresa. Para mais informações, consulte [Adição de regras de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272).
 - Feche a porta de acesso à Internet para os principais aplicativos, como os bancos de dados MySQL e Redis. 
 - Instale um software de segurança (como o agente CWP), e configure alarmes em tempo real para receber avisos sobre logins suspeitos.


