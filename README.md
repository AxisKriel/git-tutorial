# Git Tutorial

> Qualidade de Software | Mestrado em Engenharia de Software @ IPSetúbal
> 

> João Damásio <joao.damasio@estudantes.ips.pt>
> 

> Rodrigo Rente <rodrigo.rente@estudantes.ips.pt>
> 

## Índice

1. [Introdução](#introdução)
2. [Objetivos](#objetivos)
3. [Instalação](#instalação)
4. [Configuração](#configuração)
5. [Novo Projeto](#novo-projeto)
6. [Registo de Alterações](#registo-de-alterações)
7. [Ramos e Histórico de Alterações](#ramos-e-histórico-de-alterações)
8. [Colaboração e Repositórios Remotos](#colaboração-e-repositórios-remotos)

## Introdução

O Git é um sistema de controlo de versões distribuído, usado principalmente no desenvolvimento de software, mas pode ser usado para registar o histórico de edições de qualquer tipo de ficheiro (Exemplo: alguns livros digitais são disponibilizados no GitHub e escrito aos poucos publicamente). 

O Git foi inicialmente projetado e desenvolvido por Linus Torvalds para o desenvolvimento do kernel Linux, mas foi adotado por muitos outros projetos.

Cada diretório do Git é um repositório com um histórico completo e capacidade total de acompanhamento das revisões, não dependente do acesso a uma rede ou a um servidor central.

O Git também facilita a reprodutibilidade científica em uma ampla gama de disciplinas, da ecologia à bioinformática, arqueologia à zoologia.

O Git é um software livre, distribuído sob os termos da versão 2 da GNU General Public License. A sua manutenção é atualmente supervisionada por Junio Hamano.

[Git](https://git-scm.com)

Website do Git.

## Objetivos

Após concluir este tutorial, o utilizador terá os seguintes conhecimentos:

- Conhecimento básico sobre a movimentação entre pastas, criar diretórios e ficheiros utilizando a consola Git Bash, que é muito semelhante à terminal dos sistemas Linux;
- Instalação do git e configuração inicial da conta de utilizador;
- Criação de um novo repositório e registo de alterações através dos commits;
- Utilização de vários ramos e como utilizar o merge para implementar novas funcionalidades no ramo base do projeto;
- Como utilizar um repositório remoto e colaborar com outros utilizadores em plataformas tais como o GitHub.

## Instalação

1. Download do GIT: [https://git-scm.com/downloads](https://git-scm.com/downloads)
2. Após o download concluir, executar o ficheiro de instalação.
3. Escolher o local de instalação e avançar com todas as restantes opções do predefinido, que permitirá concluir este tutorial sem qualquer problema.

<aside>
💡 A instalação predefinida introduz o git na variável `PATH` do utilizador, o que permite utilizar o git de qualquer janela da consola do Windows. Não obstante, neste tutorial iremos utilizar o Git Bash como consola, pelo que é possível resolvê-lo mesmo que prefira não selecionar esta opção.

</aside>

## Configuração

1. Abrir a Git Bash com o atalho: `WIN+S` pesquisando por “Git Bash”.

<aside>
💡 O Bash abre por defeito na pasta HOME, que é definida como a pasta do utilizador atual (C:/Users/NomeDeUtilizador/). O caminho até esta pasta é encurtado para apenas “~”.

</aside>

1. Através do comando `git config`, é possível configurar o essencial de forma a permitir a realização de commits:

```bash
$ git config --global user.name "O Teu Nome"
$ git config --global user.email oteuemail@estudantes.ips.pt
```

1. Caso pretenda verificar se ficou tudo bem configurado, é possível fazê-lo utilizando os mesmos comandos, mas sem a parte final. Por exemplo, `git config --global user.name` imprime “O Teu Nome”.

## Novo Projeto

1. Criar uma pasta comum para todos os projetos Git. Neste tutorial, escolhemos o nome padrão `src` no entanto fica ao critério do utilizador.

```bash
# MKDIR <name>: cria uma pasta com o nome atribuído
$ mkdir src

# CD <path>: muda o diretório atual do Bash
$ cd src
```

1. À semelhança do anterior, criar uma pasta para o tutorial com o nome `tutorial`. Após este passo e mudando para a nova pasta, o diretório do Bash deve ser o seguinte: `~/src/tutorial/`.
2. Agora que estamos na pasta correta, vamos criar um novo repositório Git.

```bash
# GIT INIT [path]: cria um novo repositório no diretório atual ou no caminho indicado
$ git init
```

1. Em caso de sucesso, o Bash deverá ter dado a seguinte resposta:

```bash
Initialized empty Git repository in .git/
```

Agora já temos um novo repositório Git no diretório atual. Isto cria uma pasta escondida `.git` onde são guardadas as informações do repositório.

## Registo de Alterações

1. Adicionar um ficheiro de texto com um conteúdo básico:

```bash
# De forma simples, o ECHO envia o texto "Hello World!" para o ficheiro "hello.txt"
$ echo "Hello World!" > hello.txt

# Quando usado apenas com um ficheiro, o CAT lê os seus conteúdos para o Bash
$ cat hello.txt
Hello World!
```

1. O comando `git status` mostra o estado atual do repositório. Neste momento, deve mostrar que existe 1 untracked file, o ficheiro `hello.txt` .
2. Adicionar o ficheiro que acabámos de criar ao próximo commit, através do comando `git add`:

```bash
$ git add hello.txt
```

<aside>
💡 Caso pretendamos adicionar todos os ficheiros de um diretório ao registo, também podemos utilizar o seguinte comando: `git add .`

</aside>

<aside>
📌 Se adicionarmos algo por engano, podemos remover com `git remove <file>`

</aside>

1. Fazer o commit inicial do repositório através do comando `git commit`:

```bash
git commit -m "Initial commit"
```

Este comando faz o registo das alterações existentes, com a mensagem que vem a seguir ao `-m`. É importante incluir as aspas para a mensagem possa ter mais do uma palavra! Uma boa prática é utilizar uma descrição simples e objetiva, existe um conjunto de boas-práticas para as mensagens do commit no final do tutorial.

1. Para verificar que já não existem alterações pendentes, utilizamos o comando `git status`, que indica o estado atual da working tree. Agora, deverá dizer que não existe nada para registar.

## Ramos e Histórico de Alterações

Os ramos do git são um boa forma de manter o trabalho de várias features diferentes isolado, para que possa ser desenvolvido sem conflitos até chegar à altura de a acrescentar ao ramo master.

Quando queremos experimentar algo novo é uma boa prática criar um ramo novo antes de o fazer. Assim, caso não resulta da forma que esperámos, podemos sempre voltar ao estado anterior dos ficheiros.

- Nomes genéricos dos ramos padrão do git:
    - Development [ `dev`, `gen-devel`, `general-devel` ]
    - Master [ `master` ]
    - Testing [ `tests`, `testing`, `qa` ]
1. Mudar para um novo ramo `dev`: 

```bash
git checkout -b dev
```

O argumento `-b` cria o ramo caso não exista. Voltarmos ao ramo principal, basta fazer `git checkout master`. No entanto, não o iremos fazer agora pois temos alterações a fazer no ramo `dev`.

Eis as bases de alguns comandos importantes nesta fase:

- O `git commit` regista as alterações no ramo em que nos encontramos quando o usamos.
- O `git log` mostra o histórico de todos os commits com a mensagem resumida das alterações. Outra forma de ver o histórico de forma mais visual é com o comando `gitk`.
- O `git branch [name]` é outra forma de criar ramos, neste caso sem alterar automaticamente o ramo atual.
    - `git branch -d [name]` apaga um ramo.
1. No ramo `dev` que criámos há pouco, vamos fazer algumas alterações:

```bash
$ echo "This is my first Git Repository" > readme.txt

# Ao utilizarmos o operador >>, vamos acrescentar o seguinte ao fim do ficheiro
$ echo "Goodbye World!" >> hello.txt

# Agora o ficheiro deve ter duas linhas
$ cat hello.txt
Hello World!
Goodbye World!
```

<aside>
💡 Também é possível remover ficheiros através do Bash, com o comando `rm <file>`

</aside>

1. Fazer `git commit` destas alterações, que ficarão registadas no ramo `dev`.
2. Agora voltamos ao ramo master: `git checkout master`.
3. Entretanto decidimos que as alterações de desenvolvimento já estão prontas para serem implementadas, pelo que vamos fazer um merge:

```bash
git merge dev
```

- O comando `git merge <ramo>` faz merge entre dois ramos — este comando tenta fazer merge automático entre todas as alterações de um `<ramo>` e introduzi-las por cima do ramo ATUAL.
- Todos os commits que foram feitos no ramo `dev` antes do merge também passarão a existir no ramo `master`.
- Se fizermos `git log` ou `gitk` é possível ver através de uma representação visual, onde foi feito o merge a partir de outro ramo.

## Colaboração e Repositórios Remotos

Esta seção aplica os vários conhecimentos obtidos, está construída de forma mais abstrata de modo a aplicar estes conhecimentos.

Esta seção pode ser feita a pares, para a parte da colaboração. Caso contrário, também é possível simular através da utilização de pastas diferentes (no entanto, os commits ficarão registados como sendo todos da mesma pessoa).

Para fazer com outra pessoa, é necessário ir às definições do GitHub e adicionar a conta dessa pessoa como Colaborador, para que tenha permissões para fazer `git push`. No entanto, qualquer pessoa pode fazer `git clone` de qualquer repositório, desde que seja público.

1. Criar de uma conta no GitHub: [https://github.com](https://github.com/)
2. Criar um repositório simples no GitHub com o nome `tutorial`. Para facilitar a colaboração, o ideal será deixar o repositório público.
3. Adicionar as permissões necessárias nas definições do repositório caso pretenda que outro utilizador faça commits para este repositório.
4. Para adicionar o nosso repositório do GitHub como origem do nosso repositório local:

```bash
# Copiar o URL do nosso novo repositório no GitHub para utilizar aqui:
$ git remote add origin LINK_PARA_O_NOSSO_REPOSITORIO_NO_GITHUB
```

1. Fazer `push` para esse repositório do nosso conteúdo

```bash
# Enviar para o nosso repositório "origin", todas as alterações ao ramo "master"
$ git push origin master
```

<aside>
💡 Ao tentar fazer push para um repositório remoto, o Bash deverá pedir para nos autenticarmos com as nossas credenciais do GitHub

</aside>

<aside>
📌 Se houver um erro ao fazer push, pode ser porque existem alterações remotas que não existem no registo do repositório local, pelo que devemos fazer primeiro um pull através do comando `git pull`

</aside>

1. Fazer `clone` do repositório do colega, ou numa pasta diferente:

```bash
# Descarrega o código de um repositório remoto
# Como não introduzimos nenhum parametro, o clone irá para uma pasta
# com o nome do repositório
$ git clone LINK_DO_REPOSITÓRIO_REMOTO
```

1. Fazer uma alteração simples ao ficheiro e consequentemente `commit` e `push` para submeter as alterações no repositório remoto.
2. No computador original, para descarregar as alterações basta utilizar o `git pull`.

Através deste ciclo, já é possível desenvolver software em colaboração com outros.

## Fontes

[Git - gittutorial Documentation](https://git-scm.com/docs/gittutorial)

Official Git Tutorial

[Git Branch Naming Convention: 7 Best Practices to Follow | HackerNoon](https://hackernoon.com/git-branch-naming-convention-7-best-practices-to-follow-1c2l33g2)

Padrões para os nomes dos ramos do git.

[Commit message guidelines](https://gist.github.com/robertpainsi/b632364184e70900af4ab688decf6f53)

Boas práticas para as mensagems dos commits.
