# Gerenciamento de Pacotes
**Gerenciadores de pacotes**: sao utilitarios que fazem o controle dos pacotes e outros utilitarios instalados no sistema.

<br>

## Debian
----

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
Consegue fazer a instalaçao de pacotes  (e suas dependencias) que nao necessariamente estao na maquina. Para isso, ele procura pelo pacote em servidores externos configurados previamente. Depois de feito o download, o **apt** usa o **dpkg** para realizar a instalaçao dos pacotes. Podemos pensar no apt como um *frontend* para o dpkg.

**Arquivos de configuraçao:**
+ **`/etc/apt/sources.list`** -> arquivo de configuraçao onde sao guardados os servidores usados para busca de pacotes. E o princial arquivo de configuraçao do apt
	+ **`deb-src`** -> URL para o repositorio usado para baixar codigos fontes;
	+ **`buster`** -> URL para o repositorio de versoes estaveis. Esse nome muda com cada versao;
	+ **`main`** -> sessao principal do repositorio;
 + **`/etc/apt/sources.list.d/`** -> contem arquivos de configuraçao dos repositorios. Separa a configuraçao de cada repositorio em arquivos diferentes;


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
	+ **`apt-cache search [nome/descricao_do_pacote]`** -> procura por um pacote pelo seu nome ou por sua descriçao;
	+ **`apt-cache show [nome_pacote]`** -> mostra a descriçai detalhada do pacote;


<br>
<br>


## Red Hat /Cent OS

---


### Gerenciadores de Baixo Nivel

#### RPM (Red Hat Package Manager)
Faz a gestao (remoçao, instalaçao e atualizaçao) de pacotes que ja estao na maquina.

**Comando: ** **`rpm`**

+ **`rpm -i [nome_pacote].rpm`** -> realiza a instalaçao de um pacote `.rpm`;
	+ **`rpm -ivh [nome_pacote].rpm`** -> realiza a instaçao do pacote de maneira verbosa e com barra de progresso;
+ **`rpm -e [nome_pacote]`** -> realiza a remoçao do pacote;
+ **`rpm -U [nome_pacote].rpm`** -> realiza a atualizaçao de um pacote ja instalado para uma versao mais nova;
+ **`rpm -q`** -> entra no modo de consulta do *rpm* (q == Query):
	+ **`rpm -qa`** -> lista todos os pacotes instalados;
	+ **`rpm -qi [nome_pacote]`** -> traz informaçoes a respeito do pacote instalado;
		+ **`rpm -qip [nome_pacote].rpm`** ->  Traz as informaçoes de um pacote no formato *rpm*;
	+ **`rpm -ql [nome_pacote]`** -> Imprime uma lista dos arquivos relacionados a um pacote;
		+ **`rpm -qlp [nome_pacote].rpm`** -> Imprime uma lista dos arquivos relacionados ao pacote *rpm*;
	 + **`rpm -qf [caminho_arquivo]`** -> Imprime a o nome do pacote ao qual pertence o arquivo.

**Comando:** **`rpm2cpio`**:
+ **`rpm2cpio [nome_pacote].rpm`** -> converte um arquivo **.rpm** para um arquivo **cpio** e imprime na saida padrao;
	+ **Exemplo:** `rpm2cpio [nome_pacote].rpm | cpio -idv` -> realiza a extraçao do conteudo de um arquivo rpm.



<br>

### Gerenciadores de Alto Nivel 

#### YUM (Yellowdog Updater Modified)
Faz o download de pacotes (e suas dependencias) que estao em repositorios externos (na rede). Para isso, ele procura pelo pacote em servidores externos configurados. Se encontrar o pacote, faz o download e por fim usa o  **rpm** para realizar a instalaçao do(s) pacote(s). Podemos pensar no yum como um *frontend* para o rpm.


**Arquivos de configuraçao:**
+ **`/etc/yum.conf`** -> arquivo de configuraçao principal dos repositorios do yum;
+ **`/etc/yum.repos.d/`** -> contem arquivos de configuraçao dos repositorios. Separa a configuraçao de cada repositorio em arquivos diferentes;


**Comandos** 

+ **`yum install [nome_pacote]`** -> realiza a instalaçao do pacote;
+ **`yum remove [nome_pacote]`** -> realiza a remoçao do pacote;
+ **`yum search [nome_pacote|regex]`** -> busca nos repositorios pelo nome ou padrao especificado. Ele busca tanto pelo nome do pacote quanto pela descriçao;
+ **`yum update`** -> realiza atualizaçao dos index e tambem dos pacotes disponiveis (equivalente ao *apt update + apt upgrade*);
	+ **`yum update -x [lista_pacote|regex]`** -> impede que os pacotes listas sejam atualizados;
		+ **Exemplo:** `yum update -x docker*,containerd*` 
	+ **`yum update [nome_pacote]`** -> atualiza um pacote em especifico;
+ **`yum check-update`** -> verifica se ha algum pacote que pode ser atualizado;
+ **`yum whatprovides [caminho_arquivo]`** -> retorna qual pacote que prove/instala o arquivo para o sistema;
+ **`yum info [nome_pacote]`** -> imprime informaçoes a respeito do pacote;
+ **`yum repolist`** -> lista todos repositorios configurados;
+ **`yum groupinstall  "[nome_dos_pacotes]"`** -> instala um grupo de pacotes;


**Outras informaçoes/Pacotes interessantes**:
+ **`epel-release`** -> repositorio do Cent OS que contem pacotes extras. Pode ser instalado com o *yum*;
+ **`bash-completion`** -> habilita o autocompletar do bash para alguns comandos;
+ **`yum-config-manager`** -> utilitario que auxilia no gerenciamento de repositorios;
	+ **`yum-config-manager --add-repo [URL]`**
	+ **`yum-config-manager --enable [REPO]`**
	+ **`yum-config-manager --disable [REPO]`**


<br>

#### DNF ( Dandified Yum)
Outro gerenciador de pacotes de alto nivel disponivel para Red Hat. Também utilizam do *rpm* como *"backend"*.

**Comandos**:
+ **`dnf install [nome_pacote]`** -> realiza a busca e instalaçao do pacote;
+ **`dnf remove [nome_pacote]`** -> realiza a remoçao do pacote;
+ **`dnf info [nome_pacote]`** -> imprime informaçoes a respeito do pacote;
+ **`dnf search [nome_pacote]`** -> busca nos repositorios pelo nome do pacote;
+ **`dnf upgrade`** -> atualiza os pacotes do sistema;

<br>

#### ZYPPER 
Gerenciador de pacotes de alto nivel do openSUSE.Também utilizam do *rpm* como *"backend"*.

**Comandos**:
+ **`zypper install`** -> realiza a busca e instalaçao do pacote;
	+ **`zypper in [nome_pacote]`** -> realiza a busca e instalaçao do pacote (forma abreviada);
+ **`zypper rm [nome_pacote]`** -> realiza a remoçao do pacote;
+ **`zypper refresh`** -> atualiza a lista de repositorios;
