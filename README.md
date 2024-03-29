# Índice

1. [Introdução](#introdução)
2. [Git](#git)
    1. [O que é o Git?](#o-que-é-o-git)
    2. [Por que preciso disso?](#por-que-preciso-disso)
    3. [Como ele funciona?](#como-ele-funciona)
    4. [Instalação](#instalação)
    5. [Comandos Básicos](#comandos-básicos)
    6. [Comandos Auxiliares](#comandos-auxiliares)
3. [GitHub](#github)
    1. [Aplicativo Desktop](#aplicativo-desktop)
    2. [Repositório (Repo)](#repositório-repo)
    3. [Como criar um repositório](#como-criar-um-repositório)
    4. [Criando um branch](#criando-um-branch)
    5. [Fazendo um commit](#fazendo-um-commit)
    6. [Pull Request (PR)](#pull-request-pr)

# Introdução

Este documento apresenta duas ferramentas: __Git__ e __GitHub__. Não é necessário saber sobre o Git para usar o GitHub.

O __GitHub__ é um serviço que utiliza o __Git__ para armazenar projetos na nuvem, enquanto que o __Git__ é uma ferramenta de controle de versão que opera localmente no seu pc.

Assim, se preferir, pode ir direto à seção sobre [GitHub](#github), mas eu aconselho passar pela seção do [Git](#git) também para que tenha alguma ideia de como ele funciona (é bom saber na hora de resolver conflitos no seu projeto).

# Git

## O que é o Git?
Git é um software de versionamento, ou seja, um software que guarda informações sobre o seu projeto num estado específico.

## Por que preciso disso?
Basicamente para controle. Um software de versionamento mantém registros de cada modificação feita no seu projeto, o que significa que, caso algum erro seja cometido no desenvolvimento, é possível retornar para um estado anterior do seu projeto e comparar com versões anteriores, o que auxilia na solução do problema.

## Como ele funciona?
O Git armazena os dados do seu projeto numa base de dados especial, em que cada estado do seu projeto é representado por um __commit__.

Esses estados são chamados de _snapshots_, que são fotografias do seu projeto num momento específico. É dessa forma que o Git consegue recriar o seu projeto caso seja necessário retornar a um estado anterior, o Git simplesmente pega a foto do seu projeto naquele ponto anterior e mostra pra você como era o seu projeto, mostrando arquivos que talvez não existam mais e deixando de mostrar arquivos que foram criados em estados posteriores àquele.

Cada __commit__ ou _snapshot_ é indicada por uma chave, que é como se fosse o nome da foto. Assim, quando é necessário retornar o projeto para aquele momento, basta dizer ao Git esse nome que ele cuida do resto.

__site oficial:__ https://git-scm.com/

## Instalação
### Onde eu acho o arquivo de instalação?
Para instalar, procure na seção de Downloads ou clique <a href="https://github.com/git-for-windows/git/releases/download/v2.23.0.windows.1/Git-2.23.0-64-bit.exe">aqui</a> para baixar a versão 2.23.0 64 bits para Windows.

### Processo de instalação
Pode ser um simples "next next next ...", mas tem alguns detalhes interessantes que podem ser alterados para aproveitar melhor a ferramenta.

1. __Default Editor__
É interessante, __mas não obrigatório__, colocar como editor padrão o Git na sua ferramenta de edição de código (seja lá qual for, VSCode, PyCharm, Notepad++, etc.). Facilita o uso dos comandos já que, muito provavelmente, é por lá que os projetos serão feitos e controlados.

![Default Editor](./resources/img/git/default_editor.png)

2. __Adição do Git no PATH__
Colocar o Git na variável de ambiente PATH significa que o usuário pode usar os comandos de qualquer terminal (cmd, PowerShell, etc.). Recomendo usar o Git Bash (o terminal que é instalado com o Git) porque é mais parecido com terminal do Linux (os comandos são diferentes do terminal padrão do Windows).

![Git PATH](./resources/img/git/git_path.png)

O restante é next, next, next ...

# Comandos Básicos:

## git init
Cria a estrutura de controle de versão no diretório atual. Também pode ser usado especificando o diretório no formato:

>`git init path`

## git add \<file1\> \<file2\> ...
Adiciona arquivos na pilha de __commit__. Costuma-se dizer que esses arquivos estão __staged__.
Para adicionar todos os arquivos do diretório o comando pode ser especificado no formato:

>`git add .`

## git reset \<file1\> \<file2\> ...
Remove arquivos que foram colocados na pilha de __commit__. Para remover todos os arquivos, basta escrever o comando:

>`git reset` (sem o ponto)

## git commit -m "Fix/Add/Remove something something"
Cria o __commit__ no [__branch__](#git-branch-name) atual. Um __commit__ é uma foto do estado atual dos arquivos que estavam na pilha (que estavam __staged__). É dessa forma que o Git grava as informações do projeto.

Quando uma mensagem curta não é descritiva o suficiente das alterações é recomendado escrever um pequeno parágrafo sobre o __commit__ no formato:

> git commit -m "Fix/Add/Remove something something
>
> This paragraph describes the changes made  
> more in-depth to the project.

### Mensagens de commit
É uma boa prática escrever títulos de até 50 caractéres (legibilidade do log) com o formato:
__\<Ação\> \<Objeto\> \<Local\>__

__Ação:__ O que você fez? Correção, Adição, Remoção (evite "modificação", por exemplo, que não transmite logo de cara o conteúdo do __commit__, prefira um dos três primeiros);

__Objeto:__ Em que você fez? função xyz, mensagem abc (evite longas descrições, deixe elas para o corpo do __commit__ e não para o cabeçalho)

__Local:__ Aonde você fez? Pode até ser omitido dependendo da situação, mas para funções ou códigos mais longos separados por seções pode ser útil apontar aonde está a mudança;


## git branch \<name\>
Cria um novo branch com nome __\<name\>__.  

Quando um projeto é iniciado, é como marcar um ponto de partida e plantar uma semente de uma árvore. Conforme seu projeto cresce, você __incrementa__ arquivos, __acrescenta novos__ arquivos, pastas, etc. e cada etapa de desenvolvimento que termina é marcada por um __commit__ (um objeto da árvore).  

Assim, um __branch__ (galho) é uma ramificação do projeto, uma forma de __apontar__ (selecionar) um __commit__ específico, sendo que o branch default é o __master__, que não tem nada de especial por ter esse nome, ele é criado com o início do diretório do Git, ou seja, quando você executa o comando

>`git init`

e, na maioria das vezes, ninguém muda o nome dele.  

Cada projeto possui diferentes necessidades de __workflow__, mas é comum adotar a estrutura de branches a seguir:

| __Nome do branch__   | __Descrição__                               |
| ------------------   | ------------------------------------------- |
| `master`             | branch de produção                          |
| `dev` ou `staging`   | branch de desenvolvimento de novas features |
| `topics` ou `issues` | branch de solução de problemas              |

### Então o que acontece quando eu crio um novo branch?
Você está apenas criando outro apontador de __commits__ para se movimentar pela árvore do seu projeto. Isso é útil para criar diferentes estados do projeto, por exemplo um branch de __staging/desenvolvimento__, outro de __prod__ (que geralmente é o __master__) e, caso necessário, __topic branches__ para solução de bugs do projeto relatados pelos usuários.

### Como o git sabe para qual branch ele tem que olhar?
Existe outro __apontador__ que é o mestre de todos os branches chamado de __HEAD__, que é quem decide qual branch está comandando o estado atual do projeto que você enxerga.

### Ok, mas ainda não entendi a utilidade disso tudo:
O melhor cenário para entender isso é pensar num projeto grande e você precisar comandar seu único branch __master__ entre seus __commits__ de __staging__, __prod__ e quaisquer outros. Você teria que procurar o __commit__ toda vez que quisesse mudar para algum estado específico do projeto e então reverter os estados ou fazer um checkout... enfim, é algo trabalhoso. Com os __branches__, você pode usá-los como se fossem marcadores de página ou índices do seu projeto. Além disso, é possível ramificar alterações a partir de qualquer ponto da árvore do projeto para desenvolver novas features sem alterar o estado de produção estável.
Assim, quando necessário, basta trocar o __HEAD__ para o branch desejado (que terá um nome intuitivo ao invés de um hash muito doido) para navegar pela árvore do seu projeto até pontos de interesse.

## git merge \<branch_name_1\> \<branch_name_2\> ...
Uma das formas de juntar dois ou mais __branches__ (também chamados __histories__) ao __branch__ atual.  
Um exemplo visual que ajuda a entender uma situação de __merge__ é a seguinte:
Digamos que seu __branch__ de produção está no estado __D__ e, paralelamente, você esteve trabalhando na solução de um bug desde a versão __B__:

>
>            E---F---G   iss#1
>           /
>      A---B---C---D     master
>

Então na versão __G__ do bug você resolveu o problema de forma estável e está confiante em associar as mudanças ao __branch__ de produção na versão __D__. Para isso você executa o comando __git merge iss#1__ com o __HEAD__ do projeto no __master__. Assim a árvore do projeto deverá resultar em:

>
>            E---F---G    iss#1
>           /         \
>      A---B---C---D---H  master
>

Dessa forma integramos (ou mergeamos) as implementações do branch `iss#1` ao `master`.

## git rebase \<branch_name_1\> \<branch_name_2\> ...
Outra forma de integrar mudanças de um ou mais __branches__ ao __branch__ atual.
Diferente do commando __merge__, o comando de __rebase__ reconstrói o projeto para unificar ramificações, ou seja, ao invés de juntar mudanças feitas em dois ramos em um estado novo como foi visto no comando de __merge__, o comando de __rebase__ irá recriar a árvore do projeto desde o ponto de ramificação e irá criar uma nova estrura linear com todas as mudanças.

Um exemplo visual que ajuda a entender a situação de __rebase__ é a seguinte:
Digamos que seu __branch__ de produção está no estado __D__ e, paralelamente, você esteve trabalhando na solução de um bug desde a versão __B__:

>
>            E---F---G   iss#1
>           /
>      A---B---C---D     master
>

Então na versão __G__ do bug você resolveu o problema de forma estável e está confiante em associar as mudanças ao __branch__ de produção na versão __D__. Para isso você executa o comando __git rebase iss#1__ com o __HEAD__ do projeto no __master__. Assim a árvore do projeto deverá resultar em:

>
>                    E---F---G    iss#1
>                   /
>      A---B---C---D              master
>

Dessa forma, reestrutura-se o projeto como se o __branch iss#1__ fosse integrado ao projeto a partir do __commit D__

## merge VS. rebase
Não existe uma resposta óbvia sobre qual usar, mas, em geral, opta-se por fazer __merges__ em estruturas de projeto mais simples em que não há muitas ramificações e __branches__ paralelas muito longas.

Por outro lado, __rebase__ pode ser utilizado para simplificar a árvore do projeto para melhorar a legibilidade do histórico de __commits__

# Comandos Auxiliares:
## git status
Mostra o estado do projeto: qual é o branch, se existem arquivos não rastreados, quais arquivos estão na fila de __commit__, etc.
Pode ser usado especificando o caminho do diretório também:

> `git status path`

## git log
Mostra o histórico de __commits__, o hash de cada __commit__, autor, data e mensagem. O hash é o código único do __commit__, que é o que permite com que o sistema consiga retornar a uma versão anterior do projeto usando o próximo comando.

![gitk all Tree](./resources/img/git/git_log_example    .png)

## gitk --all
Abre uma janela mostrando toda a história do projeto. É parecido com o __git log__, mas permite escolher __commits__ específicos e também fornece uma visão da árvore do projeto não apenas como uma lista de __commits__.

![gitk all Tree](./resources/img/git/gitk_interface.png)

## git stash
Digamos que você precise alternar entre __branches__, mas não quer dar __commit__ no trabalho do __branch__ atual ainda. Neste caso, você cria um __stash__ das suas mudanças, ou seja, você cria uma pilha de trabalho inacabado para poder mudar de __branch__ sem perder suas alterações e sem ter que fazer um __commit__ com alterações incompletas.

# GitHub

__GitHub__ é uma plataforma de hospedagem de projetos que utiliza o __Git__. Pense nele como um _Dropbox_ ou _Google Drive_ especial para projetos de programação.

__site oficial:__ https://github.com

## Aplicativo Desktop:

O GitHub tem também um aplicativo que pode ser instalado no Desktop e pode ser baixado clicando <a href="https://central.github.com/deployments/desktop/desktop/latest/win32">aqui</a>. A instalação é bem simples, o executável dá conta de tudo, não precisa nem de next, next, next, ...

Assim que terminar de instalar, o aplicativo abre na página inicial pedindo que você entre na sua conta ou que crie uma se você ainda não tem.

![GitHub Desktop](./resources/img/desktop/github_desktop_landing.png)

Depois de entrar na sua conta, uma janela perguntando como você quer se identificar nos seus __commits__ vai aparecer.

![GitHub Identificação de usuário](./resources/img/desktop/github_commit_id.png)

Finalmente você será redirecionado para a página de criação e gerenciamento de [repositórios](#repositório-repo).

![GitHub Gerenciamento de Repos](./resources/img/desktop/github_desktop_repo_management.png)

## Repositório (Repo):

Um repositório do __GitHub__ funciona como diretório raiz do seu projeto, pense nele apenas como uma pasta na nuvem.

### Arquivos comuns de todo repo:

#### README:

Um arquivo com informações sobre o projeto. Deve conter o que seu projeto faz ou deveria fazer, instruções de instalação, enfim, precisa conter informações mínimas para quem quiser usar seu projeto ou dar manutenção.

No GitHub, esses arquivos possuem a extensão .md, que significa markdown e é um estilo de síntaxe usado para escrever textos e é o formato que é interpretado no repositório do seu projeto.

Um exemplo pode ser visto clicando [aqui](https://github.com/risniking/git_and_github_keynotes/blob/master/README.md). O arquivo direcionado pelo link é uma cópia deste documento só que escrito usando markdown, então possui exemplos de como colocar palavras em __destaque__, em _itálico_, inserção de imagens, links, etc.

Se quiser saber um pouco mais sobre esse estílo de síntaxe pode visitar https://guides.github.com/features/mastering-markdown/ ou procurar no Google por "markdown cheatsheet" ou semelhantes.

#### .gitignore:

Arquivo contendo uma lista dos arquivos que devem ser ignorados pelo seu projeto. Geralmente aqui estarão arquivos de build do código, arquivos de configuração, compressões (arquivos "zipados"), logs de erro e bases de dados ou quaisquer outros que não sejam essenciais para a execução dele.

Um exemplo comum de arquivos a serem ignorados é apresentado abaixo. O asterisco (*) representa qualquer continuação do caminho especificado, ou seja, se quisessemos ignorar todos os arquivos de texto com a extensão .txt presentes no diretório do projeto, bastaria incluir a linha *.txt ao arquivo .gitignore.

    # Compilados #  
    ##############  
    __pycache__/*  
    *.class  
    *.dll  
    *.exe  
    
    # Configuração #  
    ################  
    config.py  
    .env  
    
    # Compressos #  
    ##############  
    # Se o conteúdo desses arquivos for importante, é melhor  
    # extraí-los e realizar o commit deles.  
    # O GitHub possui os próprios métodos de compressão.  
    *.7z  
    *.dmg  
    *.gz  
    *.iso  
    *.jar  
    *.rar  
    *.tar  
    *.zip  
    
    # Logs e databases #  
    ####################  
    *.log  
    *.sql  
    *.sqlite  

## Como criar um repositório:

### Pelo site github.com:

Na página inicial do GitHub, no canto superior direito (ao lado da sua foto ou ícone da sua conta), tem um botão `+`. Clicando nele, escolha a opção __New repository__

![GitHub New repository](./resources/img/web/github_new_repo.png)

Na página de criação do repositório, insira um nome para ele (em geral é o nome do seu projeto) e na seleção de privacidade, altere o valor padrão para __Private__. Quando terminar clique no botão __Create repository__.

Se tudo der certo você deverá ver a página do seu novo repositório.

![GitHub Repo created](./resources/img/web/github_repo_created.png)

### Pelo aplicativo Desktop:

Para criar um repositório clique no botão __Create a New Repository on your hard drive...__ e forneça um nome e um local para criar o diretório na sua máquina.

![GitHub Novo Repo](./resources/img/desktop/github_desktop_new_repo.png)

Assim que terminar de criar, você verá a página abaixo e uma recomendação do GitHub para publicar seu projeto na nuvem

![GitHub Publicar Repo](./resources/img/desktop/github_desktop_publish_repo.png)

Clicando no botão __Publish repository__ uma página irá abrir, apenas clique novamente em __Publish repository__ e seu repositório será criado na nuvem e associado à essa pasta na sua máquina.

## Criando um branch:

Por padrão, quando você cria um repositório ele já vem com o __`master` branch__, que, em geral, é utilizado como o __branch__ de produção.

### Pelo site github.com:

Na página do repositório do seu projeto, clique no botão da lista de __branches__ escrito `Branch: __master__`.

![Github Novo Branch](./resources/img/web/github_web_new_branch.png)

Isso fará com que a lista de __branches__ abra. No caso, como o repositório é novo, só existe o __`master`__. Para criar um novo __branch__, basta inserir um nome que ainda não exista (em geral os nomes serão sempre os mesmos, como `staging`, `features`, `issue#247`, etc.).

![Github Lista de Branches](./resources/img/web/github_web_branch_list.png)

Termine clicando em `Create branch: nome_do_novo_branch`. Automaticamente o repositório será trocado para a visão deste novo __branch__. Agora, quando quiser trocar entre __branches__, basta clicar na lista e selecionar outro.

### Pelo aplicativo Desktop:

Da mesma forma que fizemos pelo site, clique no botão da lista de __branches__ escrito `Current branch __master__` na parte superior do aplicativo.

![Github Lista de Branches](./resources/img/desktop/github_desktop_branch_list.png)

Assim, a lista de __branches__ do projeto irá aparecer. Para criar um novo __branch__, clique no botão `New branch`.

![Github Lista de Branches](./resources/img/desktop/github_desktop_new_branch.png)

## Fazendo um commit:

### Pelo site github.com:

Digamos que você fez uma alteração em um ou mais arquivos do seu projeto e quer fazer um __commit__ dessas mudanças. Para isso, basta clicar em `Upload files`

![Github Upload files](./resources/img/web/github_web_upload_file.png)

Na página seguinte, arraste os arquivos que quer dar __commit__ ou clique em `choose your files` para selecioná-los.

![Github Upload files](./resources/img/web/github_web_commit.png)

Acrescente uma mensagem ao seu __commit__ e, caso considere necessário, adicione um parágrafo descrevendo as modificações feitas. Finalize clicando em `Commit changes`.

### Pelo aplicativo Desktop:

O aplicativo mostra todas as mudanças feitas em todos os arquivos do seu projeto, sem a necessidade de adicionar os arquivos manualmente para __commit__. Mesmo assim, é possível selecionar quais arquivos farão parte do seu __commit__ (pode ser que você tenha feita diversas mudanças, mas cada uma merece um __commit__ diferente, com uma mensagem e descrição diferentes).

![Github Upload files](./resources/img/desktop/github_desktop_commit.png)

Note que o __branch__ selecionado é o `master`, então o botão de __commit__ indica a mensagem `Commit to master`. Atente-se a isso quando fizer modificações e __commits__, pois, em geral, novas features são desenvolvidas e adicionadas num __branch__ separado (_features_, _testes_, _staging_, etc.). Depois de validadas e seu projeto se mostrar estável com as mudanças, elas são adicionadas no `master`, que é o seu __branch__ de produção.

Depois disso, o aplicativo irá sugerir que você dê um __push__ nos seus __commits__ para a `origin`, que é o nome dado ao endereço do seu repositório no GitHub.

![Github Push Origin](./resources/img/desktop/github_desktop_push_origin.png)

## Pull Request (PR):

### O que é?

Um __Pull Request__, ou só __PR__, é uma requisição para incorporar mudanças feitas em um branch para outro.

Em geral, um __PR__ é aberto para comunicar ao(s) administrador(es) do projeto sobre uma correção que você fez ou alguma feature que você implementou e quer contribuir com o 
projeto, ou seja, quer que suas modificações sejam __mergeadas__ ao branch __master__ (ou algum outro branch, depende de como o projeto é estruturado).

### Boas práticas:

Grandes projetos open-source possuem instruções de como contribuir e como escrever os __PR__ de contribuição. Na ausência dessas instruções, pode ser usado como boas práticas que 
você:

- __Coesão__: Idealmente, seu __PR__ resolve apenas um problema ou implementa uma feature específica. Lembre-se de que esse código será revisado por _alguém_, e se essa pessoa tiver 
que se preocupar em avaliar a correção ou implementação de mais de um elemento do projeto, isso pode criar confusão, refatoração e aumentar o tempo de revisão até que finalmente o 
__PR__ seja resolvido.

- __Explicação__: Dependendo do tamanho da mudança, pode ser que seja necessário apenas um título bem descritivo, mas, se a alteração for grande, é importante saber descrever sobre o 
que está sendo implementado ou corrigido, as motivações e porquês, enfim, fornecer informações para que o revisor tenha o máximo de autonomia para ler o seu código e 
saber interpretar e questionar suas implementações.

### Criando um PR no site github.com:

Depois de feito o __commit__ no branch de desenvolvimento (alguns exemplos de nomes de branch: _dev_, _staging_, _issue#27_, _seuNome:feature_...) que quer implementar no projeto, vá até o repositório do projeto e selecione o __branch__ ao qual você fez o __commit__.

![Github PR Notice](./resources/img/web/github_web_pr_notice.png)

Note que o GitHub já sugere que você abra um PR para o __commit__. Clique em __Compare & pull request__

![Github Open PR](./resources/img/web/github_web_pr_description.png)

Escreva um título que identifique sua requisição e, se necessário, detalhe as modificações no corpo do __PR__. Finalmente, quando quiser publicar, aperte __Create pull request__ e 
você será redirecionado à página de resumo do seu __PR__ onde as pessoas poderão comentar sobre ele, questionar partes específicas do seu código, etc.

![Github PR Summary](./resources/img/web/github_web_pr_summary.png)

### Criando um PR no aplicativo Desktop:

Na página do repositório, selecione o __branch__ que possui os __commits__ que você quer incorporar no projeto.

![Github Desktop Select Branch](./resources/img/desktop/github_desktop_select_branch.png)

Assim que fizer isso, um aviso irá aparecer sugerindo que você crie um __PR__. Clique em __Create Pull Request__ e você será redirecionado à página web no github.com de criação do 
seu __PR__.

![Github Desktop PR Notice](./resources/img/desktop/github_desktop_pr_notice.png)

O restante é igual ao que foi descrito em [__Criando um PR no site__](#criando-um-pr-no-site-githubcom).
