## Visão geral
Atualmente, o CentOS 8 nativo não permite a configuração do serviço NTP. Em vez disso, é necessário usar o chronyd para fornecer um tempo preciso. Este documento descreve como instalar e configurar o chronyd em uma instância do CVM do Tencent Cloud baseada no CentOS 8.

## Instruções
### Instalação e configuração do serviço chronyd
1. [Faça login em uma instância do Linux usando o método de login padrão](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute o comando a seguir para instalar o serviço chronyd.
```
yum -y install chrony
```
3. Execute o comando a seguir para modificar o arquivo de configuração `chrony.conf`.
```
vim /etc/chrony.conf
```
4. Pressione **i** para acessar o modo de edição e insira o conteúdo a seguir na linha posterior à `#log measurements statistics tracking`.
```
server time1.tencentyun.com iburst
server time2.tencentyun.com iburst
server time3.tencentyun.com iburst
server time4.tencentyun.com iburst
server time5.tencentyun.com iburst
```
O resultado deve ser o seguinte:
![](https://main.qcloudimg.com/raw/578e072599f8d50ea188d3911a9d76c7.png)
5. Pressione **Esc** e digite **:wq** para salvar e fechar o arquivo.
6. Execute os comandos a seguir em sequência para ativar a inicialização automática do chronyd e reiniciá-lo.
```
systemctl restart chronyd
```
```
systemctl enable chronyd
```

### Verificação das configurações
1. Execute o comando a seguir para verificar se o relógio está sincronizado.
```
date
```
2. Execute o comando a seguir para verificar o status da fonte do relógio.
```
chronyc sourcestats -v
```
Se um resultado semelhante ao seguinte for retornado, a configuração obteve êxito.
![](https://main.qcloudimg.com/raw/6a5f584638de922f5e80b5b138541c9e.png)

## Apêndice
### Comandos
<table>
<tr>
<th>Comando</th><th>Descrição</th>
</tr>
<tr>
<td>
<code>chronyc sources -v</code>
</td>
<td>Verifica a fonte do relógio.</td>
</tr>
<tr>
<td>
<code>chronyc sourcestats -v</code>
</td>
<td>Verifica o status da fonte do relógio.</td>
</tr>
<tr>
<td>
<code>timedatectl set-local-rtc 1</code>
</td>
<td>Configura o relógio em tempo real. O formato padrão é UTC.
</td>
</tr>
<tr>
<td>
<code>timedatectl set-ntp yes</code>
</td>
<td>Ativa o serviço NTP para sincronização.</td>
</tr>
<tr>
<td>
<code>chronyc tracking</code>
</td>
<td>Calibra o servidor NTP.</td>
</tr>
<tr>
<td>
<code>chronyc -a makestep</code>
</td>
<td>Força a sincronização do relógio do sistema.</td>
</tr>
</table>
