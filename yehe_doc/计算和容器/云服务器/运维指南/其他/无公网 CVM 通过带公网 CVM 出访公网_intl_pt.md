## Visão geral
Se você selecionar uma largura de banda com um limite superior de 0 Mbps ao adquirir um CVM, ele não poderá acessar a rede pública. Este documento usa o CentOS 7.5 como exemplo para descrever como um CVM sem um endereço IP público pode acessar a rede pública conectando-se a um CVM com um endereço IP público por meio de uma VPN do PPTP.


## Pré-requisitos
- Dois CVMs na mesma instância do VPC foram criados. Um **CVM não possui endereço IP público** e o outro **CVM possui endereço IP público**.
- O endereço IP privado do CVM com um endereço IP público foi obtido.

## Instruções
### Configuração do PPTP no CVM com um endereço IP público

1. Faça login no CVM com um endereço IP público.
2. Execute o seguinte comando para instalar o PPTP:
```
yum install -y pptpd
```
3. Execute o seguinte comando para abrir o arquivo de configuração `pptpd.conf`:
```
vim /etc/pptpd.conf
```
4. Pressione **i** para mudar para o modo de edição e adicione o código a seguir na parte inferior do arquivo.
```
localip 192.168.0.1
remoteip 192.168.0.234-238,192.168.0.245
```
5. Pressione **Esc**, digite **:wq** e salve e feche o arquivo.
6. Execute o seguinte comando para abrir o arquivo de configuração `/etc/ppp/chap-secrets`:
```
vim /etc/ppp/chap-secrets
```
7. <span id="step7">Pressione **i** para mudar para o modo de edição e adicione o nome de usuário e a senha para se conectar ao PPTP no formato a seguir na parte inferior do arquivo.</span>
```
<Username>    pptpd    <Password>    *
```
Por exemplo, se o nome de usuário e a senha para se conectar ao PPTP forem root e 123456 respectivamente, adicione o seguinte código:
```
root    pptpd    123456    *
```
8. Pressione **Esc**, digite **:wq** e salve e feche o arquivo.
9. Execute o seguinte comando para iniciar o serviço do PPTP:
```
systemctl start pptpd
```
10. Execute os seguintes comandos sequencialmente para ativar o encaminhamento:
```
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -t nat -A POSTROUTING -o eth0 -s 192.168.0.0/24 -j MASQUERADE
```

### Configuração do PPTP no CVM sem um endereço IP público

1. Faça login no CVM sem um endereço IP público.
2. Execute o seguinte comando para instalar um cliente do PPTP:
```
yum install -y pptp pptp-setup
``` 
3. Execute o seguinte comando para criar um arquivo de configuração:
```
pptpsetup --create <Configuration file name> --server <Private IP address of the CVM with a public IP address> --username <Username for connecting to PPTP> --password <Password for connecting to PPTP> --encrypt
```
Por exemplo, se você obteve o endereço IP privado 10.100.100.1 do CVM com um endereço IP público, execute o seguinte comando para criar um arquivo de configuração de teste:
```
pptpsetup --create test --server 10.100.100.1 --username root --password 123456 --encrypt
```
4. Execute o seguinte comando para se conectar ao PPTP:
```
pppd call test (o nome de arquivo de configuração criado na etapa 3)
```
5. Execute os seguintes comandos para definir rotas:
```
route add -net 10.0.0.0/8 dev eth0
route add -net 172.16.0.0/12 dev eth0
route add -net 192.168.0.0/16 dev eth0
route add -net 169.254.0.0/16 dev eth0
route add -net 9.0.0.0/8 dev eth0
route add -net 100.64.0.0/10 dev eth0
route add -net 0.0.0.0 dev ppp0
```

### Verificação do êxito da configuração
Execute o seguinte comando no CVM sem um endereço IP público para fazer ping em qualquer endereço de rede externa e verifique se pode ser feito ping nele por meio de:
```
ping -c 4 <External network address>
```
Se um resultado semelhante ao seguinte for retornado, a configuração obteve êxito:
![](https://main.qcloudimg.com/raw/c841782ce0976982d1f289d3437ec0ed.png)



