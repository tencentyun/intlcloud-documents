## Introdução

Ao criar uma instância do CVM, você tem a opção de definir um script como **Custom Data (Dados personalizados)** e usá-lo para personalizar a configuração da instância. Quando a instância é inicializada pela primeira vez, esses dados personalizados são transmitidos e executados. Se você adquiriu várias instâncias do CVM, todas as instâncias executarão o script na primeira inicialização.
Este artigo descreve como definir um script PowerShell e usá-lo para configurar uma instância do CVM do Windows.

## Considerações

- Os sistemas operacionais Windows que aceitam dados personalizados incluem:
 - Windows Server 2019 Datacenter Edition de 64 bits versão Chinês/Inglês
 - Windows Server 2016 Datacenter Edition de 64 bits versão Chinês/Inglês
 - Windows Server 2012 R2 Datacenter Edition de 64 bits versão Chinês/Inglês
- O script é executado somente quando a instância for inicializada pela primeira vez.
- Antes da codificação em Base64, o tamanho dos dados personalizados não pode exceder 16 KB.
- Os dados personalizados são codificados em Base64 e depois transmitidos. Caso queira um arquivo de script em seu formato original, não selecione **The entry is Base64-encoded text (A entrada é texto codificado em Base64)**.
- As configurações personalizadas que você definiu no script de dados personalizados demoram para serem executadas. Recomendamos que você aguarde a conclusão das configurações e verifique os resultados.
- Use a tag PowerShell, como & lt; powershell &lt;powershell&gt;&lt;/powershell&gt; para declarar o conteúdo do script Windows PowerShell.

## Instruções

### Preparação de script

Prepare um script que atenda às suas necessidades:

<span id="PowerShellScript"></span>
#### Script PowerShell
Use as tags PowerShell para envolver o conteúdo do script.
Por exemplo, se você deseja usar o script para criar um arquivo chamado `tencentcloud.txt` com o conteúdo de "Hello Tencent Cloud." na unidade C:, use as seguintes tags:
```
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```

<span id="Base64Script"></span>
#### Codificação do script com Base64

1. Execute o comando a seguir para criar um script PowerShell chamado "script_text.ps1".
```
vi script_text.ps1
```
2. Pressione **i** para mudar para o modo de edição, insira o conteúdo a seguir e salve.
```
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```
3. Execute o comando a seguir para codificar **script_text.ps1** com Base64.
```
base64 script_text.ps1
```
As seguintes informações são retornadas:
```
PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAgQzpcdGVuY2VudGNsb3VkLnR4dAo8L3Bvd2Vyc2hlbGw+Cg==
```

### Passagem do script

Fornecemos vários métodos para iniciar uma instância. Veja abaixo os métodos mais usados:
- [Uso do site oficial ou do console](#Consoletrans)
- [Uso de APIs](#APItrans)

<span id="Consoletrans"></span>
#### Uso do site oficial ou do console

1. Use [Criação de uma instância](https://intl.cloud.tencent.com/document/product/213/4855) como referência e crie uma instância do CVM. Clique em **Advanced Configuration (Configuração avançada)** em **4. Configure Security Group and CVM (4. Configurar grupo de segurança e CVM)**, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/28baf2764488ecfaf5bbac791cec7ea3.png)
2. Em **Advanced Configuration (Configuração avançada)**, insira o conteúdo do script na caixa de texto **Custom Data (Dados personalizados)**.
 - Script PowerShell: digite o conteúdo do script que você inseriu no [script PowerShell](#PowerShellScript) em seu formato original.
 - Script codificado em Base64: selecione **The entry is Base64-encoded text (A entrada é texto codificado em Base64)** e insira o conteúdo do script codificado que você codificou em [Codificação do script com Base64](#Base64Script), conforme mostrado na figura abaixo:
 ![](https://main.qcloudimg.com/raw/0b6b594f174568ca7d3312821c0571ed.png)
4. Siga as instruções e conclua a criação do CVM.

<span id="APItrans"></span>
#### Uso de APIs

Se você optar por criar uma instância do CVM usando APIs do Tencent Cloud, você pode atribuir o resultado codificado retornado em [Codificação do script com Base64](# Base64Script) para o parâmetro UserData de RunInstances.
Veja abaixo um exemplo de solicitação de criação de CVM com UserData:
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
  &Version=2017-03-12
  &Placement.Zone=ap-guangzhou-2
  &ImageId=img-pmqg1cw7
  &UserData=PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAuXHRlbmNlbnRjbG91ZC50eHQKPC9wb3dlcnNoZWxsPgo=
  &<Common request parameter>
```

### Verificação das configurações de dados personalizados

1. Faça login na instância do CVM.
2. Abra a unidade C: e verifique se existe `tencentcloud.txt`.
Em caso afirmativo, a configuração obteve êxito, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/9f94ec922111734a489b9730d66168c3.png)


