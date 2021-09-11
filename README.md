# Meu CheatSheet de Git
Passo a passo que adoto na minha utilização do git.

- [Meu CheatSheet de Git](#meu-cheatsheet-de-git)
  - [1 Instalação e Configuração](#1-instalação-e-configuração)
    - [1.1 Cmder](#11-cmder)
      - [1.1.1 Keyboard Shortcuts](#111-keyboard-shortcuts)
      - [1.1.2 Comandos para o vi](#112-comandos-para-o-vi)
  - [2 Primeiros Passos](#2-primeiros-passos)
  - [3 Comunicação com remotos (GitHub, GitBucket, GitLab)](#3-comunicação-com-remotos-github-gitbucket-gitlab)
    - [3.1 Criando chave SSH](#31-criando-chave-ssh)
      - [3.1.1 PuTTY](#311-putty)
      - [3.1.2 Linha de comando](#312-linha-de-comando)
    - [3.2 Cruzando chave SSH](#32-cruzando-chave-ssh)
    - [3.3 Configuração com Proxy](#33-configuração-com-proxy)
  - [4 Comandos Básicos](#4-comandos-básicos)
    - [4.1 Clonando Repositórios](#41-clonando-repositórios)
  - [5 Comandos Intermediários e Avançados](#5-comandos-intermediários-e-avançados)
    - [5.1 Enviando Branch para Remoto](#51-enviando-branch-para-remoto)
    - [5.2 Atualizando Branch de Remoto](#52-atualizando-branch-de-remoto)
  - [6 Mensagens de Erro](#6-mensagens-de-erro)
    - [6.1 Alterações Não Versionadas](#61-alterações-não-versionadas)
  - [7 Minhas Aliases](#7-minhas-aliases)

## 1 Instalação e Configuração
O download do Git pode ser feito pelo seguinte [LINK][1], e toda a instalação pode ser feita pelas opções *default* do instalador. Ou, no caso de um cliente Linux (Debian/Ubuntu), utilizar: `apt-get install git` (ver mais opções na [página de Linux do Git][2])

### 1.1 Cmder
Uma outra opção de utilização do Git, é pelo aplicativo terceiro [Cmder][3]. Nele o git já vem instalado e basta realizar os seguintes passos para completar a configuração:
1. Ao fazer o download do arquivo .zip, extrair todo o conteúdo dentro da pasta **.cmder** no **%UserProfile%**;
2. Definir um atalho para o .exe do Cmder e enviar para o local de preferência;
3. Ao abrir o Cmder, `Ctrl + T` e criar um novo console como `{bash::mintty as Admin}` para entrar como um editor Unix. Para não ficar fazendo isso toda vez, realizar as seguintes alterações:
   * <kbd>Settings</kbd> > <kbd>Startup</kbd> > Check "Specified named task" > Choose <kbd>{bash::mintty as Admin}</kbd> > <kbd>Save Settings</kbd>

#### 1.1.1 Keyboard Shortcuts

<kbd>Ctrl</kbd>+<kbd>L</kbd> - Limpar a tela do terminal

<kbd>Ctrl</kbd>+<kbd>Ins</kbd> - Copiar

<kbd>Shift</kbd>+<kbd>Ins</kbd> - Colar

#### 1.1.2 Comandos para o vi

<kbd>I</kbd> - Editar a janela

<kbd>:</kbd><kbd>x</kbd> or <kbd>:</kbd><kbd>w</kbd><kbd>q</kbd> - Sair do vi, gravando o arquivo modificado no arquivo nomeado na chamada original

<kbd>:</kbd><kbd>q</kbd> - Sair do vi

Para mais comandos relacionados ao editor vi, verificar esta página de [*Basic vi Commands*][4].

## 2 Primeiros Passos
Primeiramente, é necessário configurar o espaço do Git em seu computador, adicionando Nome e Email. Para isso, abra o terminal Unix (de sua preferência) e digíte:

```git
git --version
git config --global user.name "[NOME]"
git config --global user.email "[EMAIL]"
git config --list
```

Nos comandos acima, podemos verificar a versão instalada do git (1), configurar o nome (2) e email (3) e em seguida, verificar se os dados foram cadastrados corretamente.

Ao iniciar um projeto, deve-se mostrar para o Git que esta pasta é um repositório local:

```git
git init
dir -a
ls
```

Ao inicializar o Git (1), é criada uma pasta oculta com o nome .git, sendo possível enxergá-la com uma opção -a para o código dir (2) ou utilizar o (3). Também é criada uma branch (que vem com o nome *default* `master`). Se no caso a branch padrão do GitHub estiver com outro nome, basta altrar no próprio GitHub ou alterar a do Git local com os seguintes comandos:

```git
git branch
git branch --list
git branch -m [ANTIGO] [NOVO]
git branch -a
```

A diferença entre o comando (2) e (4) é que o primeiro lista somente as *branchs* locais, já o segundo lista tanto as locais quanto remotas. 

Para exluir uma branch:

```
git branch -d [BRANCH]
git branch -D [BRANCH]
```

Utilizar (1) para apagar somente a branch se você já tiver feito merge ou enviado as alterações para seu repositório remoto, evitando perda de código, ou (2), para ignorar o estado da sua branch, forçando a sua remoção. Caso queira deletar algum repositório criado localmente pelo `git init`:

```git
rm -rf .git
```

## 3 Comunicação com remotos (GitHub, GitBucket, GitLab)
Para realizar a comunicação entre o Git local e aplicações remotas é necessária uma configuração de segurança através de SSH. É possível também comunicar local com remoto sem o SSH, entretanto, toda vez que precisar fazer um *push* no remoto, solicitará a senha para do usuário, verificando se o repositório em questão é seu.

### 3.1 Criando chave SSH
O SSH (*Secure Shell* ou *Secure Socket Shell*) é um protocolo que permite a conexão com servidores remotos, de forma criptografada e mais segura, usando um par de chaves (RSA, DSA...). Há duas principais formas de criarmos essa chave: utiliazando um software terceiro - PuTTY, ou criando por linha de comando.

Primeiramente, deve-se criar uma pasta do **%UserProfile%** denominada **.ssh**, na qual guardará todas as chaves do usuário. É recomendado apenas uma de cada. Para verificar se você já tem alguma chave cadastrada, dê o seguinte comando em seu Git Bash:

```
ls -al ~/.ssh
```

Também é possível criar uma chave de segurança de hardware para que cada vez que utilizar uma máquina diferente, não precise gerar outras chaves. Entretanto, é necessário ter o hardware para este tipo de chave.

#### 3.1.1 PuTTY
1. Fazer o download do [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html), ou o programa completo, ou apenas o puttygen.exe
2. Ao entrar no PuTTY Key Generator, realizar os seguintes passos:
   * <kbd>Generate</kbd> > Mexer o mouse pela tela, pois a geração ocorre de acordo com esses movimentos > Colocar a senha e confirmar a senha > <kbd>Save public key</kbd> (com o nome `id_rsa.pub`) > <kbd>Save private key</kbd> (com o nome `id_rsa`)
   * **OBSERVAÇÕES:** 
     * Essas duas chaves devem estar dentro da pasta **.ssh** criada anteriormente;
     * Pode ser que as chaves criadas pelo PuTTYgen não seja reconhecida pelas aplicações remotas como GitHub, BitBucket. Assim, é necessária conversão da mesma para OpenSSH (no próprio programa).

#### 3.1.2 Linha de comando

Cole o texto abaixo, substituindo o endereço de e-mail pelo seu GitHub.

```
ssh-keygen -t rsa -b 2048 -C "[EMAIL]"
```

Você pode optar por outro algoritmo como o Ed25519:

```
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Caso queira simplificar, apenas o comando abaixo realizará o trabalho:

```
ssh-keygen
ssh-keygen -t rsa
```

Esses comandos criaram uma nova chave SSH, usando o e-mail fornecido como uma etiqueta. Quando aparecer a solicitação "Enter a file in which to save the key" (Insira um arquivo no qual salvar a chave), presssione Enter. O local padrão do arquivo será aceito. Em seguida, digite uma frase secreta segura para essa senha gerada.

No próximo tópico, será mostrado um código .bash que adiciona a chave criada ao `ssh-agent`, mas caso queira inserí-la manualmente, seguir os códigos abaixo:

```
eval "$(ssh-agent -s)"
> Agent pid 59566
ssh-add ~/.ssh/id_ed25519
```

### 3.2 Cruzando chave SSH
Após criada a chave SSH, é necessário avisar para a sua conta do GitHub qual é o usuário (chave SSH) que ele pode confiar edição. Para isso, vá até sua conta no GitHub e siga os seguintes passos:
* <kbd>Settings</kbd> > <kbd>SSH and GPG keys</kbd> > <kbd>New SSH key</kbd> > Coloca o título de preferência e cole todo o conteúdo da chave pública gerada no campo key

Deve-se avisar também ao cliente remoto uma forma de como autenticar a sua chave local. Uma das que mais facilitam essa autenticação é a criação de um arquivo `.bashrc`, assim, sempre que o Cmder ou outro edito de texto for aberto, pedirá sua senha da chave privada para que haja a conexão.

Abaixo está um exemplo de um `.bashrc` utilizado com variáveis Alias:

```bash
env=~/.ssh/agent.env

agent_load_env () { test -f "$env" && . "$env" >| /dev/null ; }

agent_start () {
    (umask 077; ssh-agent >| "$env")
    . "$env" >| /dev/null ; }

# agent_run_state: 0=agent running w/ key; 1=agent w/o key; 2= agent not running
agent_run_state=$(ssh-add -l >| /dev/null 2>&1; echo $?)

if [ ! "$SSH_AUTH_SOCK" ] || [ $agent_run_state = 2 ]; then
    agent_load_env
    agent_start
    ssh-add
elif [ "$SSH_AUTH_SOCK" ] && [ $agent_run_state = 1 ]; then
    ssh-add
fi

unset env

# Aliases
alias gs='git status'

```

Este arquivo deve ser colocado na pasta raiz do usuário (**%UserProfile%**) e rodado uma única vez para que crie os outros arquivos necessários.

### 3.3 Configuração com Proxy
Caso o seu repositório local esteja em uma máquina na rede com proxy ou firewall e aconteça alguns problemas, é necessário configurar o git para aquele proxy, login e usuário, com os comando abaixo:

```
git config --global http.proxy http://proxyuser:proxypwd@proxy.server.com:8080
```

É necessário alterar `proxyuser` para o seu usuário do proxy, `proxypwd` para a senha do usuário, `proxy.server.com` para o server e `8080` para a porta configurada.

Em alguns casos o https também deve ser configurado. Se mesmo realizando a etapa acima não resolver, é necessário adicionar a chave manualmente na config do git seguindo os passos deste [LINK][6]

```
$ ssh -Tv git@bitbucket.org
OpenSSH_6.9p1, LibreSSL 2.1.8
...
Permission denied (publickey).

$ ssh-add -l 
2048 SHA256:... /Users/user/.ssh/id_rsa (RSA)

$ ssh-add ~/.ssh/user-Bitbucket
Enter passphrase for /Users/user/.ssh/user-Bitbucket: 
Identity added: /Users/user/.ssh/user-Bitbucket (/Users/user/.ssh/user-Bitbucket)

$ ssh-add -l 
2048 SHA256:... /Users/user/.ssh/id_rsa (RSA)
2048 SHA256:... /Users/user/.ssh/user-Bitbucket (RSA)

$ ssh -Tv git@bitbucket.org
OpenSSH_6.9p1, LibreSSL 2.1.8
...
logged in as user.
```

## 4 Comandos Básicos
Ao criar o seu repositório local de trabalho e iniciar o seu Git (como visto na seção [Primeiros Passos](#primeiros-passos)), inicia-se os trabalhos neste repositório e os comandos básicos para manuseio do mesmo são:

```
git status
git add [ARQUIVO]
git commit -m "[MSG]"
```

Quando é realizada alguma alteração nos arquivos, ao dar o (1), será mostrado todos aqueles arquivos que estão diferentes do Git local. Atenção às cores: quando estiverem vermelhos é porque não foi passado para o Git quais arquivos devem ser *staged* (fica na *Staging Area*). Caso queria adicionar todos os arquivos (2), adicionar `git add --all` ou `git add .` ou `git add -A`. Uma outra observação válida é sobre adicionar outra submensagem ao commit (3) com uma outra opção `-m "MSG"` resultando em `git commit -m "[MSG1]" -m "[MSG2]"`. O `git commit` (apenas) abre o ambiente vi de edição para que essas mensagens sejam editadas lá (verificar subsubseção [Comandos para VI](#comandos-para-o-vi)).

Para verificar alterações no repositório local, segue os códigos:
```
git diff
git diff --cached
git diff --staged

```

O (1) mostra a diferença que ocorreu entre o meu repositório de trabalho e as alterações do último commit. No (2) e (3), as diferenças da área de preparação (Staging Area) são apresentadas. Caso goste de todas as alterações mostradas nessas diferenças, mardar para staged com o `git add`.

Já para listar o histórico de alterações, tem-se o comando:

```
git log
```

No git log (1), as modificações são listadas sempre da mais recente (topo) para mais antiga e cada uma carrega um número **SHA** (algoritmo que consegue gerar um número único) para fácil rastreio do commit e cada um carrega o Nome, Email, Data e Mensagem de Commit. Note-se também nesta etapa o conceito **HEAD**. **HEAD** é um ponteiro que aponta sempre para última modificação de uma branch. Há variações do `git log` que estão disponíveis no arquivo CRIAR ARQUIVO COM TODOS OS COMANDOS [Minhas Aliases](#minhas-aliases).

Para retornar a commits anteriores, usar o comando abaixo, sendo que não é necessário copiar o número SHA inteiro do commit, apenas os 5/6 primeiros dígitos já bastam.

```
git checkout [nºSHA]
git checkout [nomeARQUIVO.txt]
git reset --hard
```

Para retornar ao HEAD, utilizar o `git checkout [BRANCH]`. Há parâmetros que podem ser passados com o `checkout` como `-b`, que já cria e muda de branch de uma forma direta. No (2), é desfeito toda alteração do arquivo em questão e também, quando deletado algum, é possível recuperá-lo através deste programa. Mas note que se muitos arquivos forem modificados (excluídos), fica inviável refazer as alterações com este comando um po um. Assim, o (3) força o reset para o último commit. Se for apenas `git reset` é mostrado as opções de reset para escolha.

Caso opte por [retornar para um commit][5], há a opção de reset:

```
git reset --hard HEAD~1
git reset --soft HEAD~1
git reset --hard [nºSHA]
git push origin HEAD --force
git add .
git commit -c ORIG_HEAD
```

A diferença entre a opção hard e soft é que se utilizar o hard, os commits posteriores ao do retorno serão perdidos, diferentemento do soft, que manterá todos. (1) e (2) apenas retornam um commit. Caso queira retornar mais, trocar o 1 para tanto de commits anteriores, ou faça a alteração pelo SHA RASH (3). Se o commit foi enviado para o repositório remoto, a opção (4) deve ser realizada. Assim, ao refazer as alterações, um novo `git add` deve ser feito e a mensagem de commit pode ser trocada com (4).

### 4.1 Clonando Repositórios

É possível não apenas clonar em uma URL remota, mas nos arquivos locais como:

```
git clone TestGit NovoTestGit
```

Mas o mais utilizado é para clonar repositórios do GitHub:

```
cd [DIR]
git clone [URL]
```

## 5 Comandos Intermediários e Avançados

Esta seção necessita necessáriamente da configuração préviamente realizada nas seções [1](#1-instalação-e-configuração), [2](#2-primeiros-passos) e [3](#3-comunicação-com-remotos-github-gitbucket-gitlab).

### 5.1 Enviando Branch para Remoto

Para enviar as alterações (commits) realizados localmente, é necessário "empurrar" com os comandos:

```
git push
git push -u origin [BRANCH]
```

Caso não exista nenhum repositório remoto com o nome da branch indicada, será preciso enviar o comando `git push --set-upstream origin [BRANCH]`. Para simplificar, a opção `-u` substitui este comando (2).

### 5.2 Atualizando Branch de Remoto

## 6 Mensagens de Erro
### 6.1 Alterações Não Versionadas
A mensagem de erro abaixa é dada sempre quando o usuário quer trocar de uma branch para a outra, mas tem alterações em arquivos da branch atual que mão foram "commitadas".

```error
error: Your local changes to the following files would be overwritten by checkout:
  index.html
Please commit your changes or stash them before you switch branches.
```

Para resolvê-lo, realizar algum dos passos a seguir:
1. Commitar as mudanças na branch atual;
2. Colocar as mudanças em stash utilizando o `git stash`
3. Excluir as modificações com `git reset --hard`

## 7 Minhas Aliases
| Alias |     Git Command     |                                                    Description                                                    |
| ----- | :-----------------: | :---------------------------------------------------------------------------------------------------------------: |
| gs    | `git status` | Verificar status do Git |
| gch   | `git checkout --` |  |
| gl    | `git log` |  |
| glo   | `git log --oneline` |  |
| glp   | `git log --pretty=format:[FORMATO]` | "%C(yellow)%h %Cred%ad %Cblue%an%Cgreen%d %Creset%s" --date=short' #"%h%x09%an%x09%ad%x09%s" ---> %h = abbreviated commit hash ; %x09 = tab (character for code 9) ; %an = author name ; %ad = author date (format respects --date= option) ; %s = subject  |
| gfp   | `git fetch --prune` | Para ter certeza se está tudo ok, combinado remoto com local, se não, deleta no local o que não estiver no github |
| gps   | `git push` |  |
| gpl   | `git pull` |  |
| gplp  | `git pull --allow-unrelated-histories` | Para quando acontecer de de travar o push 'non-fast-forward' |
| gffs  | `git flow feature start` |  |
| gfff  | `git flow feature finish` |  |
| gffp  | `git flow feature publish` |  |





* gfp - git fetch --purse -> para ter certeza se está tudo ok, combinado remoto com local, se não, deleta no local o que não estiver no github;
* gs - git status;
* git branch - para verfificar quais as branchs do meu projeto; geralmente sempre a develop e a main (excluir com 'git branch -d NOME_DA_BRANCH' caso haja alguma desnecessária);
* git pull - para ver se tem algo a trazer do github;
* gffs estilos_login - começando agora uma nova branch de feature;
* git diff - para ver as alteraçoes feitas - ANTES DO GIT ADD
* git add .
* git commit -m 'message' -m 'optional, better description'
* Alteração antes de produzir uma release
* gfp - comando para dar uma atualizada no git
* git pull origin main --allow-unrelated-histories - é o comando para quando há erro no push

<!-- Markdown's Links -->
<!-- SITES -->
[1]: https://git-scm.com/
[2]: https://git-scm.com/download/linux
[3]: https://cmder.net/
[4]: https://www.cs.colostate.edu/helpdocs/vi.html
[5]: https://stackoverflow.com/questions/927358/how-do-i-undo-the-most-recent-local-commits-in-git
[6]: https://www.notion.so/jonathansmar/Comunicar-Git-e-BitBucket-d528f973813047a7a8db45d0dccf570b#7e19b5d9b12f4c5ab6055de146ceff9e

<!-- ARQUIVOS -->
* Para cada passo será comentado uma linha, a fim de teste;
* Alteração antes de produzir uma release
* Alteração antes de produzir uma release
* gfp - comando para dar uma atualizada no git
* git pull origin main --allow-unrelated-histories - é o comando para quando há erro no push
