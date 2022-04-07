## Descrição do erro
A mensagem de erro “Permission denied (Permissão negada)” é exibida quando eu faço login usando o VNC ou a chave SSH.
- O erro de login do VNC é mostrado abaixo:
![](https://main.qcloudimg.com/raw/5f1aedd75b6d99cddab4d83fa82d964f.png)
- O erro de login do SSH é mostrado abaixo:
![](https://main.qcloudimg.com/raw/7ab31fbb82391da2c8ae28e8ad3b961f.png)

## Possíveis causas
Usar o login por VNC ou SSH chamará `system-auth` para autenticação se este módulo estiver configurado no arquivo de configuração `/etc/pam.d/login`. Por padrão, o módulo `system-auth` introduz o módulo `pam_limits.so`. A configuração padrão do `system-auth` é mostrada abaixo:
![](https://main.qcloudimg.com/raw/e32db00ec665388bc4c7cb0454fd6fab.png)
O módulo `pam_limits.so` é usado principalmente para limitar o uso de recursos do sistema durante a sessão do usuário. O seu arquivo de configuração padrão `/etc/security/limits.conf` especifica a quantidade máxima de arquivos, a quantidade máxima de threads, a memória máxima e outros recursos que um usuário pode usar. Consulte a tabela abaixo para mais detalhes.
<table>
<tr>
<th style="width:20%">Parâmetro</th><th>Descrição</th>
</tr>
<tr>
<td><code>soft nofile</code></td>
<td>A quantidade máxima de descritores de arquivos abertos (limite flexível)</td>
</tr>
<tr>
<td><code> hard nofile</code></td>
<td>A quantidade máxima de descritores de arquivos abertos (limite rígido), que não pode ser excedida.</td>
</tr>
<tr>
<td><code>fs.file-max </code></td>
<td>A quantidade máxima de identificadores de arquivos abertos (arquivo struct no kernel) no nível do sistema.</td>
</tr>
<tr>
<td><code>fs.nr_open</code></td>
<td>A quantidade máxima de descritores de arquivo (fd) atribuídos a um processo</td>
</tr>
</table> 

A falha de login pode ser causada por configurações incorretas da quantidade máxima de descritores de arquivos abertos para a conta raiz no arquivo de configuração `/etc/security/limits.conf`. O valor definido de `soft nofile` não deve ser maior que `hard nofile`, e `hard nofile` não deve ser maior que `fs.nr_open`.


## Soluções
Realize o [procedimento de solução de problemas](#ProcessingSteps) para corrigir as configurações de relação de `soft nofile`, `hard nofile` e `fs.nr_open`.

[](id:ProcessingSteps)

## Procedimento de solução de problemas

1. Tente [fazer login no CVM do Linux usando uma chave SSH](https://intl.cloud.tencent.com/document/product/213/32501).
	- Se o login for bem-sucedido, vá para a próxima etapa.
	- Se o login falhar, use o modo de usuário único. Para mais informações, consulte a seção [Inicialização no modo de usuário único do Linux](https://intl.cloud.tencent.com/document/product/213/34819).
2. Verifique se os valores definidos atendem à relação `soft nofile ≤ hard nofile ≤ fs.nr_open`.
 - Execute o comando a seguir para obter os valores de `soft nofile` e `hard nofile`.
```
/etc/security/limits.conf
```
Neste exemplo, seus valores são 3000001 e 3000002 respectivamente, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/3bc035efb6cf46f70b30017dbefe831a.png)
 - Execute o comando a seguir para verificar o valor de `fs.nr_open`.
```
sysctl -a 2>/dev/null | grep -Ei "file-max|nr_open"
```
Neste exemplo, seu valor é 1048576, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/0fee5e2cda62d6a558cf808652a6b9dd.png)
3. Edite o arquivo `/etc/security/limits.conf` para adicionar ou modificar as configurações a seguir no final do arquivo. 
 - `root soft nofile`: 100001
 - `root hard nofile`: 100002
4. Edite o arquivo `/etc/sysctl.conf` para adicionar ou modificar as configurações a seguir no final do arquivo.
>?Esta etapa é opcional quando a relação `soft nofile ≤ hard nofile ≤ fs.nr_open` é atendida. Realize essa etapa para aumentar o limite do sistema.
>
 - `fs.file-max` = 2000000
 - `fs.nr_open` = 2000000
5. Execute o comando a seguir para que a configuração entre em vigor. Em seguida, faça o login normalmente.
```
sysctl -p
```

