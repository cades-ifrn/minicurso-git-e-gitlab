# git para Seres Humanos

## introdução

### o que é git

> "git is a DVCS (Distributed Version Control System)"
>
> Wikipedia

### história

Durante a maior parte do período de manutenção do *kernel* Linux (1991-2002), as mudanças no *software* eram repassadas como patches e arquivos compactados. Em 2002, o projeto do kernel do Linux começou a usar um sistema DVCS proprietário chamado BitKeeper.

Em 2005, o relacionamento entre a comunidade que desenvolvia o *kernel* e a empresa que desenvolvia comercialmente o BitKeeper se desfez, e o status de isento-de-pagamento da ferramenta foi revogado. Isso levou a comunidade de desenvolvedores Linux (em particular Linus Torvalds) a desenvolver sua própria ferramenta baseada nas lições que eles aprenderam ao usar o BitKeeper.

Alguns dos objetivos desse novo sistema eram:

- Velocidade
- Design simples
- Suporte robusto a desenvolvimento não linear (milhares de *branches* em paralelo)
- Totalmente distribuído
- Capaz de lidar eficientemente com grandes projetos como o *kernel* Linux (velocidade e volume de dados)

E desde sua concepção em 2005, o Git evoluiu e amadureceu ao ponto de ser um sistema fácil de usar e ainda assim mantér essas qualidades iniciais. Sendo rápido, bastante eficiente com grandes projetos e possuir um sistema impressionante de *branching* para desenvolvimento não-linear.

fonte: [Uma Breve História do Git](https://git-scm.com/book/pt-br/v1/Primeiros-passos-Uma-Breve-Hist%C3%B3ria-do-Git)

### git, github, gitlab e outros

O github é um serviço de hospedagem de repositórios git, assim como gitlab, bitbucket
e vários outros.

## vocabulário

### stage

O *stage*, ou palco, é:

- conjunto de alterações para um *commit*
- armazenado em um arquivo especial no caminho `.git/index`

### branch

- branch &equiv; bifurcação
- aponta para um *commit*
- a *branch* `master` é sagrada

### stash

A área de *stash* é:

- uma pilha de modificações inacabadas
- útil para troca rápida de alterações entre *branchs*

### tag

- marcar pontos importantes no histórico
- geralmente utilizado para marcar versões (*releases*)
- aponta para um *commit*

### HEAD

- aponta para o *commit* atual

## comandos locais

### `git config`

- realiza várias configurações do ambiente (local/global)

  ```bash
  git config --global user.name "nome do usuário"
  git config --global user.email email@email.com
  ```

- configura ferramentas de diff/merge

  ```bash
  git config --global diff.tool ferramenta_de_diff
  git config --global merge.tool ferramenta_de_merge
  ```

### `git init`

- usado para iniciar um repositório no diretório atual
- cria estrutura de arquivos no diretório .git

### `git add`

- adiciona arquivos inteiros ao stage

  `git add nome_do_arquivo`
- adiciona algumas das alterações de um arquivo

  `git add -i`

### `git status`

- como está o repositório local?
- exibe as modificações atuais dos arquivos

### `git commit`

- reúne as alterações do *stage* e as consolida

### `git log`

- histórico de commits da branch atual

### `git branch`

- lista branchs

  `git branch`
- cria nova branch

  `git branch nome_da_nova_branch`

### `git reset`

- remove arquivo do stage

  `git reset -- caminho_do_arquivo`
- altera a HEAD atual

  `git reset outra_ref`

### `git checkout`

O comando `git checkout` é usado para:

- alterar branch atual

  `git checkout nome_da_branch`
- criar nova branch a partir da HEAD atual

  `git checkout -b nome_da_nova_branch`

### `git stash`

- guarda alterações em uma área separada

  `git stash`
- aplica as alterações separadas por último

  `git stash apply`

### `git archive`

- cria snapshot/backup do repositório

  `git archive HEAD -o arquivo_de_saida.zip`

## comandos remotos

### `git clone`

- cria uma cópia a partir de um repositório remoto

  `git clone url_do_repositorio_remoto`

### `git remote`

- gerencia servidores remotos

  `git remote add nome_do_remote url_do_remote`

  `git remote rm nome_do_remote`
- lista os repositórios remotos

  `git remote -v`
- `origin` é o nome de *remote* padrão após um `clone`

### `git push`

- `push` == empurar
- envia informações locais para um repositório remoto

  `git push nome_do_remote`
- também pode ser usado para apagar *refs* de um *remote*

  `git push nome_do_remote :nome_da_ref`

### `git pull`

- pull &equiv; puxar
- baixa alterações de um *remote* e integra na *branch* atual

### `git fetch`

- somente baixa as alterações de um *remote*

  `git fetch nome_do_remote`

- as *refs* remotas são disponibilizadas localmente com o prexifo `nome_do_remote/`, ex.:

  `nome_do_remote/master`

## manipulando commits

### com o comando `git commit`

- corrigir* commit apontado por hash_de_um_commit

  `git commit --fixup hash_de_um_commit`
- corrigir último commit

  `git commit --amend`

\* necessita de um *rebase* posterior

### com o comando `git rebase`

`git rebase -i` para manipulação de forma interativa e explicativa

- edição de commits
- reordenação commits
- remoção de commits

## comando salva-vidas

- aplicar alterações de um *commit* na *HEAD* atual

  `git cherry-pick hash_ou_ref_do_commit`
- realiza operações em referências perdidas*

  `git reflog`
- quem mecheu no meu código?

  `git blame nome_do_arquivo`
- busca por *commit* que introduziu um *bug*

  `git bisect ref_bugada ref_ok`

\* útil em caso de perda de commits

## ferramentas gráficas

- `gitk`: visualização do histórico
- `git-cola`: edição de commits
- `meld`: visualização de alterações
- `gitkraken`: solução gráfica completa
- `github desktop`: solução gráfica completa

## boas práticas

- fazer *commits* auto-contidos
- realizar *merge/pull requests*
- criar *forks*
- versionamento semântico via *tags*

### forks

- o fork é meu e eu faço o que eu "quiser"
- impede trabalho inacabado no repositório oficial
- permite a alteração da `master` sem problemas

### resolução de conflitos

- resolução de conflitos é uma tarefa complexa
- converse com quem fez a alteração conflituosa
- algumas ferramentas gráficas reduzem a dor:
  * `git-cola`
  * `meld`
