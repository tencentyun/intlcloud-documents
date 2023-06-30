## Cenário

O serviço de Horário do Windows (W32Time) sincroniza a hora entre o sistema local e o servidor de origem do relógio. Ele usa o NTP para sincronizar os relógios do computador na rede. O seguinte usa um CVM que executa o Windows Server 2012 como exemplo para descrever como habilitar o serviço NTP e modificar o endereço IP do servidor de origem do relógio.

## Instruções

1. Faça login no CVM do Windows.
2. Na área de trabalho, selecione <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> > **Task Manager (Gerenciador de Tarefas)** > **Services (Serviços)** para abrir a janela **Services (Services)**.
3. Na janela **Services (Serviços)** que aparece, clique duas vezes em **Windows Time (Horário do Windows)**, conforme mostrado na figura a seguir.
![](https://main.qcloudimg.com/raw/c5e41df2fc832b0f25f798408163664c.png)
4. Na janela **Windows Time Properties (Local Computer) (Propriedades de horário do Windows (computador local))** que aparece, defina **Startup type (Tipo de inicialização)** como **Automatic (Automático)** e **Service Status (Status do serviço)** como **Running (Em execução)** e clique em **OK**, conforme mostrado na figura a seguir.
![](https://main.qcloudimg.com/raw/9201ddaca176a1523d5d12d02b6c8ec5.png)
5. Na barra de tarefas da área de trabalho, clique no ícone de hora no canto inferior direito e clique em **Change date and time settings... (Alterar configurações de data e hora…)**, conforme mostrado na figura a seguir.
![](https://main.qcloudimg.com/raw/28ba1cf5968466e114e93d222b957f99.png)
6. Na janela **Date and Time (Data e hora)** exibida, clique na guia **Internet Time (Horário da Internet)** e, em seguida, clique em **Change Settings (Alterar configurações)**, conforme mostrado na figura a seguir.
![](https://main.qcloudimg.com/raw/767eee448b33ed38ea7bc2fbdadf780d.png)
7. Na janela **Internet Time Settings (Configurações de horário da Internet)** que aparece, insira o nome de domínio ou endereço IP do servidor de origem do relógio de destino na caixa de texto **Server (Servidor)** e clique em **OK**, conforme mostrado na figura a seguir.
![](https://main.qcloudimg.com/raw/205ef59f3e8583af965a9381df0a9ef9.png)



