## Visão geral

Este documento descreve como instalar o Cloudbase-Init no sistema operacional Windows Server 2012 R2 de 64 bits.

<span id="PreparationSoftware"></span>
## Software necessário
A tabela a seguir descreve o software necessário para instalar o Cloudbase-Init.

| Software | Link para download | Descrição |
|---------|---------|---------|
| CloudbaseInitSetup_X_X_XX_xXX.msi | Baixe o pacote de instalação do Cloudbase-Init de acordo com o sistema operacional usado.<ul style="margin: 0;"><li>Versão estável (recomendada)<ul style="margin: 0;"><li>Sistema operacional Windows de 64 bits: [Clique aqui](https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x64.msi) para baixar o pacote de instalação.</li><li>Sistema operacional Windows de 32 bits: [Clique aqui](https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x86.msi) para baixar o pacote de instalação.</li></ul></li><li>Versão beta</li></ul>Para obter detalhes, consulte o [site oficial do Cloudbase-Init](http://www.cloudbase.it/cloud-init-for-windows-instances/). | Usado para instalar o Cloudbase-Init |
| TencentCloudRun.ps1 | [Clique aqui](https://cloudinit-1251783334.cosgz.myqcloud.com/TencentCloudRun.ps1) para baixar o pacote de instalação. | - |
| localscripts.py | [Clique aqui](https://cloudinit-1251783334.file.myqcloud.com/localscripts.py) para baixar o pacote de instalação. | Usado para garantir que o Cloudbase-Init seja iniciado corretamente |

## Instruções

### Instalação do Cloudbase-Init

1. Na área de trabalho, clique duas vezes no pacote de instalação do Cloudbase-Init.
2. Na caixa de diálogo, clique em **Run (Executar)** para entrar no assistente de configuração do Cloudbase-Init, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/3249309f71fccaf73feeaa5bb55301c3.png)
3. Clique em **Next (Avançar)**.
4. Marque **I accept the terms in the License Agreement (Aceito os termos do Contrato de Licença)** e clique em **Next (Avançar)** para as duas operações a seguir.
5. Na página **Configuration options (Opções de configuração)**, defina a **Serial port for logging (Porta serial para registrar em log)** para **COM1**, selecione **Run Cloudbase-Init service as LocalSystem (Executar o serviço Cloudbase-Init como LocalSystem)** e clique em **Next (Avançar)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/a772c35958cdf3be511dab58f730e7be.png)
6. Clique em **Install (Instalar)**.
7. Quando a instalação for concluída, clique em **Finish (Concluir)** para fechar o assistente de configuração do Cloudbase-Init, conforme mostrado abaixo:
>! Ao fechar o assistente de configuração do Cloudbase-Init, não marque nenhuma caixa de seleção nem execute o Sysprep.
>
![](https://main.qcloudimg.com/raw/d2d6c30def7812af9d7e484f5e8ccaa9.png)

### Modificação do arquivo de configuração do Cloudbase-Init 

1. Abra o arquivo de configuração `cloudbase-init.conf`.
O arquivo de configuração `cloudbase-init.conf` fica salvo em `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf` por padrão. 
2. Substitua o conteúdo no arquivo de configuração `cloudbase-init.conf` pelo seguinte:
```
[DEFAULT]
username=Administrator
groups=Administrators
inject_user_password=true
config_drive_raw_hhd=true
config_drive_cdrom=true
config_drive_vfat=true
bsdtar_path=C:\Program Files\Cloudbase Solutions\Cloudbase-Init\bin\bsdtar.exe
mtools_path=C:\Program Files\Cloudbase Solutions\Cloudbase-Init\bin\
metadata_services=cloudbaseinit.metadata.services.configdrive.ConfigDriveService
plugins=cloudbaseinit.plugins.windows.extendvolumes.ExtendVolumesPlugin,cloudbaseinit.plugins.common.networkconfig.NetworkConfigPlugin,cloudbaseinit.plugins.common.sethostname.SetHostNamePlugin,cloudbaseinit.plugins.common.setuserpassword.SetUserPasswordPlugin,cloudbaseinit.plugins.common.localscripts.LocalScriptsPlugin,cloudbaseinit.plugins.common.userdata.UserDataPlugin
verbose=true
debug=true
logdir=C:\Program Files\Cloudbase Solutions\Cloudbase-Init\log\
logfile=cloudbase-init.log
default_log_levels=comtypes=INFO,suds=INFO,iso8601=WARN,requests=WARN
logging_serial_port_settings=COM1,115200,N,8
mtu_use_dhcp_config=true
ntp_use_dhcp_config=true
first_logon_behaviour=no
netbios_host_name_compatibility=false
allow_reboot=false
activate_windows=true
kms_host="kms.tencentyun.com"
local_scripts_path=C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts\
```
3. Copie o script `TencentCloudRun.ps1` para `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts`.
4. Clique com o botão direito do mouse no script `TencentCloudRun.ps1`, selecione **Properties (Propriedades)** e marque a permissão executável na janela pop-up, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/3a3a31fc4d0dbd58cacb9211f7a97e79.png)
- Marque **Unblock (Desbloquear)** e clique em **OK**.
- Pule essa etapa se a opção **Unblock (Desbloquear)** não existir.
5. Substitua `localscripts.py` em `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\Python\Lib\site-packages\cloudbaseinit\plugins\common` com o arquivo `localscripts.py` no [software necessário](#PreparationSoftware).
