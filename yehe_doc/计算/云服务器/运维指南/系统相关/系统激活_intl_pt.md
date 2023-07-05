Os CVMs usam o KMS para autorizar servidores Windows.
>! 
> - Este documento trata apenas de imagens públicas do Windows Server fornecidas pelo Tencent Cloud. Ele não se aplica a imagens personalizadas ou imagens importadas de fontes externas.
> - O Windows Server 2008 e o Windows Server 2012 precisam ser autorizados usando este método. O endereço padrão do KMS (kms.tencentyun.com:1668) configurado para as imagens públicas do Windows Server 2016 e Windows Server 2019 está correto e não precisa ser modificado.


## Observações
1. O Serviço de notificação SPP no **Windows Server 2008** é usado para ativação. Certifique-se de ele que funciona corretamente, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/f84f7bd86fae0df1c2394cdc554b6a98.png)
2. Alguns softwares de otimização podem desativar a modificação das permissões de execução de programas de serviço. Por exemplo, modificar as permissões de execução de sppsvc.exe pode resultar em exceções, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/c1ad23337b0f1b6e186d0c6e50c9e1b5.png)
Antes de ativar um CVM do Windows, certifique-se de que os serviços e outras funcionalidades dele estejam normais.
 
## Ativação automática
O Tencent Cloud encapsula um script para ativar servidores Windows, o que simplifica a ativação automática. Para usar o script de ativação, siga as etapas abaixo:
1. Faça login no CVM do Windows.
2. Baixe o [script](https://iso-1251783334.cos.ap-guangzhou.myqcloud.com/scripts/activate-win.bat), e execute-o para concluir a ativação automática.


## Ativação manual

### Observações
Um relógio do sistema impreciso vai disparar um erro durante a ativação manual para alguns sistemas. Nesse caso, é necessário sincronizar o relógio do sistema primeiro, seguindo as etapas abaixo:
> Se o relógio do sistema no CVM do Windows estiver normal, pule para [Ativação](#ActivationStep).
>
1. Faça login no CVM do Windows.
2. Na área de trabalho, escolha **Start (Iniciar)** > **Run (Executar)**. Digite `cmd.exe` na caixa de diálogo "Run (Executar)" para abrir a janela do console.
3. Na janela do console, execute os seguintes comandos em sequência para sincronizar o relógio do sistema:
```
w32tm /config /syncfromflags:manual /manualpeerlist:"ntpupdate.tencentyun.com"
w32tm /resync
```

<span id="ActivationStep"></span>
### Ativação

1. Faça login no CVM do Windows.
2. Na área de trabalho, escolha **Start (Iniciar)** > **Run (Executar)**. Digite `cmd.exe` na caixa de diálogo "Run (Executar)" para abrir a janela do console.
3. Na janela do console, execute os comandos a seguir sequencialmente para concluir a ativação manual.
 - Execute os seguintes comandos sequencialmente para Windows Server 2008, Windows Server 2012 e Windows Server 2019:
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```
 - Execute os seguintes comandos em sequência para servidores Windows Server 2016:
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms1.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```




