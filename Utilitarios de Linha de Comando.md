

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
+ **`unset [var_name]`** : Apaga variaveis locais.

<br>


## Filtros de Texto

+ **`cat </caminho/arquivo>`** : Imprime arquivos na saida padrao do sistema de maneira sequencia.
	+ `cat -n </caminho/arquivo>` : Imprime o arquivo numerando as linhas.
+ **`zcat`** : Variaçao do *cat* para imprimir textos comprimidos em `gzip`.
+ **`bzcat`** : Variaçao do *cat* para imprimir textos comprimidos em `bzip2`.
+ **`xzcat`** : Variaçao do *cat* para imprimir textos comprimidos em `xz`.
+ **`cut`** : Utilitario que permite separar/cortar a saida baseado em delimitadores. Por padrão, utiliza *tab*.
	+ **`cut -d "[delimitador] -f [Começo],[FIM]"`** : Recorta apenas os campos *começo* e *fim* utilizando o *delimitador* escolhido.
+ **`tr`** : Transforma uma saida traduzindo, espremendo e ou deletando caracteres a partir da entrada padrao.
	+ `tr -s "[caracter]"` : Espreme todos os caracteres repetidos.
		+ **Exemplo:** `cat /etc/passwd | cut -d ":" -f 1`
+ **`head [/caminho/arquivo]`** : Imprime as 10 primeiras linhas de um arquivo.
+ **`tail [/caminho/arquivo]`** : Imprime as 10 últims linhas de um arquivo
	+ **`tail -f [/caminho/arquivo]`** : Imprime as ultimas 10 linhas do arquivo e continua imprimindo linhas conforme o arquivo for atualizado. Bom para seguir logs.
	+ **`tail -n[quantidade] [/caminho/arquivo]`** : Imprime as ultimas *n* linhas do arquivo.
+ **`less [caminho/arquivo]`** : Paginador
+ **`nl [caminho/arquivo]`** :  Escreve em um arquivo numerando as linhas. Semelhante ao `cat -n`.
	+ `nl -b [caminho/arquivo]` : Enumera também linhas em branco.
+ **`od`** : *Octal dump*, imprime na saida padrao (ou em um arquivo) a representaçao do mesmo octal (ou outros formatos). 
+ **`paste`** : Escreve na saída linhas separadas por um delimitador. Cada coluna e composta pela linha de um arquivo.
+ **`split [caminho/arquivo]`** : Utilitario que divide um arquivo em varios com tamanho especifico. Voce consegue tambem definir um prefixo para o nome.
	+ **Exemplo** : `split -b 100M arquivo`
		+ A opçao `-b` serve para definir o tamanho em bytes dos arquivos gerados.
	+ **Exemplo** : `split -n 5 arquivo`
		+ A opçao `-n` serve para definir a quantidade de arquivos gerados.
+ **`sort [nome/arquivo]`** : Ordena um arquivo (ou stream) seguindo um criterio. Por padrao, ordem alfabetica.
+ **`uniq`** : Utilitario que permite suprimir caracteres ou linhas repetidas.
+ **`wc`** : *Word count*, contabiliza linhas, palavras e caracteres de um arquivo.
+ **`sed`** : Utilitario manipulador de textos em arquivos (ou streams).
	+ **Exemplo** : `sed -i 's/suporte/batata/g'` 
		+ Substitui a palavra "suporte" por "batata" e todas as ocorrencias na mesma linha.
+ **`md5sum [caminho/arquivo]`** : Gera uma hash dado um arquivo.
+ **`sha256sum [caminho/arquivo]`** : Gera uma hash dado um arquivo.
+ **`sha512sum [caminho/arquivo]`** : Gera uma hash dado um arquivo.

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