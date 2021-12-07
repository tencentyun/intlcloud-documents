Este documento descreve como implementar projetos Nginx no CentOS e é adequado para novos usuários individuais do Tencent Cloud.
## Versão de software
As versões das ferramentas de software usadas neste documento seguem indicadas abaixo e podem ser diferentes das versões que você utilizará ao executar as operações.
- Sistema operacional: CentOS 7.5
- Nginx: Nginx 1.16.1

## Instalação do Nginx
1. Após concluir a aquisição, clique em **Login** na página de detalhes do CVM para fazer login na instância do CVM e, em seguida, insira seu nome de usuário e senha para configurar um ambiente Nginx. Para obter mais informações sobre como criar uma instância do CVM, consulte [Criação de instâncias CVM](https://cloud.tencent.com/document/product/213/4855).
```
# Instalar o Nginx
yum -y install nginx  
# Visualizar a versão do Nginx
nginx -v
# Visualizar o diretório de instalação do Nginx
rpm -ql nginx
# Iniciar o Nginx
service nginx start
```
2. Acesse o endereço IP público da instância do CVM e se a página a seguir for exibida, o Nginx foi implementado com sucesso:
![](https://main.qcloudimg.com/raw/8807f9fd819eb93d46c5646ba3572fac.png)
3. O diretório raiz padrão do Nginx é `/usr/share/nginx/html`. Modifique a página estática `index.html` no diretório`html` para marcar o caráter especial desta página. As operações relevantes são as seguintes:
   1. Execute o seguinte comando para entrar na página estática `index.html` em` html`:
```bash
vim /usr/share/nginx/html/index.html
```
   2. Pressione "i" para entrar no modo de edição e inclua o seguinte na tag `<body></body>`:
```bash
# Recomenda-se que você entre diretamente em `<body>`
Hello nginx , This is rs-1!
URL is index.html
```
  ![](https://main.qcloudimg.com/raw/02e833dd08a6873d5d015f4531d24645.png)
   3. Pressione "Esc" e digite `:wq` para salvar a alteração.
4. O CLB (anteriormente "CLB do aplicativo") pode encaminhar solicitações de acordo com o caminho do servidor de back-end e implementar uma página estática no caminho `/image`. As operações relevantes são as seguintes:
   1. Execute os seguintes comandos para criar e acessar um diretório `image`:
```bash
mkdir /usr/share/nginx/html/image
cd /usr/share/nginx/html/image
```
   2. Execute o seguinte comando para criar uma página estática `index.html` no diretório`image`:
```
vim index.html
```
   3. Pressione "i" para entrar no modo de edição e inclua o seguinte na página:
```bash
Hello nginx , This is rs-1!
URL is image/index.html
```
   4. Pressione "Esc" e digite `:wq` para salvar a alteração.
>! A porta padrão do Nginx é `80`. Para alterar a porta, modifique o arquivo de configuração e reinicie o Nginx.

## Verificação do serviço Nginx
Acesse o IP público e o caminho de sua instância do CVM. Se a página estática implementada for exibida, a implementação do Nginx foi bem-sucedida.
- página `index.html` do `rs-1`:
![](https://main.qcloudimg.com/raw/ede62fecd2106869d53bf142ad51903e.png)
- página `/image/index.html` do `rs-1`:
![](https://main.qcloudimg.com/raw/f0f87422487177722291c2260cac9d35.png)
