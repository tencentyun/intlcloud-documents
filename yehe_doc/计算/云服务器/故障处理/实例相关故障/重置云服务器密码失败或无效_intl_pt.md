Este documento usa o Windows Server 2012 como exemplo para descrever como solucionar problemas de redefinições de senha do CVM com falha ou inválidas.

## Problemas

- Após a redefinição da senha do CVM, o sistema exibe “The system is busy, and your instance password failed to be reset (7617d94c).” (O sistema está ocupado e a senha da sua instância falhou ao ser redefinida (7617d94c)).
- Após a redefinição da senha do CVM, a nova senha não tem efeito e a senha de login permanece a antiga.


## Possíveis causas
As possíveis causas são:
- O componente do Cloudbase-Init no CVM está danificado, modificado, desabilitado ou não foi iniciado.
- Os componentes de um processo do sistema são bloqueados pelo programa de segurança (por exemplo, 360 Safeguard) instalado no CVM.


## Solução de problemas

Com base nas possíveis causas, solucione o problema da seguinte forma:

### Verificação do serviço Cloudbase-Init

1. [Faça login em uma instância do Windows usando o VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Na área de trabalho, clique com o botão direito em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> e selecione **Run (Executar)**. Digite **services.msc** na caixa de diálogo **Run (Executar)**, e pressione **Enter** para abrir a janela **Services (Serviços)**.
3. Verifique se o serviço cloudbase-init existe, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/2615f5c0e68a31174c16c9a80884455c.png)
 - Se existir, prossiga para a próxima etapa.
 - Se não existir, reinstale o serviço cloudbase-init. Para mais informações, consulte [Instalação do Cloudbase-Init no Windows](https://intl.cloud.tencent.com/document/product/213/32364).
4. Clique duas vezes no serviço cloudbase-init para abrir a caixa de diálogo de propriedades do cloudbase-init, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/10702cb2e359d6de36aec4960771c841.png)
5. Selecione a guia **General (Geral)** e verifique se o tipo de inicialização do cloudbase-init é **Automatic (Automática)**.
 - Se for, prossiga para a próxima etapa.
 - Se não for, defina o tipo de inicialização do cloudbase-init como **Automatic (Automática)**.
6. Alterne para a guia **Log On (Login)** e verifique se a **Local System account (Conta do sistema local)** está marcada para o serviço cloudbase-init.
 - Se estiver, prossiga para a próxima etapa.
 - Se não estiver, marque a **Local System account (Conta do sistema local)** para o serviço cloudbase-init.
7. Alterne para a guia **General (Geral)**, clique em **Start (Iniciar)** em **Service status (Status do serviço)** para ativar manualmente o serviço cloudbase-init, e verifique se ocorre algum erro.
 - Se ocorrer, [verifique o programa de segurança instalado no CVM](#CheckSecuritySoftware).
 - Se não ocorrer, prossiga para a próxima etapa.
8. Na área de trabalho, clique com o botão direito em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> e selecione **Run (Executar)**. Digite **regedit** na caixa de diálogo **Run (Executar)**, e pressione **Enter** para abrir a janela do **Registry Editor (Editor do Registro)**.
9. No painel de navegação do registro à esquerda, expanda as seguintes hierarquias em ordem: **HKEY_LOCAL_MACHINE** > **SOFTWARE** > **Cloudbase Solutions (Soluções do Cloudbase)** > **Cloudbase-Init**.
10. Localize todas as chaves de registro “LocalScriptsPlugin” em **ins-xxx** e verifique se o valor de LocalScriptsPlugin é 2.
![](https://main.qcloudimg.com/raw/75580b56e3a28fb9e0559372eb33ff11.png)
 - Se for, prossiga para a próxima etapa.
 - Se não for, defina o valor de LocalScriptsPlugin como 2.
11. Na área de trabalho, clique em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> e selecione **This PC (Este PC)**. Verifique se o driver de CD está carregado em **Devices and drives (Dispositivos e unidades)**, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/8755719fb39bb5f841f4c32897545233.png)
 - Se estiver, [verifique o programa de segurança instalado no CVM](#CheckSecuritySoftware).
 - Se não estiver, inicie o driver de CD-ROM no Device Manager (Gerenciador de Dispositivos).

<span id="CheckSecuritySoftware"></span>
-### Verificação do programa de segurança instalado no CVM

Verifique as vulnerabilidades do CVM usando o programa de segurança instalado e verifique se os componentes do Cloudbase-Init estão bloqueados.
- Se o CVM tiver vulnerabilidades, resolva-as.
- Se os componentes principais estiverem bloqueados, desbloqueie-os.

Para evitar redefinições de senha do CVM com falha ou inválidas, recomendamos adicionar os diretórios e os arquivos abaixo à lista de permissões e locais confiáveis do programa de segurança.
- Permita os seguintes diretórios no programa de segurança:
```
C:\Windows\System32\WindowsPowerShell\
C:\Program Files\Cloudbase Solutions\Cloudbase-Init\Python\Scripts
C:\Program Files\QCloud
C:\Program Files\Cloudbase Solutions\
```
- Adicione os seguintes arquivos aos locais confiáveis:
```
C:\Windows\System32\cmd.exe
C:\Windows\SysWOW64\cmd.exe
```

