O Ubuntu deixou oficialmente de fornecer manutenção para o Ubuntu 10.04 LTS e, seguindo a mesma linha, a Tencent Cloud também desativou as imagens públicas do Ubuntu 10.04.

As árvores de diretórios do Ubuntu 10.04 LTS foram excluídas do repositório de fontes oficial mais recente. Para estar alinhado com essa mudança, o repositório de software da Tencent Cloud encerrará o suporte ao Ubuntu 10.04 LTS na árvore oficial de diretórios de fontes. Assim, recomendamos que você atualize as suas imagens para uma versão posterior.

Para os usuários que pretendem continuar usando a fonte de software do Ubuntu 10.04, fornecemos suporte pelos seguintes métodos:

## Método 1: atualização manual do arquivo de configuração
Para melhor experiência do usuário, o repositório de software da Tencent Cloud extrai a fonte do arquivo oficial `http://old-releases.ubuntu.com/ubuntu/` do Ubuntu 10.04 LTS (http://old-releases.ubuntu.com/ubuntu/) para os usuários. Os usuários podem usar o repositório normalmente modificando o arquivo de configuração manualmente:

Abra o arquivo de configuração da fonte do apt `vi/etc/apt/sources.list` e modifique os seguintes trechos de código:

```
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid-updates main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid-security main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid-backports main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid-updates main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid-security main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid-backports main restricted universe multiverse
```

## Método 2: execução do script automatizado
Use o script [old-archive.run](http://ubuntu10-10016717.cos.myqcloud.com/old-archive.run) fornecido pela Tencent Cloud para configuração. Para acessá-lo, baixe o arquivo no CVM com o Ubuntu 10.04 e execute os seguintes comandos:

```
chmod +x old-archive.run
./old-archive.run
```