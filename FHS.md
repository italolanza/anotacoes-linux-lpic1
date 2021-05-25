# **F.H.S** -> **F**ilesystem **H**ierarchy **S**tandard
Define os principais diretorios, e o seu conteudo, em um sistema operacional Linux ou do tipo Unix.


## Tipos de arquivos

+ **`-`** : arquivo de texto comum;
+ **`d`** : arquivo de diretorio. Arquivo que armazena metadados de outros arquivos (dados de endereçamento);
+ **`l`** : arquivo de link simbolico. Link/atalho para um outro arquivo no FS;
+ **`c`** : arquivo de caracteres (exemplo: teclado, mouse);
+ **`b`** : arquivo de bloco. Dispositivos de bloco (exemplo: pendrive, hds), gravam dados persistentes no sistema.

<br>

## Estutura de diretorios padrão

+ **`/`** : Raiz do sistema. Todos diretórios são filhos do root
+ **`/bin/`** : Contem binarios excenciais que podem ser executados por usuarios comuns.
+ **`/sbin/`** : System Binaries (Binarios do Systema). Binarios que podem ser executados apenas pelo usuario *root*.
+ **`/boot/`** :  Arquivos necessarios para a inicialização do sistema.
+ **`/etc/`** : Diretorio que armazena arquivos de configuração de programas e serviços da máquina.
+ **`/home/`** : Armazena diretorios pessoais dos usuários (execeto root).
+ **`/root`** : *Home* do usuario root.
+ **`/lib/`** : Diretorio onde bibliotecas sao armazenadas.
+ **`/media/`** :  Ponto de montagem temporario para midias removiveis.
+ **`/mnt`** : Ponto de montagem de FileSystems temporario.
+ **`/opt/`** : Optional Files. Arquivos opcionais para o funcionamento do sistema.
+ **`/tmp/`** : Armazena arquivos temporarios.
+ **`/var/`** : Armazena arquivos variaveis. Arquivos sao alterados durante o andamento do sistema sem intervençao do usuario.
+ **`/usr/`** : *Unix System Resources*. Arquivos nao necessarios para a inicializaçao e manutençao do sistema.
+ **`/dev/`** : *Devices*. Diretorio que armazena arquivos de dispositivos (periféricos em geral) (PSEUDO FILESYSTEM).
+ **`/proc`** : *Process*. Mapeia os processos que estão rodando na maquina.  Os diretorios dentro desse diretorio representam os PIDs (Process ID) dos processos em execuçao.  Alem disso, possiu arquivos de configuraçoes com alguns dados importantes
+ **`/sys`** :  *System Information*. Armazena informaçoes do sistema enquanto ele esta em execuçao.