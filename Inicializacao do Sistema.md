# Inicializaçao do Sistema
Ordem:

1. **`BIOS`** - Basic Input/Output System. Inicia o MBR
2. **`MBR`** - Master Boot Record (Primeiros 512bytes do disco). Contem o Bootloader e a tabela de partiçoes. O Bootloader e o gerenciador de inicializador
3. **`Bootloader`** - O Bootloader e programa responsavel por carregar o Kernel. A maioria das distribuiçoes Linux utilzam o **GRUB** ( **GR**and **U**nified **B**ootloader) como bootloader.
4. **`Kernel`** - Carrega o Initrd ou Initramfs (FS carregado na RAM) que auxilia com arquivos necessarios para o Kernel  realizar a inicializaçao do sistema corretamente.
5. **`Init`** - Primeiro programa inicializado pelo Kernel. E reponsavel por iniciar outros programas/serviços.


> **Recuperando a senha do boot**
	> Dentro da entrada do Kernel no GRUB, adicionar o  parametro init no Kernel da seguinte forma: `init=/bin/bash rw`. 
	> Depois de logado, rodar comando `passwd`.

<br>

## Logs de Inicializaçao do Sistema

+ **`dmesg`** - Imprime o Kernel Ring Buffer. Informaçoes/log de inicializaçao do sistema
	+ `dmesg --color=always | less -R` - log colorido e paginado.
+ **`journalctl -k`** - Imprime as informaçoes de inicializaçao do sistema + logs do Kernel em si.
+ **`/var/log/kernel.log`** - Arquivo com os logs de inicializaçao do sistema.

<br>

## Gerenciadores de Inicializaçao do Sistema

### SysVinit
Trabalha com `runlevel`'s , que sao modulos que definem os programas/processos que eu quero executado no determinado *level*/nivel. Foi substituido, pois ele iniciava cada serviço sequencialmente, o que era devagar.


**Niveis**:
+ **`0`** : Desligado
+ **`1`** : Mono usuario
+ **`2`** : Multi usuario (Sem rede)
+ **`3`** : Multi usuario (Com rede)
+ **`4`** : Nao utilizado (Pode ser personalizado)
+ **`5`** : Multi usuario com interface grafica
+ **`6`** : Reboot

**Alguns arquivos/comandos de configuraçao:**
+ **`cat /etc/inittab`** : Arquivo de configuraçao do *runlevel* padrao
+ **`runlevel`** : Verificando o *runlevel* atual
+ **`init [runlevel]`** : Mudando os niveis
+ **`/etc/init.d/`** : Scripts de inicializaçao do SysVInit
+ **`/etc/rc[0-6].d/`** : Scripts relacionados ao *runlevel \[0-6\]* 
	+ Esses scritps sao executados quando o comando `init [0-6]` e invocado.
+ **`service [serviço] [opçao]`** : Comando para gerenciar serviços no SysVInit
+ **`telinit`** : Equivalente ao `init`, porem avisa o usuario sobre reboots e desligamentos.
	+ **`telinit -q`** : Recarrega as configuraçoes do /etc/inittab e notifica os usuarios logados sobre reboot e power off.

### Upstart
Gerenciador de inicialização desenvolvido para o Ubuntu em 2006 e tinha como vantagem inicializar os serviços/processos de maneira paralela.

### Systemd
Gerenciador de inicializaçao mais atual e utilizado. Utiliza de *runlevels* por motivos de compatibilidade, porem ele trabalha com **`target`**'s. Diferente do SysV e do Upstart, o Systemd nao utiliza de Shell Scritps, mas sim programas em C compilados. Dessa forma consegue alcançar uma velocidade maior de inicializaçao dos processos.

Scritps de inicializaçao do Systemd: **`/etc/systemd/system/`**

**Comandos basicos**
+ **`systemctl list-units`** : Lista as unidades configuradas.
+ **`systemctl get-default`** : Retorna o *target* padrao configurado.
+ **`systemctl set-default`** : Configura o *target* padrao.
+ **`systemctl isolate [target]`** : Muda o target em execuçao do sistema.
	+ `init 0` --> `systemctl isolate poweroff.target|shutdown.target`
	+ `init 1` --> `systemctl isolate rescue.target`
	+ `init 2|3|4` --> `systemctl isolate multi-user.target`
	+ `init 5`  --> `systemctl isolate graphical.target`
	+ `init 6` --> `systemctl isolate reboot.target`
+ **`systemctl start [nome_do_servico].service`** : Inicia um serviço.
+ **`systemctl stop [nome_do_servico].service`** : Para um serviço.
+ **`systemctl restart [nome_do_servico].service`** : Reincia um serviço. Para o serviço e o inicia novamente.
+ **`systemctl reload [nome_do_servico].service`** : Reincia um serviço. Apenas le os arquivos de configuraçao novamente.
+ **`systemctl enable [nome_do_servico].service`** : Habilita o serviço no boot se configurado.
+ **`systemctl disable [nome_do_servico].service`** : Retira o serviço da lista de serviços que inicializam com o sistema.
+ **`systemctl status [nome_do_servico].service`** : Imprime na tela o estado do serviço.

<br>
<br>
<br>

## Bootloaders
E o programa responsavel por carregar o Kernel e assim inicializar o sistema. Fica instalado entre o MBR e a primeira partiçao do disco.

+ **`/boot/`** : Caminho onde se encontra arquivos de boot;
	+ **`/boot/config-[versao]-[arch]`** : Arquivo te texto que contem informaçoes/parametros de compilaçao do Kernel. Esse arquivo e gerado quando o Kernel e compilado;
	+ **`/boot/vmlinuz-[versao]-[arch]`** : Arquivo de imagem do Kernel;
	+ **`/boot/System.map-[versao]-[arch]`** : 
	+ **`/boot/initrd.img-[versao]`** : Arquivo que contem a imagem do pseudo FS que e carregado na RAM durante a inicializaçao do sistema. Contem utilitarios que auxiliam o Kernel a inicializar o sistema.

Comandos do Terminal do GRUB (2 e Legacy)

+ **`root (hd0,0)`** - partiçao onde se encontra o diretorio `/boot/`
+ **`setup (hd0)`** - disco sera instalado o GRUB
+ **`ls`** : lista os discos e file systems.
	+ **`ls [dev]`** : lista arquivos de disco;
+ **`set [param]=[value]`** : Utilitario que pode ser utilizado para alterar parametros de configuraçao. Os parametros sao os mesmos utilzados nos arquivos do sistema.
+ **`set root [particao]`** : Define a partiçao que possui o diretorio */boot/* que do Kernel que sera inicializada.

<br>

### GRUB Legacy

+ **`/boot/grub/menu.lst`** : Arquivo de configuraçao do GRUB Legacy. Possui os 
+ **`grub-install [DEVICE]`** : Utilitario para realizar a instalaçao do GRUB legacy em um dispisitvo selecionado. 
	+ Exemplo: `grub-install /dev/sda`
+ **`update-grub`** : Utilitario usado para reler as configuraçoes e gerar um novo arquivo de configuraçao.

<br>

#### Representaçao dos Discos

**`HD(X,Y)`** - **H**ard **D**isk; **X** representa o disco e **Y** representa a partiçao.

**Exemplo:** `(hd0,0)` - Primeiro disco, primeira partiçao

> Nota: A numeraçao dos discos e das partiçoes começam em 0.

<br>

#### Exemplo Arquivo de Configuraçao
Como adicionar um Kernel novo no GRUB Legacy: 

**Exemplo:**
```
# Adicionar no /boot/grub/menu.lst

title "Debian 10"		# Define o nome que aparece no menu
root (hd0,0) 			# Define a partiçao onde esta a partiçao /boot
kernel /boot/vmlinux-5-11.0-16-46-generic ro root=/dev/sda5
initrd /boot/initrd-5-11.0.46-generic
default=0				# Define o Kernel padrao sera utilizado
Timeout=15				# Timeout em segundos ate ele inicilizar o Kernel padrao
							# 0 : Nao mostra o menu de escolha
							# -1 : Mantem o menu indefinidamente
```

<br>

### GRUB 2

#### Instalando o GRUB atraves do Terminal do GRUB

<br>

#### Comandos e Diretorios 
+ **`/boot/grub2/grub.cfg`** : Arquivo de configuraçao do GRUB2. Esse arquivo e gerado atraves da leitura de outros arquivos e nao deve ser editado.	
	+ **`/etc/grub.d/`** : Diretorio que contem scripts que sao lidos para gerar o arquivo de configuraçao do GRUB 2
	+ /etc/grub.d/40_custom
	+ **`/etc/default/grub`** : Arquivo semelhante ao `/boot/grub/menu.lst` do GRUB Legacy. Possui configuraçoes do GRUB.
		+ Algumas configuraçoes importantens:
			+ `GRUB_DEFAULT` : Define o Kernel padrao do sistema. Pode ser especificado pela ordem numerica  (0 a N) ou pelo nome do titulo.
			+ `GRUB_SAVEDEFAULT` : Se marcado com *true*,  ele sempre vai selecionar o ultimo Kernel selecionado como padrao;
			+ `GRUB_TIMEOUT` :  Define o tempo de espera que o menu do GRUB fica disponivel;
			+ `GRUB_CMDLINE_LINUX` : Parametros passados ao Kernel;

+ **`grub2-install [DEVICE]`** : Utilitario para realizar a instalaçao do GRUB 2 em um dispisitvo selecionado. 
	+ Exemplo: `grub2-install /dev/sda`
 + **`grub2-mkconfig -o /boot/grub2/grub.cfg`** : Gera um arquivo de configuraçao baseado em um arquivo editado.
 
<br>

#### Exemplo Arquivo de Configuraçao
Como adicionar um Kernel novo no GRUB 2:

```
# Adicionar no /etc/grub.d/40_custom
# ou no /etc/default/grub (nao recomentado)

# Entrada de Kernel
menuentry "Debian 10" {
			set root=(hd0,1)
			linux /boot/vmlinuz root=/dev/sda1 ro quiet splash
			initrd /boot/initrd.img
		}
```

<br>

#### Representaçao dos Discos

**`HD(X,Y)`** - **H**ard **D**isk; **X** representa o disco e **Y** representa a partiçao.

**Exemplo:** `(hd0,1)` - Primeiro disco, primeira partiçao

> Nota: A **numeraçao dos discos** **começa em 0** e das **partiçoes** começam **em 1**.

<br>
<br>
<br>

## Desligando e Reiniciando o Sistema
### Comandos
+ **`shutdown`** : Desliga a maquina em 1 min (valor padrao).
	+ **`shutdown -c`** : Cancela o deseligamento da maquina.
	+ **`shutdown -r`** : Reinicia a maquina.
	+ **`shutdown -r +10`** : Reinicia a maquina depois de 10 minutos
	+ **`shutdown -h`** : Desliga a maquina porem deixando o hardware energizado. Depende de hardware.
	+ **`shutdown -[p|c|r|h] now`** : Executa a açao na hora
	+ **`shutdown -P HH:MM`** : Desliga a maquina no horario especificado.
+ **`init 0`** : Desliga a maquina.
+ **`init 6`** : Reinicia a maquina.
+ **`systemctl isolate shutdown.target`** : Desliga a maquina.
+ **`systemctl isolate reboot.target`** : Reincicia a maquina.
+ **`halt`** :  Desliga a maquina porem deixando o hardware energizado. Depende de hardware.
+ **`poweroff`** :  Desliga a maquina.

<br>

### ACPI
**A**dvanced **C**onfiguration and **P**ower **I**nterface e uma especificaçao que fornece um padrao aberto para a configuraçao de dispositivos e gerenciamento de energia pelo sistema operacional.

`acpid` : Daemon que faz o gerenciamento de energia da maquina. Exemplo: apertar o botao de desligar, a maquina entrar em hibernaçao depois de um tempo etc.

<br>

