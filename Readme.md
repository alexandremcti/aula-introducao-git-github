# Criando nosso projeto com Git

## Criando um novo repositório local

Vamos criar uma loja de games iniciando com o arquivo index.html

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8"/>
        <meta name="description" content="Quem é Miro Games">
        <meta name="keywords" content="loja de games">
        <title>Quem é Miro Games</title>
    </head>
    <body>
        <h1>Quem é Miro Games</h1>
        <ul>
            <li>Playstation 4</li>
            <li>XBox</li>
            <li>Nitendo Switch</li>
        </ul>
    </body>
</html>
```

Agora vamos entrar no Git Bash e executar o comando: 

```
$ git init
```

E teremos a saída:
` Initialized empty Git repository in /home/path/to/directory/.git/ `

Podemos ver o que foi criado no diretório com o comando ls -lha e veremos que foi criado um subdiretório  chamado .git na nossa pasta. Esse subdiretório contém todo o histórico de alterações dos arquivos.

## Rastreando arquivos

Vamos verificar o estado atual do nosso repositório executando o comando:

```
$ git status
```

Vamos analisar a resposta:

```
# On branch master
#
# Initial commit
#
# Untracked files:
# (use "git add <file>..." to include in what will be
committed)
#
# index.html
nothing added to commit but untracked files present (use
"git add" to track)
```

O arquivo index.html ainda não foi rastreado (untracked) para que possa ser versionado.
Queremos que ele seja rastreado, então  utilizaremos o comando:

```
$ git add index.html
```

Agora o Git sabe que esse arquivo é importante e todas as mudanças nele devem ser rastreadas.
Utilizando o comando `git status` teremos a saída:

```
# On branch master
#
# Initial commit
#
# Changes to be committed:
# (use "git rm --cached <file>..." to unstage)
#
# new file: index.html
#
```

E agora podemos ver que o arquivo index.html está entre as mudanças que serão commitadas, em outras palavras, versionadas.

## Rastreando vários arquivos

Vamos criar agora um arquivo `estilos.css` no diretório com o seguinte conteúdo:

```
h1 {
    font-family: sans-serif;
}
li {
    font-family: monospace;
}
```

Também criaremos um arquivo `logo.png` dentro do subdiretório imagens

Agora vamos executar git status novamente:

```
# On branch master
#
# Initial commit
#
# Changes to be committed:
# (use "git rm --cached <file>..." to unstage)
#
# new file: index.html
#
# Untracked files:
# (use "git add <file>..." to include in what will be
committed)
#
# estilos.css
# imagens/
```

Imagens e estilos estão entre os arquivos não rastreados. Logo podemos rastrar ambos utilizando ` git add .` e após um `git status` podemos ver que todos os arquivos estão na zona de rastreamento.

## Sobre a área de stage

Quando informamos que queremos rastrear um arquivo executando o `git add`, estamos incluíndo esse arquivo na área de stage. Todas as mudanças nesses arquivos são verificadas.

Vamos modificar o arquivo index.html

```
<!-- início do arquivo ... -->
    <head>
        <!-- tags meta ... -->
        <link rel="stylesheet" href="estilos.css">
    </head>
<!-- restante do arquivo ... -->
```

E agora vamos executar o `git status`:

```
# On branch master
#
# Initial commit
#
# Changes to be committed:
# (use "git rm --cached <file>..." to unstage)
#
# new file: estilos.css
# new file: imagens/logo.png
# new file: index.html
#
# Changes not staged for commit:
# (use "git add <file>..." to update what will be committed)
# (use "git checkout -- <file>..." to discard changes in
working directory)
#
# modified: index.html
#
```

Podemos ver que o arquivo index.html é mostrado como modified

Vamos agora executar o `git add .` para comitar as mudanças e depois vamos utilizar `git commit -m` 

# ignorando arquivos

Vamos supor agora que temos um arquivo todo.txt em que iremos registrar todas as atividades que precisamos realizar durante o dia e não queremos que este arquivo seja rastreado. Vamos criar também um diretório chamado tmp que também não queremos rastrear as mudanças

Podemos criar um arquivo no diretório raiz chamado `.gitignore` e adicionar o que não queremos que seja rastreado e ele irá ignorar toda mudança que acontecer nesse arquivo.

```
todo.txt
tmp/
```
Agora vamos rastrear o arquivo gitignore com o `git add .`
Se nós tivéssemos vários arquivos com final .log poderíamos incluir no gitignore o `*.log`

## Gravando Arquivos no Repositório

Agora queremos gravar definitivamente esses arquivos e alterações no nosso repositório. Para fazer isso vamos utilizar o comando `git commit`:

```
$ git commit -m "Commit inicial"
```

Nós informamos uma flag -m para passar uma descrição a respeito do que estamos gravando. Depois disso temos a seguinte saída:

```
[master (root-commit) 7777444] Commit inicial
4 files changed, 26 insertions(+)
create mode 100111 .gitignore
create mode 100111 estilos.css
create mode 100111 imagens/logo.png
create mode 100111 index.html
```

Na primeira linha nós temos um código antes da mensagem. Esse código é o identificador do commit.

Agora vamos observar o estado do repositório com o comando `git status`. Não há mais nada para ser commitado.

## Verificando o histórico do repositório

Para verificarmos todas as mudanças que foram realizadas utilizamos o comando:

```
$ git log
```

E para sair do git log basta apertar a tecla q.

## Verificando mudanças nos arquivos rastreados

Agora nós vamos realizar uma mudança no arquivo index.html. Vamos supor que o dono da loja informou que não possui mais playstation 4 e agora só vendem o 5. Vamos realizar a mudança

```
<li>Playstation 5</li>
```

Vamos mais uma vez executar `git status` para ver o status do arquivo.

Agora vamos executar o comando `git diff`

```
$ git diff
```

```
--- a/index.html
+++ b/index.html
@@ -11,7 +11,7 @@
 <body>
     <h1>Quem é Miro Games</h1>
     <ul>
-        <li>Playstation 4</li>
+        <li>Playstation 5</li>
         <li>XBox</li>
         <li>Nitendo Switch</li>
     </ul>
```

Assim podemos ver mudanças que foram feitas em arquivos já rastreados e que ainda não foram rastreadas. Se tivermos mudanças em outros arquivos, mas quisermos ver uma mudança em um único arquivo basta executar o comando `git diff` [nome do arquivo] e se quisermos verificar as mudanças em staged podemos executar `git diff --staged`

## Removendo arquivos do repositório

Vamos supor que criamos um outro arquivo html para os produtos no nosso projeto. Vamos rastrear o arquivo.

```
$ git add .
```

Agora vamos commita-lo.

```
$ git commit -m "incluido pagina de produtos"
```

Agora precisamos deleta-lo, mas não basta apenas deletar o arquivo. Precisamos deletar o arquivo e adicionar a deleção na área de stage, para enfim commitar no repositório.
Podemos fazer isso com o comando:

```
$ git rm produtos.html
```

Assim podemos remover e adicionar ao stage ao mesmo tempo. Agora vamos commita-lo para finalizar o versionamento no repositório.

## Removendo mudanças não rastreadas

Agora vamos supor que o dono da empresa ficou louco depois de tomar umas e ligou pedindo uma mudança de ultima hora. Nós percebemos que o patrão não conseguia fazer um 4 e resolvemos não salvar o trabalho definitivamente.

```
<body>
    <h1>Quem é Miro Games</h1>
    <h2>Tudo por 1,99</h2>
    <ul>
        <li>Playstation 5</li>
        <li>XBox</li>
        <li>Nitendo Switch</li>
    </ul>
</body>
```

No dia seguinte ele ligou de ressaca e falou pediu para desfazer a mudança. Então nós vamos lá executar o seguinte comando:

```
git checkout index.html
```

Pronto. Toda a mudança realizada foi desfeita.
E se apagassemos o arquivo index.html sem querer? Basta executar o comando abaixo:

```
$ git checkout -- index.html
```

## Removendo mudanças rastreadas

O próximo passo é remover um arquivo já rastreado. Imagine que você fez a mudança e a rastreou. Vamos modificar o arquivo index.html

```
<body>
    <h1>Quem é Miro Games</h1>
    <h2>Tudo por 1,99</h2>
    <ul>
        <li>Playstation 5</li>
        <li>XBox</li>
        <li>Nitendo Switch</li>
    </ul>
</body>
```

Basta executar o comando git reset -- index.html e removeremos a mudança que foi efetuada, preservando o arquivo modificado. Podemos ver através do git status que o arquivo voltou para a área não rastreada e permanece com a mudança realizada.

Agora vamos rastrear mais uma vez a mudança.  Depois de rastreada vamos agora reverter com o seguinte comando:

`git log -n 1 --onenline` para ver o codigo do ultimo commit.

```
$ git revert --no-edit 9f54861

[master 46c9abc] Revert "adicionando novo produto à loja"
 Date: Tue Nov 1 08:19:42 2022 -0300
 2 files changed, 1 insertion(+), 37 deletions(-)
```

Se verificarmos o arquivo index.html poderemos observar que a mudança foi desfeita. Também podemos executar o comando `git log` para ver o histórico dos nossos commits.

```
$ git log
commit 46c9abce03f29f78b7b24136e2f27595f37559e9 (HEAD -> master)
Author: Alexandre Magno AM. de Carvalho <alexandre_mcti@hotmail.com>
Date:   Tue Nov 1 08:19:42 2022 -0300

    Revert "adicionando novo produto à loja"

    This reverts commit 9f54861e47c86b72c63215395a568342e2b150a6.
```

Podemos observar que foi criado um novo commit com a mensagem Revert + a descrição do ultimo commit que realizamos. Isso é importante porque queremos sempre identificar o que ocorreu durante a história do projeto, não importa se houve um código que subiu errado. Um exemplo da vida real pode ser uma rotina de código que foi revertida para atender uma necessidade, mas que agora faz sentido retornar com ela. Saberíamos exatamente o que foi modificado e revertido.

Vamos analisar o gráfico no ppt para entender-mos o fluxo atual.

## Publicando no GitHub

Primeiramente vamos entrar no GitHub e criar uma nova conta

https://github.com/

Depois que a conta for criada nós entraremos no GitHub e iremos criar um repositório. Definiremos que ele será público.

Depois, dentro do nosso repositório, vamos aponta-lo para o repositório do GitHub.

```
$ git remote add origin https://github.com/fulanodasilva/introducao-git-github.git
```

Agora vamos enviar o nosso projeto para lá. Vamos executar o comando:

```
$ git push origin main
```

Pronto. Agora nosso projeto está no GitHub e podemos ver as mudanças realizadas.

## Obtendo o projeto do GitHub

Agora vamos criar um outro diretório na nossa máquina e clonar o projeto do github. Primeiramente nós copiaremos a url do projeto. Depois nós utilizaremos o comando:

```
$ git clone 
```

Muito provavelmente nós teremos que realizar um procedimento de passar a uma chave pública de segurança ao GitHub para podermos acessar os repositórios.

```
$ ssh-keygen
```

Vamos apertar apenas enter e será gerada uma chave na pasta .ssh. Depois nós vamos usar o comando `cat id_rsa.pub`. Vamos copiar o que foi exibido e entrar em settings >> SSH e GPG e criar uma nova chava passando o que acabamos de cópiar. Pronto, agora está tudo pronto para avançarmos.

Vamos entrar na pasta que acabamos de clonar e abrir o git bash. Utilizando `ls -a` podemos ver o conteúdo da pasta
Agora estamos na branch principal e podemos ver o que acabamos de subir. Se uxecutarmos `git log` 

## Trabalhando com branchs

Agora vamos simular como seria trabalhar em um time de desenvolvimento. Vamos criar uma branch para criar uma nova funcionalidade.

Uma branch é uma ramificação. Quando criamos uma nova branch nós queremos separar o que será criado aqui da branch da raiz.

Então vamos primeiramente fazer criar uma nova branch com o seguinte comando:

```
$ git branch development
```
e depois vamos entrar nessa nova branch com o comando:

```
$ git checkout development
```

Agora vamos realizar uma mudança em index.html

```
<body>
    <h1>Quem é Miro Games</h1>
    <ul>
        <li>Playstation 5</li>
        <li>XBox</li>
        <li>Nitendo Switch</li>
    </ul>
    <footer>
        <p>Miro S.A</p>
    </footer>
</body>
```

Agora vamos commitar nossa mudança

```
$ git add .
$ git commit -m "adicionando o footer"
```

Agora vamos subir a nossa mudança no github

```
$ git push origin development
```
