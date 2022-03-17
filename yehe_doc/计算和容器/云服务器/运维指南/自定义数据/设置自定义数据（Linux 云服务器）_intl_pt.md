## Cenário

Ao criar um CVM, você pode configurar uma instância especificando **custom data (dados personalizados)**. Durante a **primeira inicialização** do CVM, os dados personalizados serão transmitidos para o CVM em formato de texto e executados. Se você adquirir vários CVMs de uma vez, todos os CVMs executarão os dados personalizados na primeira inicialização.
Este artigo descreve como passar um script Shell ao iniciar um CVM do Linux pela primeira vez.

## Observações
- Os sistemas operacionais Linux que aceitam dados personalizados incluem:
	- Sistema operacional de 64 bits: CentOS 6.8 de 64 bits ou versões posteriores, Ubuntu Server 14.04.1 LTS de 64 bits ou versões posteriores e suse42.3x86_64
	- sistema operacional 32-bit: CentOS 6.8 de 32 bits ou versões posteriores
- Um comando pode ser executado passando texto apenas quando um CVM é iniciado pela primeira vez.
- Os dados personalizados devem ser codificados em Base64 e depois transmitidos. **Para um formato compatível, codifique os dados personalizados no ambiente Linux.**
- Execute os dados personalizados como `root`. Portanto, o comando `sudo` não é necessário no script. O usuário `root` pode acessar todos os arquivos que você criou. Se você precisar conceder permissão de acesso a outros usuários, modifique a permissão no script.
- Durante a inicialização, a execução de tarefas de dados personalizados aumentará o tempo de inicialização do CVM. Aguarde alguns minutos até que as tarefas sejam concluídas e, em seguida, teste se as tarefas foram executadas.
* Neste exemplo, o script Shell deve começar com `#!` e o caminho para o interpretador lendo o script (geralmente `/bin/bash`).

## Instruções

### Gravação de um script Shell
1. Execute o comando a seguir para criar um script Shell chamado "script_text.sh".
```
vi script_text.sh
```
2. Pressione **i** para mudar para o modo de edição, digite o texto a seguir e salve o script "script_text.sh".
```
#!/bin/bash
echo "Hello Tencent Cloud."
```
> O script Shell deve começar com `#!` e o caminho para o interpretador lendo o script (geralmente `/bin/bash`). Para obter mais informações sobre o script Shell, consulte Programação BASH do Projeto de documentações do Linux (tldp.org) (http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html).

<span id="Base64Script"></span>
### Codificação do script com Base64

1. Execute o comando a seguir para codificar o script "script_text.sh" com Base64.
```
# Base64 encoded script
base64 script_text.sh
```
Você verá as seguintes informações:
```
# Encoded result
IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
```
2. Execute o comando a seguir para verificar o resultado codificado em Base64 do script.
```
# Decode the returned result with Base64 and verify whether it is the command to be executed.
echo "IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==" | base64 -d
```

### Passamento do texto

Você pode iniciar uma instância por meio de vários métodos, e aqui apresentamos dois deles. Escolha um método de acordo com seus requisitos:
- [Uso do site oficial ou do console](#Consoletrans)
- [Uso de API](#APItrans)

<span id="Consoletrans"></span>
#### Uso do site oficial ou do console

1. Consulte [Criação de instâncias](https://intl.cloud.tencent.com/document/product/213/4855) para adquirir uma instância e clique em **Advanced Settings (Configurações avançadas)** em "4. Security Group and CVM (4. Grupo de segurança e CVM)", conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/28baf2764488ecfaf5bbac791cec7ea3.png)
2. Em **Advanced Settings (Configurações avançadas)**, insira o resultado retornado de [Script codificado em Base64](#Base64Script) na caixa de texto Custom Data (Dados personalizados), conforme mostrado abaixo:
Por exemplo, o resultado codificado em Base64 do script `script_text` é `IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==`.
![](https://main.qcloudimg.com/raw/0b6b594f174568ca7d3312821c0571ed.png)
3. Crie uma instância do CVM conforme solicitado pela página.
>O CVM do Tencent Cloud executa o script usando o software livre cloud-init. Para obter mais informações sobre o cloud-init, consulte o [site oficial do cloud-init](https://cloud-init.io/).

<span id="APItrans"></span>
#### Uso de API

Ao criar um CVM usando API, você pode passar o texto atribuindo o valor do resultado codificado retornado em [Script codificado em Base64](#Base64Script) para o parâmetro UserData da API RunInstances.
Veja abaixo um exemplo de solicitação de criação de CVM com UserData:
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
  &Version=2017-03-12
  &Placement.Zone=ap-guangzhou-2
  &ImageId=img-pmqg1cw7
  &UserData=IyEvYmluL2Jhc2gKZWNobyAiSGVsbG8gVGVuY2VudCBDbG91ZC4iCg==
  &<Common request parameters>
```
