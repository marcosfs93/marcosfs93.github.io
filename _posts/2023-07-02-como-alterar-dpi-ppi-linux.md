---
title: Como alterar o PPI ou DPI no Linux
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, alterar, dpi, ppi, linux]
subtitle: Aprenda como alterar o tamanho de DPI do sistema
category: [Dicas e tutoriais, Linux]
comments: true
cover-img: https://cdn-images-1.medium.com/max/800/1*nG5inNzRcQ_GvkbvouL8rQ.png
thumbnail-img: https://cdn-images-1.medium.com/max/800/1*nG5inNzRcQ_GvkbvouL8rQ.png
share-img: https://cdn-images-1.medium.com/max/800/1*nG5inNzRcQ_GvkbvouL8rQ.png
layout: post
---

Eu não sei se esse problema só é perceptível para mim, já que eu ainda uso a resolução 1366x768 no meu monitor LCD de 15 polegadas.

Durante o tempo que usei Windows e comecei a usar o Linux, eu percebi que o tamanho das coisas eram um pouco maiores do que deviam, o mesmo app para ambos os sistemas tinham diferenças no seu tamanho.

Após pesquisar, eu entendi que no Windows o tamanho de PPI (ou DPI) era **96**, enquanto no Linux, dependendo da interface, o numero era a partir de 100 PPI, o que explicava essa diferença no tamanho.

Após entender essa diferença eu decidi alterar o tamanho do DPI no Linux, para que fique igual ao Windows. Hoje vamos aprender a como fazer isso.

## 1. Editar o arquivo “/etc/X11/xorg.conf”

Veja se esse arquivo existe, abra o terminal e use o comando:

    $ cat /etc/X11/xorg.conf

Se o arquivo existir, as informações do conteudo vão aparecer no terminal.

----------

Caso esse arquivo não exista, vamos criar esse arquivo contendo as configurações atuais do Xorg, use o comando abaixo:

    $ sudo X -configure

Esse comando vai gerar o arquivo em “/root/xorg.conf.new”. Agora use o comando abaixo para copiar esse arquivo para o diretório do Xorg:

    $ sudo cp /root/xorg.conf.new /etc/X11/xorg.conf

Pronto, o arquivo foi criado e contem as mesmas configurações no qual o sistema está usando neste momento.

----------

## 2. Fazer backup e editar o arquivo xorg.conf:

Vamos começar fazendo o backup do arquivo atual, use o comando no terminal:

    $ sudo cp /etc/X11/xorg.conf /etc/X11/xorg.conf.bkp

Depois de fazer a cópia, vamos editar o arquivo original:

    $ sudo nano /etc/X11/xorg.conf

Após abrir o arquivo precisamos encontrar essa parte:

> Section “Device”

Dentro dessa parte adicione uma linha nova, contendo essa descrição:

> Option              "DPI" "96 x 96"

## 3. Após isso salve o arquivo

Usando as teclas **Ctrl + X** e depois **Y ou S**.

Para servir de referencia, o meu arquivo xorg.conf ficou assim:

![](https://cdn-images-1.medium.com/max/800/1*nG5inNzRcQ_GvkbvouL8rQ.png)

Depois disso basta reiniciar o sistema, ao iniciar você vai perceber que o tamanho da interface dos apps vai ficar mais semelhante ao que é no Windows.

Caso você não use Nvidia e a dica não tenha funcionado com você, deixe seu comentário informando qual placa você usa.

### Referencias:
[https://wiki.archlinux.org/title/Xorg](https://wiki.archlinux.org/title/Xorg)
