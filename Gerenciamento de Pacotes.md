# Gerenciamento de Pacotes
**Gerenciadores de pacotes**: sao utilitarios que fazem o controle dos pacotes e outros utilitarios instalados no sistema.

<br>

## Debian

### Gerenciadores de Baixo Nivel

#### DPKG (Debian Package)
Faz a gestao (remoçao, instalaçao e atualizaçao) de pacotes que ja estao na maquina.

**Comando: ** **`dpkg`**

+ **`dpkg -i`** : instala pacotes com extençao **`.deb`**;

>  O `dpkg` nao resolve dependecias/biblitoecas. Ou seja, caso um pacote que possui dependencias nao cumpridas ele nao permite a instalaçao do mesmo.

+ **`dpkg -i [nome_pacote].deb --force-all`** -> força a instalaçao do pacote mesmo que falta dependencias;
+ **`dpkg -r [nome_pacote]`** -> remove o pacote;
+ **`dpkg -P [nome_pacote]`** -> remove o pacote e seus arquivos de configuraçao;
+ **`dpkg -I [nome_pacote].deb`** -> coleta informaçoes sobre um pacote;
+ **`dpkg -l`** -> lista todos os pacotes instalados na maquina;
+ **`dpkg -L [nome_pacote]`** -> arquivos relacionados ao pacote (ja instalado);
+ **`dpkg-reconfigure [nome_pacote]`** -> serve para alterar configuraçoes de um pacote.

<br>

### Gerenciadores de Alto Nivel

#### APT (Advanced Package Tools)
Consegue fazer a instalaçao de pacotes que nao necessariamente estao na maquina. Para isso, ele procura pelo pacote em servidores externos configurados previamente. Depois de feito o download, o **apt** usa o **dpkg** para realizar a instalaçao dos pacotes. Podemos pensar no apt como um *frontend* para o dpkg.

**Arquivos de configuraçao:**
+ **`/etc/apt/sources.list`** -> arquivo de configuraçao onde sao guardados os servidores usados para busca de pacotes. E o princial arquivo de configuraçao do apt
	+ **`deb-src`** -> URL para o repositorio usado para baixar codigos fontes;
	+ **`buster`** -> URL para o repositorio de versoes estaveis. Esse nome muda com cada versao;
	+ **`main`** -> sessao principal do repositorio;
	 


**Comandos** 

+ **`apt-get`** -> utilizario usado para baixar, instalar, atualizar e remover pacotes;
	+ **`apt-get install [nome_pacote]`** -> baixa (se necessario) e instala o pacote;
		+ **`apt-get install -f | --fix-broken install`** -> resolve problemas de dependecias dos pacotes instalados;
		+ **`apt-get install [nome_pacote] --download-only`** -> Faz apenas o download do pacote. O mesmo pode ser encontrado em `/var/cache/apt/archives`;
	+ **`apt-get remove [nome_pacote]`** ->  remove o pacote(s);
	+ **`apt-get purge [nome_pacote]`** -> remove o pacote(s) e tambem seus arquivos de configuraçao;
	+ **`apt-get update`** -> utilitario que atualiza a lista de pacotes (local) com base nos repositorios listados no arquivo de configuraçao (`/etc/apt/sources.list`);
	+ **`apt-get upgrade`** -> atualiza os pacotes para ultima versao disponivel listada nos repositorios configurados;
	+ **`apt-get clean`** -> limpa o cache do apt (`/var/cache/apt/archives`);
+ **`apt-file`** -> utilitario para buscar arquivos dentro dos pacotes;
	+ **`apt-file list [nome_pacote]`** -> lista todos os arquivos relacionados ao pacote;
	+ **`apt-file search [nome_arquivo]`** -> mostra o pacote ao qual esse arquivo esta relacionado;
+ **`apt-cache`** -> utilitario para executar opraçoes como pesquisas no indice do pacote;
	+ **`apt-cache search`** -> pesquisa por um pacote;
	+ **`apt-cache search [nome/descricao_do_pacote]`** -> procura por um pacote pelo seu nome ou por sua descriçao
	+ **`apt-cache show [nome_pacote]`** -> mostra a descriçai detalhada do pacote;








