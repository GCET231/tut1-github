# Usando Git para Gerenciar Código RTL

>_tutorial traduzido de Brian Zimmer e Ben Keller da Berkeley University, Califórnia._

## Como utilizar este tutorial

Nosso curso utilizará o Git para todos as atividades práticas de laboratório e desenvolvimento de projetos. Isso permitirá que a equipe visualize e avalie mais facilmente seus arquivos. Além disso possibilitará que você utilize um controle de versão para um backup mais eficiente do desenvolvimento, facilitando ainda a colaboração em projetos em grupo.

Já existe muita informação disponível sobre Git, e as melhores fontes são listadas abaixo. Para as nossas práticas, é necessário um conhecimento básico de Git. Este tutorial provê uma breve introdução e apresenta alguns comandos mais comuns, mas é altamente recomendado que você pesquise nas referências abaixo (que varia em tamanho de algumas páginas introdutórias a livros inteiros).

## Recursos

* [Git in 1 Hour](http://www.youtube.com/watch?v=OFkgSjRnay4): Um ótimo vídeo introdutório ao Git.
* [Página Oficial](http://git-scm.com/documentation): tem links para todos os melhores lugares para aprender sobre Git, incluindo livros gratuitos.
* [FAQ](https://git.wiki.kernel.org/index.php/GitFaq)

## Por que usar Controle de Versão
Sistemas de controle de versão realizam uma "captura" estática dos seus arquivos em um tempo específico. Isso é uma excelente forma de manter um backup de seus arquivos e facilmente visualizar como as coisas mudaram ao longo do tempo. Além disso, controle de versão permite que múltiplas pessoas trabalhem no mesmo código. A maioria dos softwares com centenas de desenvolvedores usam sistemas de controle de versão para reunir as contribuições de todos. Mesmo que haja uma curva de aprendizado, sistemas de controle de versão economizam tempo no longo prazo. Fazer cópias de arquivos para backup ou enviá-los por e-mail pode funcionar, mas o controle de versão promove formas mais simples e mais eficientes de realizar tarefas comumente realizadas.

## Por que Git?

O Git é diferente dos outros sistemas de controle de versão no fato de existir o conceitos de repositórios global e local. Em um sistema tradicional, como o Subversion, cada vez que você faz um "commit" (lembre) do estado do seu código, ele é enviado para o repositório compartilhado. O problema disso é que outras pessoas podem ver todos os seus commits. Muitas vezes o que você está fazendo irá quebrar todo o sistema. Se você realiza commits regularmente, você pode quebrar o código dos outros. Por outro lado, no Git você possui um repositório local separado. Você pode realizar quantos commits desejar, e compartilhar apenas suas mudanças com outros quando ela estiver mais madura. Isso também resulta em operações mais rápidas, uma vez que tudo está geralmente acontecendo localmente.

## Exemplo de fluxo de trabalho
Nós criamos um repositório de exemplo para você experimentar. Descompacte o [arquivo]() no seu diretório raiz e em seguida execute os comandos a seguir:

`% git clone ~gcet231/git/git-tut.git`

`% cd git-tut`

Agora você criou uma cópia local do seu repositório remoto, o qual você poderá visualizar e editar. Comece criando um arquivo de exemplo. Adicione qualquer texto que você desejar nele, e sinta-se livre para substituir o nano pelo editor de usa escolha.

`% nano TODO`
`% type type type ...`

Agora vamos ver o que o Git vê.

`% git status`

O Git vê esse arquivo como um arquivo não rastreado (_untracked file_). Isso quer dizer que o Git está ignorando o arquivo por enquanto e não saberá sobre nenhuma mudança que aconteça nele.

`% git add TODO`

Agora verifique o que o Git vê executando novamente `git status`. O Git agora diz que está rastreando esse arquivo. Mas você ainda pode fazer mudanças nesse arquivo, e o Git não se lembrará o que você fez. Neste momento, o arquivo está apenas "staged". Para o Git se lembrar de como o arquivo era em um certo tempo, você precisa realizar um commit (fazer uma captura).

`% git commit -m "log message"`

Se você não incluir a opção `-m "log message"`, um editor de texto se abrirá. Entre com a mensagem de registro, salve, e saia, e então o commit acontecera. Você deve introduzir uma mensagem de registro para cada commit. Execute `git status` novamente para ver que o Git acredita que tudo está atualizado como esperado.

Agora vamos ver como nós visualizados o histórico. Abra seu arquivo, e adicione outra linha.

`% nano TODO`

`% type type type ...`

Para visualizar o que mudou, execute:

`% git diff TODO`

Agora realize o commit dessas mudanças também:

`% git add .`
`% git commit -m "log message"`

Onde `git add .` irá adicionar todos os arquivos no diretório. Você pode ainda usar a opção -a para realizar o commit de todas as mudanças em arquivos rastreados (isso não irá adicionar novos arquivos):

`% git commit -am "log message"`

Agora adicione uma nova linha, novamente:

`% nano TODO`

Imagine que você não gostou de suas mudanças e deseja revertê-las:

`% git checkout -- TODO`

O `--` existe porque o comando `git checkout branchname` abrirá um branch (um tópico mais avançado) e o `--` faz com que o Git saiba que você que realizar o checkout de um arquivo.

Outro recurso bastante interessante é o fato de que você pode visualizar versões antigas de um arquivo. Imagine que uma fala foi introduzida, e você deseja visualizar uma versão anterior de um arquivo.

`% git log`

Para visualizar o registro graficamente, você pode instalar um pacote chamado gitk.

Perceba que próximo às palavras "commit" existe uma string de palavras e números chamados de SHA. Essa chave corresponde a um identificador única para um dado commit. Você pode encontrar ela tanto no `gitk` quanto no `git log`. Para visualizar a versão de TODO para um dado commit, cole o número abaixo (o seu poderá ser um pouco diferente).

`% git show 90940d1cdbb016952db2ba368fdc4906e010a9ff:TODO`

Note que depois do `:` está o caminha para o arquivo. Em geral, você não precisa da SHA completa. Além disso, se for um arquivo longo, você pode preferir abri-lo em seu editor favorito.

`% git show 90940d:TODO | nano -`

Mas e se você possuir dúzias de arquivos, e deseja visualizar o estados do repositório antes de um dado commit? Usando a SHA encontrada no `git log` ou `gitk`, basta fazer um "checkout" desta revisão.

`% git checkout 33c9894e13f8c3d9d4307c4b77e1a92e286d70ba`

Uma vez que você tenha finalizado e deseja retornar para o estado anterior:

`% git checkout master`

Certifique-se de realizar o commit antes de voltar nos históricos, do contrário você poderá perder o arquivos.

Por último, se você está trabalhando com outras pessoas, você pode enviar suas mudanças (_push_) para um repositório remoto. Sempre que você quiser fazer isso, você precisa se certificar de suas coisas. Primeiro, garanta que você tenha feito o commit de todas as suas modificações locais e o seu `git status` está limpo, do contrário você pode gerar problemas. Por fim, garanta que sua cópia local está atualizada, baixando as mudanças do repositório remoto (_pull_).

`% git pull origin master`

O `origin` refere-se ao repositório remoto padrão (você pode possuir vários repositórios remotos) e `master` se refere ao fato de que você deseja enviar seu código para o fluxo principal (e não para um branch). Geralmente, isso pode ser ignorado, e o `git pull` funcionará normalmente.

Leia o status do pull. Se a versão remota mudou desde a última vez, ele tentará juntar as mudanças automaticamente! Geralmente, isso funciona magicamente. Por exemplo, se um novo arquivo foi adicionado, ele irá apenas baixar o arquivo. Se uma linha foi acrescentada para um arquivo que você mudou também e as linhas estão muito distantes, ambas as mudanças serão fundidas. Mas se o mesmo arquivo foi muito modificado seja remotamente ou localmente e o Git não conseguir descobrir como juntá-los, você verá um erro:

```
CONFLICT (content): Merge conflict in README
Automatic merge failed; fix conflicts and then commit the result.
```

Para corrigir esse conflito, edite os arquivos que ele listou (neste caso, README). As partes do código onde o problema ocorreu estão marcadas dentro do arquivo. Por exemplo:

```
<<<<<<<< HEAD:README
Example empty git repository
========
Example of an empty Git repository f12702bfd22e037cf55d0e7e2da4e9f0f1d58f62:README
```

A versão no seu arquivo local está no topo e a versão que está no repositório remoto está em baixo. Corrija o código escolhendo uma das duas e remova os marcadores.

Você pode usar uma ferramenta para fazer isso digitando `git mergetool`. Tente digitar vimdiff como a ferramenta de merge, e você visualizará 3 painéis. O painel da esquerda contém o seu arquivo, o do meio o arquivo a ser corrigido, e o da direita o arquivo remoto. Modifique o painel do meio até que o conflito deixe de existir.

Uma vez que a fusão dos arquivos foi corrigida, realize o commit das suas mudanças. Se você usou o mergetool, ele irá automaticamente ser registrado quando você sair, e um arquivo filename.orig irá manter um backup do arquivo problemático.

`% git commit -m "fixed merges"`

Agora que tudo está bem, você poderá enviar suas mudanças para o repositório remoto.

`git push origin master`

Note que nesse tutorial você verá um erro quando tentar realizar um push, porque você não tem permissão para escrever no repositório do tutorial.

### Configurando o Sublime Text como Git Mergetool

Se você prefere analisar os conflitos em um editor com interface gráfica, você pode fazê-lo com poucas linhas de código. O Sublime Text é um editor de código fonte poderoso e altamente personalizável, com suporte a diversas linguagens de programação. Ele também se caracteriza por ser leve e ideal para tarefas rápidas.

Para configurar o Sublime Text como editor padrão do Git Mergetool execute os comandos a seguir:

````
% git config --global mergetool.sublime.cmd "subl -w \$MERGED"
% git config --global mergetool.sublime.trustExitCode false 
% git config --global merge.tool sublime
% git mergetool -y
````

## Ignorando arquivos

Arquivos que são gerados dinamicamente (e.g., código compilado ou arquivos de layout da ferramenta de síntese) não devem ser armazenados em repositórios. Mantê-los em um repositório é redundante (uma vez que eles podem ser gerados a partir de outros arquivos no repositório) e pode causar uma bagunça.

"make clean" é um comando muito usado para remover esses arquivos gerados dinamicamente. No Git, nós criamos um arquivo que irá ignorar tais arquivos.

Primeiro crie um arquivo de registro executando o comando `touch run.log`. Agora o `git status` mostra um arquivo não rastreado que nós não queremos que o Git saiba que existe.

Na raiz do diretório, execute:

`% nano .gitignore`

Dentro deste arquivo, nós listamos os diretórios ou arquivos que não devem ser visualizados individualmente, em cada linha. 

```
build*
*.log
tmp/
```

O comando `git status` agora não deve mais exibir o seu arquivo de registro. Note que o arquivo `.gitignore` deve ser enviado para o repositório, mas ele irá funcionar mesmo que você ainda não tenha realizado o commit.

## Tópicos Avançados

Existem muitos outros recursos no Git, e apenas alguns poucos foram introduzidos aqui. Alguns outros recursos que valem a pena serem aprendidos (especialmente em um repositório com múltiplas pessoas):

* `git blame`: Irá exibir quem modificou cada linha em um arquivo e quando.
* `git bisect`: Pode voltar através de revisões antigas usando uma busca binária e determinar quando uma falha for encontrada.
* Branching: Possibilita a mudança rápida entre diferentes versões do mesmo repositório. Ótimo para realizar experimentações.
* Plugins para editores: Editores como VIM e Emacs possuem plugins excelentes. Editores modernos, como o Visual Code Studio possuem suporte nativo ao Git. 

## Folha de dicas

Comando | Descrição
------------ | -------------
`git clone (url)` | Faz uma cópia do repositório a partir de um servidor remoto e cria uma versão local
`git status` | Visualiza quais arquivos foram modificados desde o último commit
`git diff` | Visualiza o que foi modificado
`git add (filename)` | Adiciona um arquivo para o próximo commit
`git pull` | Atualiza o repositório local a partir do repositório remoto
`git push` | Envia os últimos commits para o repositório remoto
`git checkout -- (filename)` | Reverte um arquivo para a úlgima versão registrada
`git clean -dfx (dirname)` | Reverte um diretório inteiro para seu estado no repositório remoto
`gitk` | Visualiza graficamente o histórico de commits