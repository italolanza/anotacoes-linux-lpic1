## Comandos basicos


+ **`pwd`** : *Print Working Directory*, imprime na tela o diretorio atual.
+ **`hostname`** : Imprime o hostname da maquina.
	+ **`hostname -i`** : Imprime o *IP* da maquina.
+ **`whoami`** : Imprime o nome do usario que voce esta logado no momento.
+ **`su`** : *Switch User*. Comando para trocar de usuario.
	+ `su [nome_do_usario]`
+ **`ls`** : Lista o conteudo de um diretorio
	+ `ls -a` :  Lista todos arquivos de um diretorio, incluindo arquivos ocultos
	+ `ls -l` : Lista os arquivos de um diretorio de maneira longa (com metadados).
+ **`cd [caminho/diretorio]`** : *Change directory*, muda o diretorio de trabalho.
	+ **`cd -`** : Volta para o diretorio anterior.
+ **`mkdir [nome_do_diretorio]`** : *Make Directory*. Comando usado para criar diretorios.
+ **`touch [/caminho/nome_do_arquivo]`** : Utilizado para editar metadados de um arquivo. Caso o arquivo nao exista, um arquivo com o nome sera criado.
+ **`more, less [nome_do_arquivo]`** : Paginadores de saida. `less` e o sucessor do `more`.
+ **`head [nome_do_arquivo]`** : Imprime as primeiras linhas de um arquivo. Por padrão, as 10 primeiras linhas.
+ **`tail [nome_do_arquivo]`** Imprime as linhas finais do arquivo. Por padrão, as 10 ultimas linhas.
	+ `tail -f [nome_do_arquivo]` : usado para imprimir as ultimas linhas do arquivo e continua conforme o arquivo for crescendo.
+ **`rm [caminho/nome_do_arquivo]`** : Remove/deleta o arquivo.
+ **`mv [caminho/origem/arquivo] [caminho/destino/arquivo]`** : Utilizado para mover arquivo de um caminho de origem para um caminho de destino renomeando o arquivo. Pode ser utilizado para renomear uma arquivo.
+ **`cp [caminho/origem/arquivo] [caminho/destino/arquivo]`** : Utilizado para copiar um arquivo de um diretorio de origem para um diretorio de destino alterando o nome.
+ **`history`** : Imprime na tela a sequencia de comandos executados previamente no terminal.
+ **`man [nome_do_comando]`** : Armazena documentaçao dos comandos (e alguns arquivos de configuraçao) offiline.
+ **`wall`** : Manda mensagens para todos os usuarios
+ **`write [user] [tty]`** : Manda mensagem para um usuario em especifico
+ **`xxd`** : Make a hexdump or do the reverse.
+ **`hexdump`** : Display file contents in hexadecimal, decimal, octal, or ascii