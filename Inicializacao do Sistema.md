# Inicializaçao do Sistema
Ordem:

1. **`BIOS`** - Basic Input/Output System. Inicia o MBR
2. **`MBR`** - Master Boot Record (Primeiros 512bytes do disco). Contem o Bootloader e a tabela de partiçoes. O Bootloader e o gerenciador de inicializador
3. **`GRUB`** - GRand Unified Bootloader, responsavel por carregar o Kernel.
4. **`Kernel`** - Carrega o Initrd ou Initramfs (FS carregado na RAM) que auxilia com arquivos necessarios para o Kernel  realizar a inicializaçao do sistema corretamente.
5. **`Init`** - Primeiro programa inicializado pelo Kernel. E reponsavel por iniciar outros programas/serviços.
6. **`RunLevel`** - 

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