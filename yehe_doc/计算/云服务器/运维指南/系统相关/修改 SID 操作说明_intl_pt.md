## Cenário

O sistema operacional Microsoft usa um identificador de segurança (SID) para identificar computadores e usuários. As instâncias do CVM criadas com a mesma imagem terão o mesmo SID e podem enfrentar problemas de login no domínio. Se você precisar criar um ambiente de domínio do Windows, será necessário modificar o SID.
Este documento usa o CVM com o sistema operacional Windows Server 2012 como um exemplo para descrever como modificar o SID usando as ferramentas sysprep e sidchg do sistema.

## Observações

- Isso se aplica apenas ao Windows Server 2008 R2, Windows Server 2012 e Windows Server 2016.
- Para modificar o SID em lote, você pode criar uma imagem personalizada (selecione "run sysprep to create the image (execute o sysprep para criar a imagem)").
- Modificar o SID pode causar perda de dados ou danos ao sistema. Recomendamos que você crie um snapshot ou imagem do disco do sistema com antecedência.

## Instruções

### Uso do sysprep para modificar o SID

> 
> - Depois de usar o sysprep para modificar o SID, é necessário redefinir manualmente alguns parâmetros do sistema, incluindo informações de configuração de IP.
> - Quando você usa o sysprep para modificar o SID, C:\Users\ Administrator será redefinido e alguns dados no disco do sistema serão apagados. Faça backup dos dados.
> 
1. [Login no CVM do Linux por VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Na interface do sistema operacional, clique com o botão direito do mouse em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> > **Run (Executar)**, digite **cmd** e pressione **Enter** para abrir uma linha de comando de administrador.
3. <span id="step_03">Na linha de comando de administrador, execute o comando a seguir para salvar a configuração de rede atual.</span>
```
ipconfig /all
```
4. Na linha de comando de administrador, execute o comando a seguir para abrir a ferramenta sysprep.
```
C:\Windows\System32\Sysprep\sysprep.exe
```
5. Na janela "System Preparation Tool 3.14 (Ferramenta de preparação do sistema 3.14)" exibida, realize a configuração a seguir.
 - Defina **System Cleanup Action (Ação de limpeza do sistema)** como **Enter System Out-of-Box Experience (OOBE) (Entrar na configuração inicial pelo usuário do sistema (OOBE))** e marque **General (Geral)**.
 - Defina **Shutdown Options (Opções de desligamento)** como **Reboot (Reiniciar)**.
6. Clique em **OK**, e o sistema será reiniciado automaticamente.
7. Após concluir a inicialização, siga o assistente para realizar a configuração (selecione o idioma, redefina a senha, etc.).
8. Na interface do sistema operacional, clique com o botão direito do mouse em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> > **Run (Executar)**, digite **cmd** e pressione **Enter** para abrir uma linha de comando de administrador.
9. Execute o comando a seguir para verificar se o SID foi modificado.
```
whoami /user
```
Se uma mensagem semelhante à seguinte for retornada, o SID foi modificado.
![](https://main.qcloudimg.com/raw/34efb1f4128c753e6c0546f3e8d58678.png)
10. Redefina as informações de ENI (como endereço IP, endereço de gateway, DNS, etc.) com base nas informações de configuração de rede salvas na [Etapa 3](#step_03).


### Uso do sidchg para modificar o SID

1. Faça login no CVM.
2. Acesse e baixe a ferramenta sidchg por meio do navegador IE.
Endereço de download da ferramenta sidchg: `http://www.stratesave.com/html/sidchg.html`
3. Use a linha de comando de administrador para executar o seguinte comando e abrir a ferramenta sidchg, conforme mostrado abaixo:
Por exemplo, a ferramenta sidchg é salva na unidade C: e seu nome é sidchg64-2.0p.exe.
![](https://main.qcloudimg.com/raw/284926ae1eae88228fb009f247b82068.png)
`/R` significa reinicialização automática após a modificação e ` /S` significa desligamento após a modificação. Para obter detalhes, consulte [Instruções oficiais do SIDCHG](http://www.stratesave.com/html/sidchg.html).
4. Insira a chave de licença ou a chave de teste conforme solicitado pela página e pressione **Enter**.
5. Digite **Y** conforme solicitado pela página e pressione **Enter**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/43c19634475517b183402d15fa32e962.png)
6. Na caixa de prompt para modificar o SID, clique em [OK] para redefini-lo, conforme mostrado abaixo:
O sistema será reiniciado durante a redefinição.
![](https://main.qcloudimg.com/raw/b59ec21417cc0de1fd7d851fcd8a2a3b.png)
7. Após concluir a inicialização, clique com o botão direito em <img src = "https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style = "margin: 0;">> **Run (Executar)**, digite **cmd** e pressione **Enter** para abrir a linha de comando de administrador.
8. Execute o comando a seguir para verificar se o SID foi modificado.
```
whoami /user
```
Se uma mensagem semelhante à seguinte for retornada, o SID foi modificado.
![](https://main.qcloudimg.com/raw/34efb1f4128c753e6c0546f3e8d58678.png)
