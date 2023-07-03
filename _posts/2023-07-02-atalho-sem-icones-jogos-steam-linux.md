---
title: Atalho dos Jogos da Steam sem ícones no Linux
date: 2023-07-02
author: M4rQu1Nh0S
tags: [atalho, jogos, steam, linux, sem, icones]
subtitle: Saiba como fazer para resolver o problema
category: [Dicas e tutoriais, Linux]
comments: true
#cover-img: https://cdn-images-1.medium.com/max/800/0*Ctsj_IhWRvBBVbQq.png
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*Ctsj_IhWRvBBVbQq.png
share-img: https://cdn-images-1.medium.com/max/800/0*Ctsj_IhWRvBBVbQq.png
layout: post
---

<img align="left" alt='Screen shot dos atalhos sem icones' src="https://cdn-images-1.medium.com/max/800/0*Ctsj_IhWRvBBVbQq.png"/>
Esse é um tipo de problema que pode acontecer quando você vai trocar de distribuição Linux e prefere fazer backup da pasta **.steam** da pasta **/home/<user>** do que reinstalar tudo do zero.

Acontece que a Steam ao ser instalada no Linux ela criar e armazena os arquivos dela e os seus jogos na pasta **“~/.steam”** e por isso é bem pratico copiar e colar essa pasta ao reinstalar ou mudar de sistema, do que baixar tudo de novo.

## Fazendo backup dos jogos com os atalhos e ícones
Existem arquivos da Steam que ficam fora do diretório .steam: Os ícones dos jogos e o atalho dos aplicativos.

Os ícones dos jogos da Steam ficam localizados dentro do diretório “**~/.local/share/icons/hicolor**”, com o nome começando com **steam_icon_id** no caso do CS GO o id é **730**, ou seja **steam_icon_730** é o nome do arquivo de ícone do CS GO.

O atalho dos jogos, que aparecem no menu de aplicativos do sistema, ficam localizados dentro do diretório “**~/.local/share/applications”**. o nome dos arquivos geralmente tem o mesmo nome dos jogos

Então para evitar problemas é importante fazer o backup desses 3 diretórios:

1.  “~/.steam”
2.  “~/.local/share/icons/hicolor”
3.  “~/.local/share/applications”

Existem diversos tutoriais que ensinam a gerar atalhos para aplicativos e também ícones dos atalhos, a forma mais fácil e direta para reparar esse problema é reinstalando a Steam do zero.

## Recriando os atalhos e os ícones
É necessário reinstalar a Steam, normalmente uma reinstalação baixa tudo do zero, mas se você não quer baixar tudo de novo, você pode pelo menos fazer isso:

1-  Fazer o backup da pasta: **~/.steam/debian-installation/steamapps/common**
2-  Fazer o backup da pasta: **~/.steam/debian-installation/userdata/**
3-  Apagar a pasta **~/.steam**
4-  Reinstalar a Steam
5-  Criar o diretório vazio da pasta **common**, com o comando no terminal:

    $ mkdir -p ~/.steam/debian-installation/steamapps/common

6- Restaurar o backup da pasta **common** que foi salvo anteriormente

7- Criar o diretório vazio da pasta **userdata**, com o comando no terminal:

    $ mkdir -p ~/.steam/debian-installation/userdata

8- Restaurar o backup da pasta **userdata** que foi salvo anteriormente

9- Abrir o App da Steam e selecionar o jogo e clicar em Instalar

Com isso a Steam vai verificar que os arquivos do jogo já existe, então ela vai apenas checar os arquivos e criar o atalho no sistema, já com o ícone aparecendo.

De acordo com os meus testes essas instruções são suficientes, mas por via das duvidas é importante fazer o backup da pasta principal **~./steam** e restaurar só a pasta **common** e **userdata**.

Veja o resultado agora:

<img align="left" alt='Screenshot após recuperar os icones dos atalhos' src="https://cdn-images-1.medium.com/max/800/1*Hg48LKYjw4PnvPp8cqG3rw.png"/>

Bom pessoal, é isso, a recriação dos atalhos e ícones é feito somente uma vez, daí você pode fazer o backup da pasta **“~/.steam”**, **“~/.local/share/icons/hicolor”** e **“~/.local/share/applications”** já que é mais rápido.

Até o próximo post e um feliz ano novo a todos!
