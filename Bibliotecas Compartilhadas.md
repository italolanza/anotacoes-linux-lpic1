# Bibliotecas Compartilhadas
Bibliotecas sao um conjunto de pedaços de codigo pre-compilado que podem ser reutilizados por outros programas.

Bibliotecas compartilhadas são bibliotecas carregadas por programas quando eles iniciam. Quando uma biblioteca compartilhada é instalada corretamente, todos os programas iniciados posteriormente usam a nova biblioteca compartilhada. 

<br>

## Convensao de Nomenclatura
Toda bibliotecas compartilhadas no Linux devem seguir um padrao de nomenclatura `[lib_name].so.[versao]`.


**Exemplo:** `libc.so.3.45`

<br>

## Diretorios

Local onde ficam armazenados bibliotecas essenciais do sistema:
+ **`/lib/`**
+ **`/lib32/`**
+ **`/lib64/`**

Local onde ficam armazenadas bibliotecas secundarias:
+ **`/usr/lib/`**
+ **`/usr/local/lib/`**

Outros diretorios e arquivos
+ **`/etc/ld.so.conf`** : Arquivo de configuraçao dos caminhos das bibliotecas
+ **`/etc/ld.so.conf.d`** : Diretorio com arquivos dos caminhos das das bibliotecas
+ **`ldconfig`** : Faz a releitura dos arquivos que armazenam os caminhos da bibliotecas
+ **`ldd [path/to/bin]`** : Imprime as dependencias de um executavel/binario
+ **`LD_LIBRARY_PATH`** : Variavel de ambiente que armazena caminhos possiveis para bibliotecas