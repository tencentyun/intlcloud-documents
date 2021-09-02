O TencentOS Server (também conhecido como Tencent Linux, TS ou Tlinux) é o sistema operacional Linux da Tencent projetado para cenários em nuvem. Com funcionalidades especializadas e desempenho otimizado, o TencentOS Server oferece um ambiente operacional de alto desempenho, seguro e confiável para aplicativos em instâncias do Cloud Virtual Machine (CVM). O TencentOS Server é gratuito e os aplicativos desenvolvidos no CentOS e outras distribuições podem ser executados diretamente no TencentOS Server. Além disso, o Tencent Cloud oferece atualizações, manutenção e suporte técnico de forma contínua.

## Casos de uso

O TencentOS Server pode ser usado nos seguintes cenários:

- O TencentOS Server é adequado para instâncias da maioria dos tipos de CVM.
- Ao iniciar instâncias, usa-se o TencentOS Server para transferir as operações relacionadas ao cloud-init (iniciador de nuvem) por meio de dados do usuário (o campo userdata) para permitir a configuração dinâmica.

## Apresentação do TencentOS Server 2.4

### Ambiente do usuário

Os pacotes de software do modo de usuário são compatíveis com o CentOS 7 mais recente, que pode ser usado diretamente no TencentOS Server 2.4.

### Serviços do sistema e configurações de otimização

#### Serviços do sistema

- `tlinux-irqaffinity`: o serviço de afinidade IRQ do TencentOS Server.
- `tlinux-bootlocal`: o serviço de bootlocal do TencentOS Server. Ele será iniciado após a execução automática do script `/etc/rc.d/boot.local` na inicialização.

#### Ferramentas do sistema

`tencent-tools`: os comandos tos (t) usados para o gerenciamento do sistema. Os parâmetros compatíveis são os seguintes:

```bash
tos version 2.2
Usage:
	tos TencentOS Server System Management Toolset
	tos -u|-U| update [rpm_name]Update the system 
	tos -i|-I| install rpm_name	install rpms
	tos -s|-S| showShow the system version
	tos -c|-C| check [rpm_name]Check the modified rpms
	tos -f yum | fix yumFix yum problems
	tos -f dns | fix dnsFix DNS problems
	tos -a|-A | analyzeAnalyze the system performance 
	tos set dns			Set DNS
	tos set irqSet irqaffinity, restart irqaffinity service
	tos -cu| check-updateCheck available package updates
	tos -b|-B| backup [ reboot ]Backup the system online, or reboot to backup 
	tos -r|-R| recover|reinstallRecover or Reinstall the system
	tos -h|-H| helpShow this usage
	tos -v|-V| versionShow the script version
```

#### Configurações do sistema

- **pam**: define uma política de senha segura.
- **modifying `/etc/bashrc`**: otimiza a exibição do bash ("Bourne-Again Shell", interpretador de comando).
- **`/etc/hosts`**: adiciona o TENCENT64 e o TENCENT64.site.
- **`/root/.bashrc`**: otimiza a configuração.

#### Kernel do TencentOS Server 2.4

O TencentOS Server 2.4 usa o longterm kernel 4.14 (de longo prazo) da comunidade do kernel. Para obter mais informações, consulte o [TencentOS-kernel](https://github.com/Tencent/TencentOS-kernel).


## Aquisição do TencentOS Server

Você pode adquirir e usar o TencentOS Server por meio dos seguintes métodos:

- Ao criar uma instância do CVM, selecione **Public Image (Imagem pública)** e a versão correspondente do TencentOS Server.
  Para obter mais informações, consulte [Criação de instâncias pela página de aquisição do CVM](https://intl.cloud.tencent.com/document/product/213/4855).
- Para as instâncias atuais do CVM, é necessário reinstalar o sistema operacional do TencentOS Server.
  Para obter mais informações, consulte [Reinstalação do sistema](https://intl.cloud.tencent.com/document/product/213/4933).

## Notas de versão

| Data de lançamento      | Tag da imagem                                                    | Descrição                                                  |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 17 de setembro de 2019 | TencentOS Server 2.4, conhecido anteriormente como Tencent Linux versão 2.4 (final) | ID da imagem: img-hdt9xxkt<br>Versão do kernel: 4.14.105<br>Região: todas as regiões |


## Suporte técnico

O Tencent Cloud fornece o seguinte suporte técnico para o TencentOS Server:

- O Tencent Cloud fornece atualizações de segurança no repositório YUM. Você pode executar o comando `yum update` para atualizar o TencentOS Server para a versão mais recente.
- O TencentOS Server é uma imagem de sistema operacional projetada para cenários em nuvem. Ele é baseado na versão 4.14.105 do kernel, que há muito tempo tem sido mantida pela comunidade do kernel. Se necessário, o Tencent Cloud fornecerá assistência técnica para ajudar você a solucionar quaisquer problemas que encontrar durante a utilização do TencentOS Server.
