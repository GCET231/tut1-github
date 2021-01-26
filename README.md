# Comandos Básicos do Git

O Git é um sistema de controle de versão de código robusto e completo. Sistemas de controle de verão ajudam na busca por modificações nos códigos-fonte ao longo do tempo e facilitam o compartilhamento de mudanças provenientes dos colaboradores. Para projetos de qualquer nível de complexidade algum tipo de controle de versão é uma necessidade. Existem diversos sistemas de controle de versão por aí, cada um com suas vantagens e desvantagens. Neste curso, nós usaremos o Git, um dos sistemas de controle de versão mais populares. É importante que você faça um esforço para entender como o Git funciona, pois assim você perceberá como é fácil usá-lo no dia a dia. O link abaixo apresenta uma boa visão geral:

[https://rogerdudler.github.io/git-guide/index.pt_BR.html](https://rogerdudler.github.io/git-guide/index.pt_BR.html)

Uma vez que você tenha entendido o material acima, complete o tutorial a seguir:

[http://try.github.com](http://try.github.com)

O Git é uma ferramenta muito poderosa, mas que pode ser um pouco complicada no começo. Se você não sabe o que está fazendo, você pode provocar muitas dores de cabeça para você mesmo e para aqueles a sua volta, então seja cuidadoso. Se você estiver em dúvida sobre como fazer algo com Git, pergunte para o seu professor ou a um colega mais experiente.

Para os propósitos das nossas aulas, você provavelmente precisará dominar os comandos a seguir:

* `git status`
* `git add`
* `git commit`
* `git pull`
* `git push`
* `git clone`

Entretanto, se você deseja realmente entender como usar alguns recursos mais poderosos (diff, blame, branch, log, mergetool, rebase, e muitos outros), eles podem realmente aumentar muito a sua sua produtividade.

O Git possui um grande conjunto de funcionalidades muito bem documentada na Internet. Se há alguma coisa que você acredita que o Git pode fazer, existe uma grande chance de um comando para isso já existir. Nós encorajamos você a explorar e discutir com seus colegas e professores.

_Opcional:_ Se você deseja explorar mais, confira o tutorial um pouco mais avançado.

## Instalando o Git

O Git é uma ferramenta nativa (já vem instalada junto com o sistema) em sistemas Linux e MacOS. Instruções sobre como instalar o Git podem ser encontradas aqui: [http://happygitwithr.com/install-git.html](http://happygitwithr.com/install-git.html). Usuários Windows devem seguir a Opção 1 na seção 6.2. 

Após instalar o Git em seu sistema, abra o terminal e execute o comando:

`git --version`

Instruções mais detalhadas sobre a instalação no Windows podem ser encontradas neste vídeo: [https://youtu.be/F_fPEMnr1OQ](https://youtu.be/F_fPEMnr1OQ)

## Configurando seu acesso ao Github

Nós usaremos o Github como nosso servidor Git remoto ao longo do semestre. O Github é um serviço de hospedagem Git que tem sido a casa de vários projetos privados e públicos (open-source).

### Chaves SSH

O Github autentica você para acesso aos seus repositórios utilizando chaves ssh. Siga o tutorial adiante para configurar suas chaves SSH (isso deve ser feito nos computadores do laboratório quando estiver autenticado com sua conta, assim como no seu próprio computador).

Primeiro crie uma nova chave SSH (utilize o e-mail institucional caso esteja em um computador do laboratório, caso contrário, utilize outro e-mail cadastrado no GitHub):

`ssh-keygen -t rsa -b 4096 -C "seu_email@ufrb.edu.br"`

Pressione enter e use as configurações padrão.

Então, a partir do terminal execute:

`cat ~/.ssh/id_rsa.pub`

Copie toda a chave pública que foi exibida. Siga até aqui: [https://github.com/settings/keys](https://github.com/settings/keys), clique em "New SSH Key", cole sua chave pública na caixa de texto, e clique em "Add SSH key"

Finalmente, teste sua conexão SSH seguindo as instruções em: [https://help.github.com/articles/testing-your-ssh-connection/](https://help.github.com/articles/testing-your-ssh-connection/)

Se enfrentar algum problema durante o processo, pergunte ao seu professor.

## Guia Prático do GitHub

### Criando um repositório no GitHub

A seguir nós criamos um repositório e copiamos o link para que possamos baixá-lo no nosso próprio computador.

![Alt Text](https://github.com/GCET231/tutorial1-github/blob/main/img/create_repo.gif)

### Clonando o repositório para seu computador

Para clonar um repositório, use o comando a seguir:

`% git clone https://github.com/joaocarlos/repository-name.git`

![Alt Text](https://github.com/GCET231/tutorial1-github/blob/main/img/create_repo.gif)