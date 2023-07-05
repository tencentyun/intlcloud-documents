## Descrição do problema
Ao criar um novo namespace de rede, o comando correspondente bloqueia e não permite continuar. Mensagem Dmesg: "unregister_netdevice: waiting for lo to become free. Usage count = 1 (unregister_netdevice: esperando que lo se torne livre. Quantidade de uso = 1)"

## Causas
Esse problema é causado por um bug no kernel. As seguintes versões do kernel possuem esse bug:
- Versão do kernel do Ubuntu 16.04 x86_32: 4.4.0-92-generic.
- Versão do kernel do Ubuntu 16.04 x86_32: 4.4.0-92-generic.

## Solução

Atualize o kernel para a versão 4.4.0-98-generic. Nesta versão, o bug já foi corrigido.

## Instruções
1. Execute o comando a seguir para verificar a versão vigente do kernel.

```
uname -r
```

2. Execute o comando a seguir para verificar se a versão 4.4.0-98-generic está disponível para atualização.

```
sudo apt-get update
sudo apt-cache search linux-image-4.4.0-98-generic
```

Se as informações abaixo forem exibidas, significa que esta versão existe na fonte e está disponível para atualização. 

```
linux-image-4.4.0-98-generic - Linux kernel image for version 4.4.0 on 64 bit x86 SMP
```

3. Execute o comando a seguir para instalar a nova versão do kernel e o pacote Cabeçalho correspondente.

```
sudo apt-get install linux-image-4.4.0-98-generic linux-headers-4.4.0-98-generic
```

4. Execute o comando a seguir para reiniciar o sistema.

```
sudo reboot
```

5. Execute o comando a seguir para acessar o sistema e verificar a versão do kernel.

```
uname -r
```

Se o seguinte resultado for exibido, significa que a atualização da versão foi bem-sucedida:

```
4.4.0-98-generic
```
