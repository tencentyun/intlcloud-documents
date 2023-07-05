## Visão geral
Este documento descreve como construir e usar o Docker em uma instância Tencent Cloud CVM e é projetado para novos desenvolvedores CVM que estão familiarizados com o sistema operacional Linux.

## Software

Este documento usa o seguinte software para construir o ambiente Docker:
- Sistema operacional: Sistema operacional Linux. Este documento usa a versão CentOS 7.6 como exemplo.
>? O Docker deve ser construído em um sistema operacional de 64 bits com o kernel versão 3.10 ou posterior.
>

## Pré-requisitos
Um CVM Linux é necessário para configurar um ambiente Docker. Se você ainda não comprou um CVM Linux, consulte [Personalização das configurações do CVM Linux](https://intl.cloud.tencent.com/document/product/213/10517).
>? O Docker deve ser construído em um sistema operacional de 64 bits com o kernel versão 3.10 ou posterior.
>

## Instruções

### Instalação do Docker

1. Consulte [Fazer login na instância do Linux usando o método de login padrão](https://intl.cloud.tencent.com/document/product/213/5436). Você também pode usar outros métodos de login com os quais se sinta mais confortável:
 - [Fazer login em instâncias do Linux por meio de ferramentas de login remoto](https://intl.cloud.tencent.com/document/product/213/32502)
 - [Fazer login em instâncias do Linux via chave SSH](https://intl.cloud.tencent.com/document/product/213/32501)
2. Execute os seguintes comandos em sequência para adicionar o repositório yum.
```
yum update
```
```
yum install epel-release -y
```
```
yum clean all
```
```
yum list
```
3. Execute o seguinte comando para instalar o Docker.
```
yum install docker-io -y
```
4. Execute o seguinte comando para rodar o Docker.
```
systemctl start docker
```
5. Execute o seguinte comando para verificar o resultado da instalação.
```
docker info
```
Se você vir a solicitação a seguir, isso indica que o Docker foi instalado com sucesso.
![](https://main.qcloudimg.com/raw/a848737e9d011f528f66dc54fca61c08.png)


### Utilização do Docker
É possível usar o Docker com os seguintes comandos:
- Gerenciar o daemon do Docker.
 - Executar o daemon do Docker.
```
systemctl start docker
```
 - Interromper o daemon do Docker.
```
systemctl stop docker
```
 - Reiniciar o daemon do Docker.
```
systemctl restart docker
```
- Gerenciar imagens. Este documento usa a imagem Nginx do Docker Hub como exemplo.
```
docker pull nginx 
```
 - Modificar a marca da imagem para ajudá-lo na identificação.
```
docker tag docker.io/nginx:latest tencentyun/nginx:v1
```
 - Consultar imagens existentes.
```
docker images
```
 - Excluir uma imagem à força.
```
docker rmi -f tencentyun/nginx:v1
```
- Gerenciar contêineres.
 - Acessar um contêiner.
```
docker run -it ImageId /bin/bash
```
Execute o comando `docker images` para obter o valor `ImageId`.
 - Sair do contêiner. Execute o comando `exit` para sair do contêiner.
 - Acessar um contêiner em execução em segundo plano.
```
docker exec -it container ID /bin/bash
```
 - Criar uma imagem do contêiner.
```
docker commit <container ID or container name> [<repository name>[:<tag>]]
```
Por exemplo:
```
docker commit 1c23456cd7**** tencentyun/nginx:v2
```

### Criação de imagens

1. Execute o seguinte comando para abrir o arquivo "Dockerfile".
```
vim Dockerfile
```
2. Pressione **i** para alternar para o modo de edição e insira o seguinte conteúdo:
```
FROM tencentyun/nginx:v2 #Declarar uma imagem básica.
MAINTAINER DTSTACK #Declarar o proprietário da imagem.
RUN mkdir /dtstact #Adicionar o comando que precisa ser executado antes que o contêiner seja iniciado após o comando RUN. Como os arquivos Dockerfile podem conter no máximo 127 linhas, recomendamos que você escreva e execute os comandos no script.
ENTRYPOINT ping https://cloud.tencent.com/ #Os comandos executados na inicialização. O último comando deve ser um comando de frontend executado constantemente. Caso contrário, o contêiner será encerrado após a execução de todos os comandos.
```
3. Pressione **Esc** e digite **:wq** para salvar o arquivo.
4. Execute o seguinte comando para construir uma imagem.
```
docker build -t nginxos:v1 .  #O único ponto (.) especifica o caminho do Dockerfile e deve ser incluído.
```
5. Execute o seguinte comando para verificar se a imagem foi criada.
```
docker images
```
6. Execute os seguintes comandos em sequência para executar e verificar o contêiner.
```
docker run -d nginxos:v1         #Executar o contêiner em segundo plano.
docker ps                        #Verificar o contêiner em execução.
docker ps -a                     #Verificar todos os contêineres, incluindo aqueles que não estão em execução.
docker logs CONTAINER ID/IMAGE #Verificar o log de inicialização para solucionar o problema com base na ID ou nome do contêiner, se você não vir o contêiner nos resultados retornados
```
7. Execute os seguintes comandos em sequência para criar uma imagem.
```
docker commit fb2844b6**** nginxweb:v2 #Adicionar o ID do contêiner, o nome e a versão da nova imagem, após o comando commit.
docker images                  #Listar as imagens locais que foram baixadas e criadas.
```
8. Execute o seguinte comando para enviar a imagem para o repositório remoto.
A imagem é enviada ao Docker Hub por padrão. Para enviar a imagem, faça login no Docker, marque e nomeie a imagem no seguinte formato: `Docker username/image name: tag`.
```
docker login #Digite o nome de usuário e a senha do registro de imagem após executar o comando
docker tag [image name]:[tag] [username]:[tag]
docker push [username]:[tag]
```
Depois que a imagem é enviada, você pode fazer login no Docker Hub para visualizá-la.



