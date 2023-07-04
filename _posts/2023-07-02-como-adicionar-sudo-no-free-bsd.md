---
title: Como adicionar o comando sudo no sistema
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, adicionar, comando, sudo, free, bsd]
subtitle: Aprenda a instalar e habilitar a função
categories: [dicas e tutoriais, BSD]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/1*ldbmKT7AU0giAcDb7LDziQ.png
share-img: https://cdn-images-1.medium.com/max/800/1*ldbmKT7AU0giAcDb7LDziQ.png
layout: post
---

<p align='center'><img alt='logo FreeBSD' src="https://cdn-images-1.medium.com/max/800/1*ldbmKT7AU0giAcDb7LDziQ.png"/></p>
Apesar do FreeBSD ser um sistema com uma estrutura aparentemente igualzinha a do linux, existem certos elementos que podem ser diferentes. Um exemplo e tema desse post é o comando **sudo**, que permite aumentar os privilégios de acesso do usuário, que no linux ele já vem instalado por padrão em quase todas as distribuições.

Quando instalamos o FreeBSD e tentamos fazer as mesmas coisas que fazemos no linux, como por exemplo, usar o sudo pra instalar um aplicativo, no BSD você tem uma mensagem de que o comando sudo não existe.

Acontece que no FreeBSD o sudo não vem instalado, para fazer esse comando funcionar precisamos instalar a aplicação, ou fazer login no usuário root manualmente.

Logue no sistema usando o usuário **root** pelo prompt do sistema. Para isso basta digitar o comando **login** e apertar Enter
Aí o sistema vai pedir para que você digite a senha, coloque a senha que você escolheu e aperte enter.

Feito isso, basta instalar o pacote **sudo**

    # pkg install sudo

Com isso o comando sudo já estará funcionando, porem… funcionando somente para o usuário root. Em um sistema como o linux por exemplo, temos pelo menos **dois usuários**, um é o root e o outro é o seu **usuário comum**.

Vamos precisar fazer com que o comando sudo funcione tambem para os demais usuários para o caso de haver a necessidade de elevar o acesso em determinado momento, como por exemplo instalar novos aplicativos.

Para fazer o comando sudo funcionar nos demais usuários, vamos precisar editar o arquivo **sudoers**, supondo que você não tenha ainda uma interface gráfica instalada e ativada, instale o pacote **nano** com o comando:

    # pkg install nano

Bom, inicialmente já temos o que precisamos:

- Estar logado no usuário root
- ter o pacote nano instalado
- ter o pacote sudo instalado

Para fazer o comando sudo funcionar vamos precisar incluir os demais usuários no arquivo sudoers. use o comando abaixo:

    # sudo nano /usr/local/etc/sudoers

Após isso a tela vai mudar e no canto de baixo, em vermelho, você vai ter a mensagem
**[ Error reading /usr/local/etc/sudoers is meant to be read only ]**

Vamos precisar permitir o nano de fazer alterações no arquivo, aperte **Ctrl + O** para desbloquear e depois aperte **Enter**.

Agora desça a pagina usando as setas do teclado, desça até a parte **## user privilege** **specification**

Abaixo de **root ALL=(ALL) ALL** escreva na linha de baixo **usuário ALL=(ALL) ALL**
Troque **usuário** pelo nome do usuário da sua maquina. Exemplo:

> _marcos ALL=(ALL) ALL_

No meu caso esse trecho ficou assim:

> _## User privilege specification
> root ALL=(ALL) ALL
> marcos ALL=(ALL) ALL_

Aperte **Ctrl + X**, Aperte **Y** e depois **Enter** pra salvar as alterações.

Digite **Exit** pra sair do usuário root.

Caso não tenha retornado para o usuário normal, digite o comando **login** e faça login na sua conta normal.

Depois é só testar, vamos tentar instalar o **wget** usando pkg junto com o sudo

    # sudo pkg install wget

Se der certo o pkg vai perguntar se você quer fazer a instalação. até aí já comprovamos que o comando sudo está funcionando perfeitamente.

Usar o sudo é mais pratico do que fazer o login de forma manual, espero que tenha sido util.

