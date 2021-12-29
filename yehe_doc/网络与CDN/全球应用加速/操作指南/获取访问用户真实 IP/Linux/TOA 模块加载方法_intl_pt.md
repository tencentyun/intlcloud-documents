Baixe e descompacte o pacote do TOA correspondente à versão do sistema operacional Linux no Tencent Cloud:
- **arm64**
	- [kernel-4.18.0 ](https://gaap-1251337138.file.myqcloud.com/kernel-4.18.0.rar)
- **centos**
	- [CentOS 6.5 64](https://gaap-1251337138.file.myqcloud.com/CentOS%206.5%2064.rar)
	- [CentOS 7.2 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.2%2064.rar)
	- [CentOS 7.3 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.3%2064.rar)
	- [CentOS 7.4 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.4%2064.rar)
	- [CentOS 7.5 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.5%2064.rar)
	- [CentOS 7.6 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.6%2064.rar)
	- [CentOS 7.7 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.7%2064.rar)
	- [CentOS 7.8 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.8%2064.rar)
	- [CentOS 7.9 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.9%2064.rar)
	- [CentOS 8.0 64](https://gaap-1251337138.file.myqcloud.com/CentOS%208.0%2064.rar)
	- [CentOS 8.2 64](https://gaap-1251337138.file.myqcloud.com/CentOS%208.2%2064.rar)
- **debian**
	- [Debian 8.2 64](https://gaap-1251337138.file.myqcloud.com/Debian%208.2%2064.rar)
	- [Debian 9.0 64](https://gaap-1251337138.file.myqcloud.com/Debian%209.0%2064.rar)
	- [Debian 10.2 64](https://gaap-1251337138.file.myqcloud.com/Debian%2010.2%2064.rar)
- **suse linux**
	- [SUSE Linux Enterprise Server 11 SP3 64](http://toamodule-1253438722.file.myqcloud.com/SUSE%20Linux%20Enterprise%20Server%2011%20SP3%2064.zip)
	- [SUSE Linux Enterprise Server 12 64](http://toamodule-1253438722.file.myqcloud.com/SUSE%20Linux%20Enterprise%20Server%2012%2064.zip)
	- [SUSE Linux Enterprise Server 12 SP3 64](https://gaap-1251337138.file.myqcloud.com/SUSE%20Linux%20Enterprise%20Server%2012%20SP3%2064%E4%BD%8D.rar)
- **ubuntu**
	- [Ubuntu Server 14.04.1 LTS 64](https://gaap-1251337138.file.myqcloud.com/Ubuntu%20Server%2014.04.1%20LTS%2064.rar)
	- [Ubuntu Server 16.04.1 LTS 64](https://gaap-1251337138.file.myqcloud.com/Ubuntu%20Server%2016.04.1%20LTS%2064.rar)
	- [Ubuntu Server 18.04.1 LTS 64](https://gaap-1251337138.file.myqcloud.com/Ubuntu%20Server%2018.04.1%20LTS%2064.rar)
	- [Ubuntu Server 20.04.1 LTS 64](https://gaap-1251337138.file.myqcloud.com/Ubuntu%20Server%2020.04.1%20LTS%2064.rar)




1. Depois que a descompactação for concluída, execute o comando `cd` para acessar a pasta descompactada e execute o comando de carregamento do módulo:
```
insmod toa.ko
```
2. Execute o seguinte comando para verificar se o carregamento obteve êxito:
```
lsmod | grep toa
```
3. Se sim, carregue o arquivo `toa.ko` no script de inicialização (o arquivo `toa.ko` precisará ser carregado novamente se o servidor tiver sido reiniciado).

Se você não conseguir encontrar um pacote de instalação correspondente à sua versão do sistema operacional na lista acima, baixe e compile o pacote de origem da versão geral para o sistema operacional Linux. Esta versão é compatível com a maioria das distribuições Linux, como CentOS 6.9, CentOS 7 e Ubuntu 14.04.
1. Obtenha o pacote de origem.
	- Pacote de origem para CentOS 7 e versões posteriores
```
wget "http://thunder-pro-mainland-1258348367.cos.ap-guangzhou.myqcloud.com/gaap-toa%E6%BA%90%E7%A0%81(centos7%E4%BB%A5%E4%B8%8A).zip"
```
	- Pacote de origem para versões anteriores ao CentOS 7
```
wget "http://thunder-pro-mainland-1258348367.cos.ap-guangzhou.myqcloud.com/gaap-toa%E6%BA%90%E7%A0%81(centos7%E4%BB%A5%E4%B8%8B).zip"
```
2. Compile o pacote de origem para gerar o arquivo do módulo TOA.
```
yum install gcc
yum install kernel-headers
yum install kernel-devel
unzip gaap-toa*.zip //Decompress the source package above
cd gaap-toa* //Access the corresponding directory
make
```
3. Carregue o arquivo do módulo TOA.
```
mv toa.ko /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
insmod /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
```

Se um erro de compilação for relatado, ele pode ter sido causado pela inconsistência entre a versão do kernel instalada e a versão `uname -r` exibida. No diretório `/lib/modules/`, verifique a versão do kernel de fato instalada, modifique o `uname -r` no `Makefile` para a versão atual do kernel e compile o arquivo novamente.
