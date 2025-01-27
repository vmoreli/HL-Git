# Meu CheatSheet de Git
Passo a passo que adoto na minha utilização do git.

- [Meu CheatSheet de Git](#meu-cheatsheet-de-git)
  - [1 Instalação e Configuração](#1-instalação-e-configuração)
    - [1.1 Visual Studio Code](#11-visual-studio-code)
    - [1.2 Cmder](#12-cmder)
      - [1.2.1 Keyboard Shortcuts](#121-keyboard-shortcuts)
      - [1.2.2 Comandos para o vi](#122-comandos-para-o-vi)
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
    - [5.3 Deletando Branch do Remoto](#53-deletando-branch-do-remoto)
    - [5.4 Renomeando uma Branch](#54-renomeando-uma-branch)
    - [5.5 Mesclando Alterações](#55-mesclando-alterações)
    - [5.6 Resolvendo Conflitos](#56-resolvendo-conflitos)
      - [5.6.1 kdiff3](#561-kdiff3)
    - [5.7 Pull Request](#57-pull-request)
  - [6 Mensagens de Erro e Workarounds](#6-mensagens-de-erro-e-workarounds)
    - [6.1 Alterações Não Versionadas](#61-alterações-não-versionadas)
    - [6.2 Desfazendo commits](#62-desfazendo-commits)
  - [7 Gitflow](#7-gitflow)
  - [8 Minhas Aliases](#8-minhas-aliases)

## 1 Instalação e Configuração
O download do Git pode ser feito pelo seguinte [LINK][1], e toda a instalação pode ser feita pelas opções *default* do instalador. Ou, no caso de um cliente Linux (Debian/Ubuntu), utilizar: `apt-get install git` (ver mais opções na [página de Linux do Git][2]). Vale ressaltar um ponto importante na instalação do Git que é a opção de "Adding Git-Bash to the new Windows Terminal"; este novo terminal do windows agrupa as ferramentas e shells de linha de comando, como prompt de comando, PowerShell, WSL e GitBash, caso marque a opção na instalção do Git. O download pode ser feito na Microsoft Store ou pelo seguinte [link][8].

Fica a dica de uma aplicação desenvolvida para uma melhor visualização de como funciona o Git, ou até mesmo, uma ferramenta para criar imagens para didática do Git: [Git-School][10].

![git-school][git-school]

### 1.1 Visual Studio Code
O VSCode é o editor de código-fonte mais utilizado do mundo. Uma de suas principais vantagens frente à outros editores é a utilização de extensões desenvolvidas pela comunidade, que inclui suporte para depuração, controle de versionamento Git incorporado (*Source Control*), realce de sintaxe, complementação inteligente de código, snippets e refatoração de código.. Neste tópico serão abordadas as melhores extensões para utilizar o Git com o VSCode da melhor forma e aproveitando os melhores recursos que o editor tem a oferecer.

Um detalhe a acrescentar para este tópico a possibilidade de uma pasta `.vcode/` que contenha as informações específicas para esta integração, como um arquivo `extensions.json` que carrega as extensões recomendadas para uma melhor utilização de um determinado *workspace* (repositório):

```json
{
    "recommendations": [
        "ms-ceintl.vscode-language-pack-pt-br"
    ]
}
```

Para mais dicas de instalação, teclas de atalho, plugins e integrações, ver material de apoio [1][9].

**Source Control**

O Visual Studio Code integrou o gerenciamento de controle de origem (SCM) e inclui suporte Git pronto para uso. Muitos outros provedores de controle de origem estão disponíveis por meio de extensões no VS Code Marketplace.

É esta função nativa que habilita os seguintes marcadores de estado dos arquivos:
* **A** - Added (Este é um arquivo novo que foi adicionado ao seu repositório)
* **M** - Modified (Um arquivo existente que foi alterado)
* **D** - Deleted (Um arquivo foi excluido)
* **U** - Untracked (O arquivo é novo ou foi alterado, mas ainda não foi adicionado ao repositório)
* **C** - Conflict (Há um conflito no arquivo)
* **R** - Renamed (O arquivo foi renomeado)
* **S** - Submodule (No repositório, existe outro subrepositório)

**Git Lens**

**Git History**

**Git Graph**

**Git Blame**

### 1.2 Cmder
Uma outra opção de utilização do Git, é pelo aplicativo terceiro [Cmder][3]. Nele o git já vem instalado e basta realizar os seguintes passos para completar a configuração:
1. Ao fazer o download do arquivo .zip, extrair todo o conteúdo dentro da pasta **.cmder** no **%UserProfile%**;
2. Definir um atalho para o .exe do Cmder e enviar para o local de preferência;
3. Ao abrir o Cmder, `Ctrl + T` e criar um novo console como `{bash::mintty as Admin}` para entrar como um editor Unix. Para não ficar fazendo isso toda vez, realizar as seguintes alterações:
   * <kbd>Settings</kbd> > <kbd>Startup</kbd> > Check "Specified named task" > Choose <kbd>{bash::mintty as Admin}</kbd> > <kbd>Save Settings</kbd>

#### 1.2.1 Keyboard Shortcuts

<kbd>Ctrl</kbd>+<kbd>L</kbd> - Limpar a tela do terminal

<kbd>Ctrl</kbd>+<kbd>Ins</kbd> - Copiar

<kbd>Shift</kbd>+<kbd>Ins</kbd> - Colar

#### 1.2.2 Comandos para o vi

<kbd>I</kbd> - Editar a janela

<kbd>:</kbd><kbd>x</kbd> or <kbd>:</kbd><kbd>w</kbd><kbd>q</kbd> - Sair do vi, gravando o arquivo modificado no arquivo nomeado na chamada original

<kbd>:</kbd><kbd>q</kbd> - Sair do vi

Para mais comandos relacionados ao editor vi, verificar esta página de [*Basic vi Commands*][4].

## 2 Primeiros Passos
Primeiramente, é necessário configurar o espaço do Git em seu computador, adicionando Nome e Email. Para isso, abra o terminal Unix (de sua preferência) e digíte:

```
(1) λ git --version
(2) λ git config --global user.name "[NOME]"
(3) λ git config --global user.email "[EMAIL]"
(4) λ git config --list
```

Nos comandos acima, podemos verificar a versão instalada do git (1), configurar o nome (2) e email (3) e em seguida, verificar se os dados foram cadastrados corretamente.

Ao iniciar um projeto, deve-se mostrar para o Git que esta pasta é um repositório local:

```
(5) λ git init
(6) λ dir -a
(7) λ ls
```

Ao inicializar o Git (5), é criada uma pasta oculta com o nome .git, sendo possível enxergá-la com uma opção -a para o código dir (6) ou utilizar o (7). Também é criada uma branch (que vem com o nome *default* `master`). Se no caso a branch padrão do GitHub estiver com outro nome, basta altrar no próprio GitHub ou alterar a do Git local com os seguintes comandos:

```
(8.1) λ git branch
(8.2) λ git branch --list
(8.3) λ git branch -m [ANTIGO] [NOVO]
(8.4) λ git branch -a
```

A diferença entre o comando (8.1/8.2) e (8.4) é que o primeiro lista somente as *branchs* locais, já o segundo lista tanto as locais quanto remotas. 

Para exluir uma branch local:

```
(8.5) λ git branch -d [BRANCH]
(8.6) λ git branch -D [BRANCH]
```

Utilizar (8.5) para apagar somente a branch se você já tiver feito merge ou enviado as alterações para seu repositório remoto, evitando perda de código, ou (8.6), para ignorar o estado da sua branch, forçando a sua remoção. Vale ressaltar que não é possível realizar esta alteração se estiver `checkado` na branch. Mas se por acaso se arrependa da remoção indevida da branch, basta trazê-la de novo ao local por `git checkout [BRANCH]`.

Caso queira deletar por completo algum repositório criado localmente pelo `git init`:

```
(9) λ rm -rf .git
```

## 3 Comunicação com remotos (GitHub, GitBucket, GitLab)
Para realizar a comunicação entre o Git local e aplicações remotas é necessária uma configuração de segurança através de SSH. É possível também comunicar local com remoto sem o SSH, entretanto, toda vez que precisar fazer um *push* no remoto, solicitará a senha para do usuário, verificando se o repositório em questão é seu.

### 3.1 Criando chave SSH
O SSH (*Secure Shell* ou *Secure Socket Shell*) é um protocolo que permite a conexão com servidores remotos, de forma criptografada e mais segura, usando um par de chaves (RSA, DSA...). Há duas principais formas de criarmos essa chave: utiliazando um software terceiro - PuTTY, ou criando por linha de comando.

Primeiramente, deve-se criar uma pasta do **%UserProfile%** denominada **.ssh**, na qual guardará todas as chaves do usuário. É recomendado apenas uma de cada. Para verificar se você já tem alguma chave cadastrada, dê o seguinte comando em seu Git Bash:

```
(10) λ ls -al ~/.ssh
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
(11.1) λ ssh-keygen -t rsa -b 2048 -C "[EMAIL]"
```

Você pode optar por outro algoritmo como o Ed25519:

```
(11.2) λ ssh-keygen -t ed25519 -C "your_email@example.com"
```

Caso queira simplificar, apenas o comando abaixo realizará o trabalho:

```
(11.3) λ ssh-keygen
(11.4) λ ssh-keygen -t rsa
```

Esses comandos criaram uma nova chave SSH, usando o e-mail fornecido como uma etiqueta. Quando aparecer a solicitação "Enter a file in which to save the key" (Insira um arquivo no qual salvar a chave), presssione Enter. O local padrão do arquivo será aceito. Em seguida, digite uma frase secreta segura para essa senha gerada.

No próximo tópico, será mostrado um código .bash que adiciona a chave criada ao `ssh-agent`, mas caso queira inserí-la manualmente, seguir os códigos abaixo:

```
(12) λ eval "$(ssh-agent -s)"
> Agent pid 59566
(13) λ ssh-add ~/.ssh/id_ed25519
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

```{attr.source='.numberLines'}
(14) λ git config --global http.proxy http://proxyuser:proxypwd@proxy.server.com:8080
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
(15) λ git status
(16) λ git add [ARQUIVO]
(17) λ git commit -m "[MSG]"
```

Quando é realizada alguma alteração nos arquivos, ao dar o (15), será mostrado todos aqueles arquivos que estão diferentes do Git local. Atenção às cores: quando estiverem vermelhos é porque não foi passado para o Git quais arquivos devem ser *staged* (fica na *Staging Area*). Caso queria adicionar todos os arquivos (16), adicionar `git add --all` ou `git add .` ou `git add -A`. Uma outra observação válida é sobre adicionar outra submensagem ao commit (17) com uma outra opção `-m "MSG"` resultando em `git commit -m "[MSG1]" -m "[MSG2]"`. O `git commit` (apenas) abre o ambiente vi de edição para que essas mensagens sejam editadas lá (verificar subsubseção [Comandos para VI](#comandos-para-o-vi)).

❕ **Dica**: Para juntar (16) e (17) em uma única linha, utilizar o comando `git commit -a -m "[MSG]"` ou até `git commit -am "[MSG]"`.

Para verificar alterações no repositório local, segue os códigos:
```
(18.1) λ git diff
(18.2) λ git diff --cached
(18.3) λ git diff --staged
```

O (18.1) mostra a diferença que ocorreu entre o meu repositório de trabalho e as alterações do último commit. No (18.2) e (18.3), as diferenças da área de preparação (*Staging Area*) são apresentadas. Caso goste de todas as alterações mostradas nessas diferenças, mardar para staged com o `git add`.

Já para listar o histórico de alterações, tem-se o comando:

```
(19) λ git log
```

No (19), as modificações são listadas sempre da mais recente (topo) para mais antiga e cada uma carrega um número **SHA** (algoritmo que consegue gerar um número único) para fácil rastreio do commit e cada um carrega o Nome, Email, Data e Mensagem de Commit. Note-se também nesta etapa o conceito **HEAD**. **HEAD** é um ponteiro que aponta sempre para última modificação de uma branch. Há variações do `git log` que estão disponíveis no arquivo [CRIAR ARQUIVO COM TODOS OS COMANDOS] [Minhas Aliases](#minhas-aliases).

Para retornar a commits anteriores, usar o comando abaixo, sendo que não é necessário copiar o número SHA inteiro do commit, apenas os 5/6 primeiros dígitos já bastam.

```
(20.1) λ git checkout [nºSHA]
(20.2) λ git checkout [nomeARQUIVO.txt]
(21.1) λ git reset --hard
```

Para retornar ao HEAD, utilizar o `git checkout [BRANCH]`. Há parâmetros que podem ser passados com o `checkout` como `-b`, que já cria e muda de branch de uma forma direta. No (20.2), é desfeito toda alteração do arquivo em questão e também, quando deletado algum, é possível recuperá-lo através deste programa. Mas note que se muitos arquivos forem modificados (excluídos), fica inviável refazer as alterações com este comando um po um. Assim, o (21.1) força o reset para o último commit. Se for apenas `git reset` é mostrado as opções de reset para escolha.

Caso opte por [retornar para um commit][5], há a opção de reset:

```
(21.2) λ git reset --hard HEAD~1
(21.3) λ git reset --soft HEAD~1
(21.4) λ git reset --hard [nºSHA]
(22) λ git push origin HEAD --force
(23) λ git add .
(24) λ git commit -c ORIG_HEAD
```

A diferença entre a opção hard e soft é que se utilizar o hard, os commits posteriores ao do retorno serão perdidos, diferentemento do soft, que manterá todos. (21.2) e (21.3) apenas retornam um commit. Caso queira retornar mais, trocar o 1 para tanto de commits anteriores, ou faça a alteração pelo SHA RASH (21.4). Se o commit foi enviado para o repositório remoto, a opção (22) deve ser realizada. Assim, ao refazer as alterações, um novo `git add` deve ser feito e a mensagem de commit pode ser trocada com (24).

### 4.1 Clonando Repositórios

É possível não apenas clonar em uma URL remota, mas nos arquivos locais como:

```
(25.1) λ git clone [OLD.DIRECTORY] [NEW.DIRECTORY]
```

Mas o mais utilizado é para clonar repositórios do GitHub:

```
(26) λ cd [DIR]
(25.2) λ git clone [URL]
```

## 5 Comandos Intermediários e Avançados

Esta seção necessita necessáriamente da configuração préviamente realizada nas seções [1](#1-instalação-e-configuração), [2](#2-primeiros-passos) e [3](#3-comunicação-com-remotos-github-gitbucket-gitlab).

### 5.1 Enviando Branch para Remoto

Para enviar as alterações (commits) realizados localmente, é necessário "empurrar" com os comandos:

```
(27.1) λ git push
(27.2) λ git push -u origin [BRANCH]
```

Caso não exista nenhum repositório remoto com o nome da branch indicada, será preciso enviar o comando `git push --set-upstream origin [BRANCH]`. Para simplificar, a opção `-u` substitui este comando (27.2).

### 5.2 Atualizando Branch de Remoto

Em um cenário real, seriam duas pessoas trabalhando no mesmo respositório remoto, e consequentemente, com dois locais em diferentes estados. Caso o primeiro não tenha feito o `checkout` neste repositório, não será mostrado no comando `branch`. Mas mesmo que ele faça em alguma branch já criada pelo segundo, esta só ira aparecer no seu repositório local se tiver trazido o remoto pelo código:

```
(28) λ git pull
```

Ainda assim, mesmo com o comando (28), se não for feito o checkout, não será mostrado as novas branchs no `git branch`. Para verificar quais são as novas, utilizar a opção dada em (8.4).

### 5.3 Deletando Branch do Remoto

Os comandos para remoção da branch local podem ser revisados em (8.5) e (8.6). No entanto, para remover uma beanch de um servidor, é necessário o seguinte comando:

```
(29) λ git push --delete origin [BRANCH]
```

Tome muito cuidado com este comando caso trabalhe em grupo, pois pode ser que alguém esteja editando está branch e perderá o backup do servidor. **ATENÇÂO: ALINHE COM TODOS OS INTEGRANTES DO SEU TIME!**. Para confirmar que deu certo, abrir o GitHub e ver que a branch sumiu.

### 5.4 Renomeando uma Branch

O comando para renomear uma branch local, basta seguir as intruções abaixo:

```
(30.1) λ git branch -m [nomeANTIGO] [nomeNOVO]
(30.2) λ git branch -m [nomeNOVO]
```

Adicionar a opção `-m` ao comando branch para realizar a mudança e em seguida, digitar o nome antigo da branch, seguido do novo, caso não esteja na branch de alteração, ou apenas o novo nome se estiver.

Não é possível renomear uma branch do servidor estando localmente. Para tal realização, há um caminho específico:

1. `git pull` - para trazer as útlimas alterações do meu código remoto;
2. `git branch -m [nomeNOVO]` - para alterar o nome localmente;
3. `git push --delete origin [nomeANTIGO]` - apagar a antiga do servidor;
4. `git push -u origin [nomeNOVO]` - para mandar para servidor a branch com novo nome.
   
Mas **‼ ATENÇÂO:** para fazer este tipo de alteração, **ALINHE COM TODOS OS INTEGRANTES DO SEU TIME!**

### 5.5 Mesclando Alterações

Incorpora as alterações dos commits citados (desde o momento em que os seus históricos divergirem do ramo atual) para dentro do ramo atual. Este comando é utilizado pelo `git pull` para incorporar as alterações vindas de outro repositório e pode ser utilizado manualmente para mesclar as alterações de uma branch para outra. 

```
(31) λ git merge [BRANCH]
```

O Git merge traz as alterações já com um commit de `Merged`. Caso não queria este commit, basta utilizar a opção `--no-commit`. Uma observação importante é que o comando só realiza o commit se não existir conflitos, entretanto, se houver, é necessário tratá-los manualmente para a finalização do merge (ver subseção [5.6](#56-resolvendo-conflitos)).

Lembre-se que o merge carrega sempre o conceito de **TRAZER AS ALTERAÇÔES PARA A BRANCH ATUAL**.

### 5.6 Resolvendo Conflitos

Os conflitos acontecem quando em um mesmo arquivo, há alterações na mesma linha. Ou então quando algum desenvolvedor exclui arquivos enquanto outra pessoa faz alterações. Nesses casos, o Git não pode determinar qual está correto, sendo necessária uma resolução manual por parte do desenvolvedor que conduz o merge; o resto da equipe não fica ciente deles. O Git apenas marca os arquivos em conflito e interrompe o processo de merge. 

Geralmente o Git apresenta um primeiro aviso, sempre forçando o developer a trazer as alterações do servidor:

```
! [rejected]           main -> main (fetch first)
error: failed to push some refs to '[REMOTO]'
hint: updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

Entretanto, ao tentar dar o `git pull`, é dada a mensagem de conflito:

```
...
CONFLICT (content): Merge conflict in [ARQUIVO]
Automatic merge failed; fix conflicts and then commit the result.
```

Assim, basta abrir o editor de texto de sua preferência e decidir o que fazer com as mudanças e commitá-las para fechar o commit (no final deve ter 2 commits na frente do servidor, um do merge e o outro da alteração).

❕ **DICA**: Sempre quando for começar uma alteração no código, SEMPRE realizar um `git pull`, para evitar conflitos deste tipo.

#### 5.6.1 [kdiff3][11]

Há uma ferramenta gráfica que auxilia a resolução dos conflitos, chamada kdiff3 (software antigo - última release em 2014, mas leve e muito funcional). Ao realizar a instalação padrão do software, ir para o Git Bash e inicializar:

```
(31.1) λ git config --global --add merge.tool kdiff3
(31.2) λ git config --global --add mergetool.kdiff3.path "[DIR]"
(31.3) λ git config --global --add mergetool.kdiff3.trustExitCode false
(32) λ git mergetool
```

O arquivo .gitconfig será editado com os comandos. Para listar os comandos atuais do arquivo, basta adicionar a opção list: `git config --global --list`. Com o código (31.1) é passadi para o arquivo qual a ferramenta externa de merge será utilizada. O (31.2) configura o local que o software kdiff3 foi instalado, geralmente: "C:/Program Files/KDiff3/kdiff3.exe". Por fim, quando tiver um ambiente em conflito, utilizar (32) para que seja resolvido pelo kdiff3.

![kdiff3][kdiff3]

### 5.7 Pull Request
O pull request, é o pedido para que o repositório original, ou uma branch do repositório original, faça a ação de pull (puxar) as atualizações do repositório fork ou de um branch do próprio repositório. Depois que uma pull request é aberta, você pode discutir e revisar as possíveis alterações com colaboradores e adicionar commits de acompanhamento antes que as alterações sofram merge no branch base.

Este pedido é realizado no servidor (GitHub, GitLab, BitBucket) e feito de uma maneira visual. No GitHub pode ser feito rascunhos de pull requests em repositório público.

## 6 Mensagens de Erro e Workarounds
### 6.1 Alterações Não Versionadas
A mensagem de erro abaixa é dada sempre quando o usuário quer trocar de uma branch para a outra, mas tem alterações em arquivos da branch atual que mão foram "commitadas".

```
error: Your local changes to the following files would be overwritten by checkout:
  index.html
Please commit your changes or stash them before you switch branches.
```

Para resolvê-lo, realizar algum dos passos a seguir:
1. Commitar as mudanças na branch atual;
2. Colocar as mudanças em stash utilizando o `git stash`
3. Excluir as modificações com `git reset --hard`

### 6.2 Desfazendo commits

Quando realizar algum commit errado e quiser alterar mensagem, arquivos e qualquer alteração realizada naquele commit, seguir os passos a seguir:

1. `git commit -m "Something terribly misguided"`
2. `git reset HEAD~`
3. Editar os arquivos necessários
4. `git add .`
5. `git commit -c ORIG_HEAD`

O comando em (1) é responsável por refazer um commit. Isso irá desfazer seu último commit enquanto deixa sua árvore de trabalho (o estado de seus arquivos no disco) intocada. É preciso adicioná-los novamente antes de confirmá-los.

No item (5) é confirmado as alterações, reutilizando a mensagem de confirmação antiga. `reset` copia o antigo cabeçalho para `.git/ORIG_HEAD`; O commit com `-c ORIG_HEAD` irá abrir um editor, que inicialmente contém a mensagem de log do commit antigo e permite que você o edite. Se não precisar editar a mensagem, pode usar a opção `-C`.

**Alternativamente, para editar o commit anterior (ou apenas sua mensagem)**, `commit --amend` irá adicionar mudanças dentro do índice atual ao commit anterior.

**Para remover (não reverter) um commit que foi enviado para o servidor**, é necessário reescrever o histórico com `git push origin master --force`.

Estes dois POSTs no StackOverflow aborda maneiras diferentes de realizar o Undo & Redo de um commit: [How do I undo the most recent local commits in Git?] e [How can I move HEAD back to a previous location? (Detached head) & Undo commits]

O segundo link mostra o `git reflog`, que você pode usar para determinar o SHA-1 para o commit ao qual deseja reverter. Depois de obter esse valor, use a sequência de comandos conforme explicado acima.

## 7 Gitflow

## 8 Minhas Aliases
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




<!-- Markdown's Links
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
* -->

<!-- Markdown's Links -->
<!-- SITES -->
[1]: https://git-scm.com/
[2]: https://git-scm.com/download/linux
[3]: https://cmder.net/
[4]: https://www.cs.colostate.edu/helpdocs/vi.html
[5]: https://stackoverflow.com/questions/927358/how-do-i-undo-the-most-recent-local-commits-in-git
[6]: https://www.notion.so/jonathansmar/Comunicar-Git-e-BitBucket-d528f973813047a7a8db45d0dccf570b#7e19b5d9b12f4c5ab6055de146ceff9e
[7]: https://rdmd.readme.io/docs/code-blocks
[8]: https://www.microsoft.com/pt-br/p/windows-terminal/9n0dx20hk701#activetab=pivot:overviewtab
[9]: https://www.alura.com.br/artigos/visualstudio-code-instalacao-teclas-de-atalho-plugins-e-integracoes
[10]: https://git-school.github.io/visualizing-git/#free-remote
[11]: http://kdiff3.sourceforge.net/
[12]: https://stackoverflow.com/questions/927358/how-do-i-undo-the-most-recent-local-commits-in-git
[13]: https://stackoverflow.com/questions/34519665/how-can-i-move-head-back-to-a-previous-location-detached-head-undo-commits/34519716#34519716


<!-- ARQUIVOS -->

<!-- IMAGENS -->
[git-school]: https://kancane.nl/images/git-remote-6.png
[kdiff3]: https://cdn.kde.org/screenshots/kdiff3/diffscreen_two_way.png

<!-- COMENTÁRIOS -->
