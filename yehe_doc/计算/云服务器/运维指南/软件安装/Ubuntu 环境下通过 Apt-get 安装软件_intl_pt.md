## Introdução
O Advanced Package Tool (APT) é uma interface de usuário de software livre que usa bibliotecas centrais para lidar com a instalação e remoção de software em várias distribuições do Linux. O APT oferece uma interface centralizada para gerenciamento de software e uma experiência melhor do que ter que baixar e instalar um software de cada vez. O Tencent Cloud hospeda fontes do APT para que você possa instalar software sem adicionar fontes.

## Pré-requisitos
Faça login em uma instância do CVM do Linux que executa o Ubuntu.

## Instruções
> A seguir, o Nginx é usado como exemplo.
>

### Lista de softwares disponíveis
Execute o seguinte comando para listar os softwares disponíveis:
```
sudo apt-cache search all
```

### Instalação de software
Execute o seguinte comando para instalar o Nginx: 
```
sudo apt-get install nginx
```
Certifique-se de que este é o software que deseja instalar e digite `Y` para aprovar a instalação. Aguarde até que a instalação do software seja concluída, conforme mostrado na figura abaixo:
![](https://mc.qcloudimg.com/static/img/d03f55bba1690ff30532b73148ccc1e9/45.png)

### Consulta do software instalado
Você pode executar comandos diferentes para consultar o software instalado.
- Execute o comando a seguir para consultar o diretório do pacote de software e todos os arquivos no pacote de software.
``` 
sudo dpkg -L software_name 
```
- Execute o comando a seguir para consultar as informações de versão do pacote de software.
``` 
sudo dpkg -l software_name 
```

Exiba informações sobre o Nginx instalado, conforme mostrado na figura abaixo:
![](https://mc.qcloudimg.com/static/img/8bbc99d7a31e8463da36f3dc2221c028/46.png)
