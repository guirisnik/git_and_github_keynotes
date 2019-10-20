# 1. O que é o Git?
Git é um sistema de controle de versão distribuido (DVCS, em inglês). Isso significa que a cópia do repositório de cada usuário/desenvolvedor também é um repositório completo, com todo o histórico do projeto, em contraste com sistemas CVS ou SVN que possuem apenas um repositório mestre com todas as informações e histórico.

===========================================

## Como ele guarda informações?
Ao contrário da maioria dos programas de versionamento que armazena um histórico de mudanças, o git armazena snapshots, que representam o estado completo do projeto num período específico e essa snapshot identificada por uma chave (hash) numa blob (acrônimo de binary large object, uma grande bolha de dados).

============================================

## O que são branches?
Quando você inicia um repositório, é como marcar um ponto de partida e plantar uma semente de uma árvore. Conforme seu projeto cresce, você incrementa arquivos, acrescenta novos arquivos, pastas, etc. e cada etapa de desenvolvimento que termina é marcada por um commit (um objeto da árvore).
Assim, um branch (galho) é uma forma de apontar (selecionar) um commit, sendo que o branch default é o master, que não tem nada de especial por ter esse nome, ele é criado com o início do repositório e, na maioria das vezes, ninguém muda o nome dele.

============================================

## Então o que acontece quando eu crio um novo branch?
Você está apenas criando outro apontador de commits para se movimentar pela árvore do seu projeto. Isso é útil para criar diferentes estados do projeto (por exemplo um branch de staging e outro de prod).

============================================

## Como o git sabe para qual branch ele tem que olhar?
Existe outro apontador que é o mestre de todos os branches chamado de HEAD. Assim, o HEAD é quem decide qual branch que está comandando o estado atual do projeto que você enxerga.

============================================

## Ok, mas ainda não entendi a utilidade disso tudo:
O melhor cenário para entender isso é pensar num projeto grande e você precisar comandar seu único branch master entre seus commits de staging, prod e quaisquer outros. Você teria que procurar o commit toda vez que quisesse mudar para algum estado específico do projeto e então reverter os estados ou fazer um checkout... enfim, é algo trabalhoso. Com os branches, você pode usá-los como se fossem marcadores de página ou índices do seu projeto.
Assim, quando necessário, basta trocar o HEAD para o branch desejado (que terá um nome intuitivo ao invés de um hash muito doido) para navegar pela árvore do seu projeto até pontos de interesse.
Essa é uma das utilidades de branching. A outra não menos importante é de testar novas funcionalidade sem quebrar o código que está hospedado em algum lugar servindo a uma aplicação. O branch de prod é aquele que está sendo usado de fato, mas o branch de staging continua fazendo commits e incrementando a árvore do seu projeto sem quebrar a aplicação principal. Quando estiver seguro das mudanças, esses branches podem ser fundidos.

============================================

# Mensagens de commit:
É uma boa prática escrever mensagens de até 50 caractéres (legibilidade do log) com o formato:
<Ação> <Objeto> <Local>

<Ação>: O que você fez? Correção, Adição, Remoção (evite "modificação", por exemplo, que não transmite logo de cara o conteúdo do commit, prefira um dos três primeiros);

<Objeto>: Em que você fez? função xyz, mensagem abc (evite longas descrições, deixe elas para o corpo do commit e não para o cabeçalho)

<Local>: Aonde você fez? Pode até ser omitido dependendo da situação, mas para funções ou códigos mais longos separados por seções pode ser útil apontar aonde está a mudança;

============================================

# Git vs Github:

Não são a mesma coisa.

Github é um site, um serviço que usa Git.

Git é um sistema de versionamento independente do Github. Você pode usar Git e armazenar seu código no google drive, por exemplo. O versionamento é feito pelo Git e o armazenamento é feito pelo drive.

O Github é um serviço que facilita o uso do Git porque acrescenta um front-end ao Git, mostrando número de commits, versões, mudanças em arquivos, entre outros.

============================================

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