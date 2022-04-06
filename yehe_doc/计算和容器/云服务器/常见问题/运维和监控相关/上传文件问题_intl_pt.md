### A CVM vem com o FTP?
Sim. Você pode instalar e configurar o FTP conforme necessário.
- Para criar sites FTP usando o serviço FTP integrado do Windows, consulte [Implantação do serviço FTP (Windows)](https://intl.cloud.tencent.com/document/product/213/10414).
- Para criar sites FTP usando o software vsftpd, consulte [Implantação do serviço FTP (Linux)](https://intl.cloud.tencent.com/document/product/213/10912).

### Como faço para carregar arquivos em uma CVM do Windows?
- Para um Windows local, consulte [Upload de arquivos do Windows para uma CVM do Windows usando MSTSC](https://intl.cloud.tencent.com/document/product/213/2761).
- Para um Linux local, consulte [Upload de arquivos do Linux para uma CVM do Windows usando RDP](https://intl.cloud.tencent.com/document/product/213/34822).
- Para um MacOS local, consulte [Upload de arquivos do MacOS para uma CVM do Windows usando MRD](https://intl.cloud.tencent.com/document/product/213/34820).

### Como um host local transfere os dados de e para uma CVM do Windows?
### Para transferir dados:
- Se você usar o arquivo RDP para fazer login em uma CVM do Windows a partir de um computador Windows local, poderá arrastar e carregar os arquivos locais diretamente na CVM.
- Faça o [upload de arquivos do Windows para uma CVM do Windows usando MSTSC](https://intl.cloud.tencent.com/document/product/213/2761)
- [Configure o serviço FTP (Linux)](https://intl.cloud.tencent.com/document/product/213/10912) no host local.

### Como faço para carregar arquivos para uma CVM do Linux usando o WinSCP?
Para mais informações, consulte [Upload de arquivos via WinSCP para uma CVM do Linux a partir do Windows](https://intl.cloud.tencent.com/document/product/213/2131).

### Como faço para carregar ou baixar arquivos de uma CVM do Linux?
Para mais informações, consulte [Upload de arquivos via SCP para uma CVM do Linux a partir do Linux](https://intl.cloud.tencent.com/document/product/213/2133).

### O que devo fazer se a conexão cliente-servidor expirar durante o upload do arquivo FTP?
O firewall do servidor ou o grupo de segurança pode ter bloqueado a conexão. Siga as etapas abaixo para solucionar esse problema:
1. Verifique as configurações de firewall do servidor.
2. Desative o firewall ou adicione regras.
