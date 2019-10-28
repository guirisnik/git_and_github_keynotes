# Git

## O que é o Git?
Git é um sistema de controle de versão distribuido (DVCS, em inglês). Isso significa que a cópia do repositório de cada usuário/desenvolvedor também é um repositório completo, com todo o histórico do projeto; as versões de um projeto não são centralizadas e cada usuário que quiser contribuir pode manter alterações localmente como se fosse o projeto principal, em contraste com sistemas CVS ou SVN que possuem apenas um repositório mestre com todas as informações e histórico. 
*site oficial:* (https://git-scm.com/)

### Como o Git guarda seu projeto?
Ao contrário da maioria dos programas de versionamento que armazena um histórico de mudanças, o git armazena snapshots, que representam o estado completo do projeto num período específico e essa snapshot identificada por uma chave (hash) numa blob (acrônimo de binary large object, uma grande bolha de dados).  
Isso significa que é muito mais simples de retornar a qualquer período do projeto caso aconteça algum problema ou queira verificar o estado do projeto num ponto anterior (Se já usou outras ferramentas de controle de versão sabe que esse tipo de tarefa é um Golias quando o projeto precisa de um rollback).

## Instalação
### Onde eu acho o arquivo de instalação?
Para instalar, procure na seção de Downloads ou clique (https://github.com/git-for-windows/git/releases/download/v2.23.0.windows.1/Git-2.23.0-64-bit.exe "aqui") para baixar a versão 2.23.0 64 bits para Windows.

### Processo de instalação
Pode ser um simples "next next next ...", mas tem alguns detalhes interessantes que podem ser alterados para aproveitar melhor a ferramenta.

1. Default Editor
É interessante, *mas não obrigatório*, colocar como editor padrão o Git na sua ferramenta de edição de código (seja lá qual for, VSCode, PyCharm, Notepad++, etc.). Facilita o uso dos comandos já que, muito provavelmente, é por lá que os projetos serão feitos e controlados.

2. Adição do Git no PATH
Colocar o Git na variável de ambiente PATH significa que o usuário pode usar os comandos de qualquer terminal (cmd, PowerShell, etc.). Recomendo usar o Git Bash (o terminal que é instalado com o Git) porque é mais parecido com terminal Unix.

O restante é next, next, next ...

## Comandos Básicos:
### git init
Cria a estrutura de controle de versão no diretório atual. Também pode ser usado especificando o diretório no formato:

>`git init <path>`

### git add <file1> <file2> ...
Adiciona arquivos na pilha de commit. Costuma-se dizer que esses arquivos estão *staged*.
Para adicionar todos os arquivos do diretório o comando pode ser especificado no formato:

>`git add .`

### git reset <file1> <file2> ...
Remove arquivos que foram colocados na pilha de commit. Para remover todos os arquivos, basta escrever o comando:

>`git reset` (sem o ponto)

### git commit -m "<message>"
Cria o commit no *branch* atual. Um commit é uma foto do estado atual dos arquivos que estavam na pilha (que estavam *staged*). É dessa forma que o Git grava as informações do projeto.

### git branch <name>
Cria um novo branch com nome <name>.  

Quando um projeto é iniciado, é como marcar um ponto de partida e plantar uma semente de uma árvore. Conforme seu projeto cresce, você *incrementa* arquivos, *acrescenta novos* arquivos, pastas, etc. e cada etapa de desenvolvimento que termina é marcada por um *commit* (um objeto da árvore).  

Assim, um *branch* (galho) é uma ramificação do projeto, uma forma de *apontar* (selecionar) um commit específico, sendo que o branch default é o *master*, que não tem nada de especial por ter esse nome, ele é criado com o início do repositório e, na maioria das vezes, ninguém muda o nome dele.  

Cada projeto possui diferentes necessidades de *workflow*, mas é comum adotar a estrutura de branches a seguir:

| *Nome do branch*     | *Descrição*                                 |
| ------------------   | ------------------------------------------- |
| `master`             | branch de produção                          |
| `dev` ou `staging`   | branch de desenvolvimento de novas features |
| `topics` ou `issues` | branch de solução de problemas              |

#### Então o que acontece quando eu crio um novo branch?
Você está apenas criando outro apontador de commits para se movimentar pela árvore do seu projeto. Isso é útil para criar diferentes estados do projeto, por exemplo um branch de *staging/desenvolvimento*, outro de *prod* (que geralmente é o *master*) e, caso necessário, *topic branches* para solução de bugs do projeto relatados pelos usuários.

#### Como o git sabe para qual branch ele tem que olhar?
Existe outro *apontador* que é o mestre de todos os branches chamado de *HEAD*, que é quem decide qual branch está comandando o estado atual do projeto que você enxerga.

#### Ok, mas ainda não entendi a utilidade disso tudo:
O melhor cenário para entender isso é pensar num projeto grande e você precisar comandar seu único branch *master* entre seus commits de *staging*, *prod* e quaisquer outros. Você teria que procurar o commit toda vez que quisesse mudar para algum estado específico do projeto e então reverter os estados ou fazer um checkout... enfim, é algo trabalhoso. Com os *branches*, você pode usá-los como se fossem marcadores de página ou índices do seu projeto. Além disso, é possível ramificar alterações a partir de qualquer ponto da árvore do projeto para desenvolver novas features sem alterar o estado de produção estável.
Assim, quando necessário, basta trocar o *HEAD* para o branch desejado (que terá um nome intuitivo ao invés de um hash muito doido) para navegar pela árvore do seu projeto até pontos de interesse.

### git merge <branch_name_1> <branch_name_2> ...
Uma das formas de juntar dois ou mais *branches* (também chamados *histories*) ao *branch* atual.  
Um exemplo visual que ajuda a entender uma situação de merge é a seguinte:
Digamos que seu *branch* de produção está no estado *D* e, paralelamente, você esteve trabalhando na solução de um bug desde a versão *B*

>       E---F---G   iss#1
>      /
> A---B---C---D     master

Então na versão *G* do bug você resolveu o problema de forma estável e está confiante em associar as mudanças ao *branch* de produção na versão *D*. Para isso você executa o comando *git merge iss#1* com o *HEAD* do projeto no *master*. Assim a árvore do projeto deverá resultar em:

>       E---F---G    iss#1
>      /         \
> A---B---C---D---H  master

# Mensagens de commit:
É uma boa prática escrever mensagens de até 50 caractéres (legibilidade do log) com o formato:
<Ação> <Objeto> <Local>

<Ação>: O que você fez? Correção, Adição, Remoção (evite "modificação", por exemplo, que não transmite logo de cara o conteúdo do commit, prefira um dos três primeiros);

<Objeto>: Em que você fez? função xyz, mensagem abc (evite longas descrições, deixe elas para o corpo do commit e não para o cabeçalho)

<Local>: Aonde você fez? Pode até ser omitido dependendo da situação, mas para funções ou códigos mais longos separados por seções pode ser útil apontar aonde está a mudança;



# Git vs Github:

Não são a mesma coisa.

Github é um site, um serviço que usa Git.

Git é um sistema de versionamento independente do Github. Você pode usar Git e armazenar seu código no google drive, por exemplo. O versionamento é feito pelo Git e o armazenamento é feito pelo drive.

O Github é um serviço que facilita o uso do Git porque acrescenta um front-end ao Git, mostrando número de commits, versões, mudanças em arquivos, entre outros.



# 2. Comandos básicos:
## git init <path>
Inicializa o versionamento no repositório atual. Esse comando cria uma pasta chamada .git oculta com toda a estrutura necessária para gerenciar as versões do projeto

## git status <path>
Mostra o estado do projeto: qual é o branch, se existem arquivos não rastreados, quais arquivos estão na fila de commit, etc.

## git add <file>
Adiciona arquivos na fila de commit para serem rastreados.

## git commit -m "<comment>"
Faz commit dos arquivos na fila e guarda a atualização sob a descrição do <comment>

## git log
Mostra o histórico de commits o hash do commit, autor, data e mensagem. O hash é o código único do commit, que é o que permite com que o sistema consiga retornar a uma versão anterior do projeto usando o próximo comando.

## git checkout <commit_hash>
Retorna o projeto ao estado do commit específico ao hash que foi passado. Caso tenham mudanças que não foram commitadas no projeto, o git lança um erro pedindo que você faça o commit ou que você "empilhe" a sua sujeira, em outras palavras, ele quer que você crie um stash do seu trabalho, que você arrume a mesa com a papelada do projeto atual, guarde numa pasta e pegue seus outros materiais de trabalho que precisam de atenção naquele momento.
Pense no checkout como uma máquina do tempo. É possível voltar a um período no projeto em que alguma pasta ou arquivo não existia e, de fato, quando o checkout é feito esse arquivo não estará mais no repositório, mas ele continua existindo no master branch
A ideia que o Git passa é a de que cada commit representa um corpo diferente e, quando você muda de branch ou para um commit anterior, você desconecta a cabeça do corpo master e liga ela a um corpo anterior para poder movimentar aquele corpo e ter a perspectiva antiga.

## git stash
Cria uma pilha com seu trabalho inacabado. É útil quando você precisa mudar de branch para trabalhar em outra coisa e não quer guardar um commit que não contribui para o projeto, uma vez que o que estava fazendo ainda não foi terminado.
Cada git stash cria uma pilha diferente que pode ser vista com git stash list e, para retomar uma stash usa-se git stash apply <stash_id>

## git revert --no-commit <commit_hash>..HEAD
Recria o estado de commit específico daquele hash como se cada commit fosse revogado até aquele ponto. Isso é uma atitude um pouco drástica de revogar commits até um determinado período.
A diferença entre git checkout e este comando é que o primeiro é apenas uma viagem no tempo visual, ou seja, você pode ver como o projeto era, os arquivos que existiam na época, etc.; já o segundo é um passo que permite que você recomece o projeto a partir daquele período, dando novos commits, modificando arquivos, etc.