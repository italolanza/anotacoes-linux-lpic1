# System Architecture
----

## Informaçoes do Sistema

### `/proc/`
+ **`/proc/uptime`** :  Possui as informaçoes de quanto tempo a maquina esta ligada.
	+ **`uptime`** : Comando/Utilitario que apresenta as informaçoes de maneira mais amigavel

+ **`/proc/cpuinfo`** : Armazena informaçoes a respeito do processador (CPU) da maquina.

+ **`/proc/cmdline`** : Armazena informaçoes a respeito dos parametros passsados ao Kernel durante o boot (so é alimentado).

+ **`/proc/meminfo`** : Armazena informaçoes a respeito da memoria da maquina.

+ **`/proc/partitions`** : Armazena informaçoes a respeito das partiçoes disponiveis.
	+ **`lsblk`** : Utilitario que apresenta as informaçoes das partiçoes de maneira mais amigavel.

+ **`/proc/version`** : Armazena a informaçoes a respeito da versao do Kernel.

+ **`/proc/interrupts`** : Armazena informaçoes de IRQs. Informaçoes de requisiçoes de interrupçoes.

+ **`/proc/ioports`** : Armazena informaçoes a respeito de todas as portas de entrada e saida de dados.

<br>

### `/sys/`
Pseudo filesystem que armazena informaçoes de baixo nivel do sistema. Exemplo: informaçoes a respeito do Kernel e de seus modulos.


<br>

### `/dev/`
Diretorio que mapeia os dispositivos reconhedidos pelo `udev`.  Essas informaçoes recebidas atraves do `D-Bus`.

+ **`udev`** - deamon que roda na maquina e gerencia os dispositivos no linux. Ele manda informaçoes para o D-Bus que 
+ **`D-Bus`** : E um mecanismo de [comunicação entre processos](https://pt.wikipedia.org/wiki/Comunica%C3%A7%C3%A3o_entre_processos) (CIP) e [chamada de procedimento remoto](https://pt.wikipedia.org/wiki/Chamada_de_procedimento_remoto) que possibilita a comunicação entre vários [programas de computador](https://pt.wikipedia.org/wiki/Programas_de_computador "Comunicação entre processos") (isto é, [processos](https://pt.wikipedia.org/wiki/Processo_(computa%C3%A7%C3%A3o))) rodando simultaneamente na mesma máquina.


<br>

## Kernel
Responsavel por gerenciar os recursos do hardware para os processos. O kernel possui **modulos** que extendem as funcionalidades mesmo. Exemplo: drivers.


+ **`uname`** : Utilitario que imprime informaçoes a respeito do Kernel do sistema.
	+ **`uname -r`** : Imprime a informaçao do release
	+ **`uname -a`** : Imprime todas as informaçoes.
+ **`lsmod`** : Lista todos os modulos de kernel carregados em memoria.
+ **`modinfo [nome_do_modulo]`** : *Modules Informations*. Lista informaçoes a respeito de algum modulo do sistema.
+ **`modprobe [nome_do_modulo]`** : Utilitario capaz de habilitar e desabilitar modulos do kernel.
	+ **`modprobe -r [nome_modulo]`** : Desabilita um modulo carregado.
+ **`insmod [caminho/modulo]`** : *Install Modules*. Utilitario que permir instalar modulos do sistema.

### Parametros do Kernel
+ **`sysctl`** : Utilitario do sistema que permite alterar parametros de Kernel em runtime
+ **`sysctl -a`** : Mostra todos parametros do Kernel disponiveis


<br>

## Dispositivos

+ **`lspci`** : Lista dispositivos conectados ao barramento PCI.
+ **`lsusb`** : Lista dispositivos conectados ao barramento USB.
+ **`lscpu`** : Lista informaçoes a respeito das cpus.
+ **`lsblk`** : Lista informaçoes a respeito dos dispositivos de bloco.
+ **`lsmem`** : Lista dispositivos de memoria.


