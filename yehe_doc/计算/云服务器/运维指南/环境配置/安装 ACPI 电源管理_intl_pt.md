## Introdução

As máquinas x86 usam dois métodos de gerenciamento de energia, o **APM** (Gerenciamento avançado de energia) e o **ACPI** (Configuração avançada e interface de energia). O ACPI é um padrão de gerenciamento de energia desenvolvido em conjunto pela Intel, Microsoft e Toshiba, que fornece uma interface mais flexível para gerenciamento de computador e dispositivo, já o APM é o antigo padrão de gerenciamento de energia.
O Linux aceita o APM e o ACPI, mas os dois padrões não podem ser executados simultaneamente. O Linux executa o ACPI por padrão. O Tencent Cloud também recomenda o ACPI. 
Se o ACPI não estiver instalado em um sistema Linux, o desligamento normal falhará. Este documento descreve como verificar se o ACPI foi instalado e, se não tiver sido, como instalá-lo.

## Observações

Para o CoreOS, não há necessidade de instalar o ACPI.

## Instruções
 
1. Execute o comando a seguir para verificar se o ACPI foi instalado.
```
ps -ef|grep -w "acpid"|grep -v "grep"
```
 - Se não houver nenhum processo em execução, significa que o ACPI não foi instalado. Vá para a próxima etapa.
 - Se houver um processo em execução, significa que o ACPI foi instalado.
2. Execute o comando a seguir para instalar o ACPI.
 - Para Ubuntu ou Debian:
```
sudo apt-get install acpid
```
 - Para Redhat ou CentOS:
```
yum install acpid
```
 - Para SUSE:
```
in apcid
```
