## Introdução
Este artigo descreve como implementar o Node.js em um CVM e criar um projeto de amostra.

Isso requer que você esteja familiarizado com os comandos comuns do Linux, como [Instalação de software via YUM em um ambiente CentOS](https://intl.cloud.tencent.com/document/product/213/2046), e compreenda as versões do software instalado.

## Software
A configuração do Node.js envolve:
- CentOS: uma distribuição do sistema operacional Linux. Usamos o CentOS 7.6 neste artigo.
- Node.js: um ambiente de tempo de execução JavaScript. Usamos Node.js 10.16.3 e Node.js 6.9.5 neste artigo.
- npm: um gerenciador de pacotes para JavaScript. Usamos o npm 6.9.0 neste artigo para gerenciar várias versões do Node.js.

## Pré-requisitos
Para configurar o Node.js, você precisa de um CVM Linux Se você ainda não comprou um, consulte [Introdução aos CVMs Linux](http://intl.cloud.tencent.com/document/product/213/2936).

## Instruções
### Etapa 1: login em uma instância do Linux
[Faça login em uma instância do Linux usando WebShell (recomendado)](https://intl.cloud.tencent.com/document/product/213/5436). Você também pode usar outros métodos de login com os quais se sinta confortável:
- [Faça login em uma instância do Linux usando software de login remoto](https://intl.cloud.tencent.com/document/product/213/32502).
- [Faça login em uma instância do Linux usando SSH](https://intl.cloud.tencent.com/document/product/213/32501)


### Etapa 2: Instalação do Node.js
1. Execute o seguinte comando para fazer download do pacote de instalação Node.js de 64 bits para Linux.
```
wget https://nodejs.org/dist/v10.16.3/node-v10.16.3-linux-x64.tar.xz
```
> Consulte o [site oficial do Node.js](https://nodejs.org/download/) para mais informações.
>
2. Execute o seguinte comando para descompactar o pacote de instalação.
```
tar xvf node-v10.16.3-linux-x64.tar.xz
```
3. Execute os seguintes comandos para criar links simbólicos.
```
ln -s /root/node-v10.16.3-linux-x64/bin/node /usr/local/bin/node
```
```
ln -s /root/node-v10.16.3-linux-x64/bin/npm /usr/local/bin/npm
```
Uma vez criados, você pode usar os comandos node e npm em qualquer diretório CVM.
4. Execute os comandos a seguir para visualizar as versões Node.js e npm.
```
node -v
```
```
npm -v
```

### Etapa 3: Instalação de várias versões do Node.js (opcional)
> Este processo permite que você instale várias versões do Node.js. Os desenvolvedores podem usar isso para alternar rapidamente entre as versões.
>
1. Execute o seguinte comando para instalar o git.
```
yum install -y git
```
2. Execute o seguinte comando para baixar o código-fonte NVM e conferir a versão mais recente.
```
git clone https://github.com/cnpm/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`
```
3. Execute o seguinte para configurar as variáveis ​​de ambiente NVM.
```
echo ". ~/.nvm/nvm.sh" >> /etc/profile
```
4. Execute o seguinte comando para ler as variáveis ​​de ambiente do sistema.
```
source /etc/profile
```
5. Execute os comandos a seguir para visualizar todas as versões do Node.js.
```
nvm list-remote
```
6. Execute os comandos a seguir para instalar várias versões do Node.js.
```
nvm install v6.9.5
```
```
nvm install v10.16.3
```
7. Execute o seguinte comando para visualizar todas as versões Node.js instaladas.
```
nvm ls
```
Se aparecer o seguinte, a instalação foi bem-sucedida e a versão atual em uso é Node.js 10.16.3.
![](https://main.qcloudimg.com/raw/a315fe51314357fb44ec725f20c101ed.png)
8. Execute o seguinte comando para alternar para outra versão.
```
nvm use v6.9.5
```
As seguintes informações são exibidas:
![](https://main.qcloudimg.com/raw/817fd96fef77f818e65ce41a3723e5bc.png)

### Etapa 4: Criação de um projeto de amostra
1. Execute os seguintes comandos para criar um arquivo denominado `index.js` no caminho raiz.
```
cd ~
```
```
vim index.js
```
2. Pressione **i** para entrar no modo de edição e insira o seguinte no arquivo `index.js`:
```
const http = require('http');
const hostname = '0.0.0.0';
const port = 7500;
const server = http.createServer((req, res) => { 
    if (res.statusCode === 200) {
    res.setHeader('Content-Type', 'text/plain');
    res.end('Hello World\n');
}); 
server.listen(port, hostname, () => { 
    console.log(`Server running at http://${hostname}:${port}/`);
});
```
> Este artigo usa a porta 7500 no arquivo `index.js`. Você pode usar outras portas conforme necessário.
>
3. Pressione **Esc** e insira **: wq** para salvar o arquivo e voltar.
4. Execute o seguinte comando para executar o projeto Node.js que acabamos de criar.
```
node index.js
```
5. Abra uma janela do navegador em sua máquina local e visite a seguinte URL para verificar se o projeto foi executado com sucesso.
```
http://CVM_Public_IP:Port
```
Se aparecer o seguinte, o Node.js foi instalado com sucesso.
![](https://main.qcloudimg.com/raw/5b72798dc9e988eee8d8186055aa45e9.png)


## Perguntas frequentes
Se você encontrar um problema ao usar o CVM, consulte os seguintes documentos para solucionar problemas com base em sua situação real.
- Para questões relacionadas ao login do CVM, consulte [Login de senha e login de chave SSH](https://intl.cloud.tencent.com/document/product/213/18120) e [Login e acesso remoto](https://intl.cloud.tencent.com/document/product/213/17278).
- Para questões relacionadas à rede CVM, consulte [Endereços IP](https://intl.cloud.tencent.com/document/product/213/17285) e [Portas e grupos de segurança](https://intl.cloud.tencent.com/document/product/213/2502).
- Para questões relacionadas aos discos CVM, consulte [Discos de sistema e dados](https://intl.cloud.tencent.com/document/product/213/17351).

