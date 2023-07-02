---
title: Como fazer login no AUR do Arch Linux
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, fazer, login, aur, arch, linux, autenticar, gerenciar]
subtitle: Saiba como fazer login no git do AUR para gerenciar seus pacotes
category: [Dicas e tutoriais, Linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*zIrqE774fW_PBDsn.png
share-img: https://cdn-images-1.medium.com/max/800/0*zIrqE774fW_PBDsn.png
layout: post
---

![](https://cdn-images-1.medium.com/max/800/0*zIrqE774fW_PBDsn.png)<br/>
Se você estava no AUR e encontrou um pacote abandonado (sem mantenedor) e quer adotar o pacote e também fazer atualizações no PKGBUILD e dos arquivos, neste tutorial vou ensinar a como se autenticar no AUR e enviar o pacote de volta para o AUR.

**Conteúdo**

- [Como se autenticar no SSH do AUR](#Como-se-autenticar-no-SSH-do-AUR)
- [Para baixar o pacote git do AUR e fazer modificações](#Para-baixar-o-pacote-git-do-AUR-e-fazer-modificações)
- [Para enviar as mudanças de volta para o AUR](#Para-enviar-as-mudanças-de-volta-para-o-AUR)

### Como se autenticar no SSH do AUR

1- Crie o diretório .ssh:

	$ mkdir ~/.ssh/

2- Crie o arquivo “config” dentro de .ssh

	$ nano ~/.ssh/config

Isso vai abrir o editor de texto ‘nano’, dentro desse arquivo coloque:

> _Host aur.archlinux.org
> IdentityFile ~/.ssh/aur
> User aur_

3- Agora vamos criar uma chave de autenticação, use o comando:

	$ ssh-keygen -f ~/.ssh/aur

(caso encontre erro, instale o pacote usando o comando `pacman -S openssh`)

Depois o terminal vai mostrar essa mensagem:

> _Enter passphrase for key ‘/home/user/.ssh/aur_

Aqui você deve criar uma **frase secreta**, ela será requisitada no momento de salvar as mudanças do pacote de volta para o AUR.

Digite a **frase secreta** e repita mais uma vez, após isso será mostrado essa mensagem:

> _Your public key has been saved in /home/user/.ssh/_**_aur.pub_**

4- Agora vamos copiar os dados desse arquivo **aur.pub** e para a conta do AUR, use o comando:

	$ cat ~/.ssh/aur.pub

5- Copie o código, vá na pagina do AUR, clique em My Account (canto superior esquerdo), procure o campo “**Chave pública SSH:**” e cole o código lá.

Insira a senha da conta AUR no final da pagina e clique em **Save**.

### Para baixar o pacote git do AUR e fazer modificações:

1- Vai na pagina do AUR, do pacote que você quer fazer mudanças e pegue o endereço **ssh .git** do pacote.

_Exemplo:_ **_ssh://_**_aur@aur.archlinux.org/hamsket-nightly-bin_**_.git_**

1.  _Caso apareça o erro:_

> _aur@aur.archlinux.org: Permission denied (publickey).
> fatal: Could not read from remote repository._

> _Please make sure you have the correct access rights
> and the repository exists._

Tente remover o arquivo `~/.ssh/known_hosts`, use o comando:

	$ rm ~/.ssh/known_hosts

tente baixar o repositório git novamente.

_Isso pode acontecer se você cometeu algum erro ao criar a chave SSH e tentou baixar o repositório. Quando for necessário fazer novamente a chave ssh, remova esse arquivo known_hosts._

3- Abra o terminal e rode o comando:

	$ git clone ssh://aur@aur.archlinux.org/nome_pacote.git

Após isso o terminal vai perguntar se você quer adicionar chave de autenticação, digite **Yes** or **Sim**.

Depois disso o terminal vai pedir a **frase secreta** que você criou na autenticação

Depois de terminar é só acessar o pacote

	$ cd "nome do pacote"

4- Agora você pode fazer modificações nos arquivos do pacote.

[_Lembre-se de seguir as recomendações do AUR quanto as informações que devem ser alteradas no arquivo PKGBUILD._](https://wiki.archlinux.org/title/AUR_submission_guidelines)

### Para enviar as mudanças de volta para o AUR:

Agora vamos ensinar a como fazer upload do projeto de volta para o AUR:

1- No terminal, no diretório do projeto, use o comando:

	$ makepkg --printsrcinfo > .SRCINFO

_Caso tenha mexido também no arquivo PKGBUILD_.

	$ git add .

_Isso vai criar uma lista de arquivos modificados_.

	$ git commit -m "mensagem aqui"

**Caso apareça a mensagem:**

> _Please tell me who you are._
>
> _Run_
>
> _git config — global user.email “you@example.com”
> git config — global user.name “Your Name”_

Você vai ter que adicionar o seu email e o nome de usuário, basta seguir o exemplo e usar os comandos:

	$ git config --global user.email "marcos@gmail.com"

	$ git config --global user.name "M4rQu1Nh0S"

Após isso tente novamente usar o comando:

	$ git commit -m "mensagem aqui"

_Aqui você vai dizer brevemente o que foi mudado no pacote_.

	$ git push

_Isso vai fazer o upload do pacote de volta para o AUR_.

Após isso o terminal vai pedir a frase secreta e após isso o pacote no AUR será atualizado.

O tutorial termina aqui, informações adicionais foram omitidas para tornar o tutorial simples e objetivo, lembre-se de estudar o AUR para obter a melhor forma de distribuir seus pacotes no AUR.

Caso tenha encontrado algum erro ou queira sugerir algum procedimento adicional ou mais adequado do que os passados neste tutorial, deixe seu comentário, até a próxima.

