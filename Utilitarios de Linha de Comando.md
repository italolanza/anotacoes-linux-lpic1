

## Comandos Basicos

+ **`pwd`** : *Print Working Directory*, imprime na tela o diretorio atual.	
+ **`touch [/caminho/nome_do_arquivo]`**: Utilizado para editar metadados de um arquivo. Caso o arquivo nao exista, um arquivo com o nome sera criado.
+ **`uname`** : Imprime na tela informaçoes a respeito do Kernel.
	+ `uname -a`: Imprime todas informaçoes do Kernel (nome e versao).
+ **`man [nome_do_comando]`** : Imprime informaçoes de documentaçao (se existir) do comando (e alguns arquivos de configuraçao) offiline.
+ **`ls`** : Lista o conteudo de um diretorio
	+ `ls -a` :  Lista todos arquivos de um diretorio, incluindo arquivos ocultos
	+ `ls -l` : Lista os arquivos de um diretorio de maneira longa (com metadados).
+ **`hostname`** : Imprime o hostname da maquina.
	+ **`hostname -i`** : Imprime o *IP* da maquina.
+ **`whoami`** : Imprime o nome do usario que voce esta logado no momento.
+ **`su`** : *Switch User*. Comando para trocar de usuario.
	+ `su [nome_do_usario]`
+ **`which [comando`** : Imprime apenas o caminho absoluto do comando. Nota:  Comandos built-in, (exemplo cd), sao armazenados na memoria.
+ **`type [comando]`** : Imprime o caminho absoluto do comando e tambem se o comando foi usado recentemente.
+ **`whereis [comando]`** : Imprime o caminho absoluto do comando e o caminho para sua documentaçao.
+ **`help [comand_builtin]`** : Imprime informaçoes de ajuda de comandos builtin do bash.
+ **`history`** : Imprime na tela a sequencia de comandos executados previamente no terminal. Todo comando rodado com um espaço previamente nao e salvo no history.
	+ `history -c` : Limpa todas as entradas do *history*.	
+ **`export [var_name]`** : transforma uma variavel local em uma variavel de ambiente.
+ **`set`** : Lista todas variaveis e funçoes definidas no sistema.
+ **`env`** : Lista todas variaveis de ambiente.
+ **`unset [var_name]`** : Apaga variaveis locais

<br>

## Outros Utilitarios

+ **`file [arquivo]`** : Imprime informaçoes a respeito de um arquivo.
+ **`apropos [padrao]`** : Semelhando ao `man -k`, procura na descriçao dos comandos das paginas do *man* que cotenha o termo/padrao pesquisado.
+ **`cd [caminho/diretorio]`** : *Change directory*, muda o diretorio de trabalho.
	+ **`cd -`** : Volta para o diretorio anterior.
+ **`mkdir [nome_do_diretorio]`** : *Make Directory*. Comando usado para criar diretorios.
+ **`more, less [nome_do_arquivo]`** : Paginadores de saida. `less` e o sucessor do `more`.
+ **`head [nome_do_arquivo]`** : Imprime as primeiras linhas de um arquivo. Por padrão, as 10 primeiras linhas.
+ **`tail [nome_do_arquivo]`** Imprime as linhas finais do arquivo. Por padrão, as 10 ultimas linhas.
	+ `tail -f [nome_do_arquivo]` : usado para imprimir as ultimas linhas do arquivo e continua conforme o arquivo for crescendo.
+ **`rm [caminho/nome_do_arquivo]`** : Remove/deleta o arquivo.
+ **`mv [caminho/origem/arquivo] [caminho/destino/arquivo]`** : Utilizado para mover arquivo de um caminho de origem para um caminho de destino renomeando o arquivo. Pode ser utilizado para renomear uma arquivo.
+ **`cp [caminho/origem/arquivo] [caminho/destino/arquivo]`** : Utilizado para copiar um arquivo de um diretorio de origem para um diretorio de destino alterando o nome.
+ **`wall`** : Manda mensagens para todos os usuarios.
+ **`write [user] [tty]`** : Manda mensagem para um usuario em especifico
+ **`xxd`** : Make a hexdump or do the reverse.
+ **`hexdump`** : Display file contents in hexadecimal, decimal, octal, or ascii.
+ **`ccze [/caminho/arquivo/log]`** : A robust log colorizer.


<br>

## Variaveis Uteis

+ **`$_`** : Variavel de ambiente que armazena o parametro do uiltimo comando executado.
+ **`$?`** : Variavel que armazena o return code do ultimo comando executado.
+ **`$PS1`** : Variavel local que armazena as primeiras informaçoes do bash antes do comando.
	+ Exemplo: `<user>@<host_name>$ [comando]`
+ **`$HISTTIMEFORMAT`** : Se configurada, adiciona informaçoes de data e tempo no historico de comandos rodados.
	+ Exemplo: `HISTTIMEFORMAT='%F %T'` : Adiciona data e hora no historico dos comandos executados
+ **`HISTSIZE`** : Define o tamanho maximo de linhas mostrada pelo comando *`history`*.
+ **`HISTFILESIZE`** :  Define a quantidade maxima de linhas que sera armazenada no arquivo *bash_history*.