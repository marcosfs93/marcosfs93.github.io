---
title: Linux - Diminuindo a resolução de tela para um App
date: 2023-07-02
author: M4rQu1Nh0S
tags: [linux, diminuir, resolução, tamanho, do, app, aplicativo]
subtitle: Aprenda a alterar a resolução dos app
categories: [dicas e tutoriais, linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*LuCfGjrSx4b8Gm30.png
share-img: https://cdn-images-1.medium.com/max/800/0*LuCfGjrSx4b8Gm30.png
layout: post
---

<p align='center'><img alt='comparativo do app com resolucao padrao e com a versao reduzida' src="https://cdn-images-1.medium.com/max/800/0*LuCfGjrSx4b8Gm30.png"/></p>
Nem todo mundo está usando a resolução Full HD no PC (1920x1080) e podem existir apps que só funcionam perfeitamente a partir dessa resolução, caso contrário parte da sua interface não vai caber na tela, o que pode prejudicar sua experiencia e produtividade com o app.

Felizmente no Linux, seja GTK ou QT, é possível reduzir o tamanho da sua interface exclusivamente para um app especifico, a seguir vou compartilhar os comandos que ajudam a diminuir o **DPI** ou o tamanho das **fontes**, cada app vai se comportar de uma forma diferente, dependendo do comando.

## Para aplicativos GTK:

GDK_SCALE=0.9
**GDK_DPI_SCALE=0.9**

## Para aplicativos QT:

QT_AUTO_SCREEN_SET_FACTOR=0
QT_SCALE_FACTOR=0.9
QT_FONT_DPI=96
**QT_AUTO_SCREEN_SCALE_FACTOR=0.9**

## Se o app estiver em flatpak:
O comando é igual ao de cima só muda o começo, veja::

    flatpak override --user --env=**GDK_DPI_SCALE=0.9**  com.gnome.gedit

No caso dos flatpaks se atente se o app é baseado em gtk ou qt.

## Exemplo:
Então supondo que eu quero executar o editor de texto **gedit**, mas quero que a escala seja 0.10x menor que o tamanho normal, sendo assim devo ir ao terminal e executar o comando:

    $ GDK_DPI_SCALE=0.9 gedit

Ou se eu quiser executar o Kdenlive com a escala reduzida:

    $ QT_AUTO_SCREEN_SCALE_FACTOR=0.9 kdenlive

## Conclusão:
É possível tornar essas mudanças permanente, inclusive dá pra mexer na escala da interface do sistema como um todo, mas por hoje o proposito foi apenas informar quais os comandos que tornam isso possível.

Alias, quando se trata de apps em Qt no Flatpak a configuração pode não dar certo, eu tive uns problemas com o Kdenlive flatpak, o escalonamento funciona melhor no app nativo ou na versão AppImage.

### Referências:

- [https://unix.stackexchange.com/questions/596887/how-to-scale-the-resolution-display-of-the-desktop-and-or-applications](https://unix.stackexchange.com/questions/596887/how-to-scale-the-resolution-display-of-the-desktop-and-or-applications)
- [https://github.com/flathub/us.zoom.Zoom/issues/190#issuecomment-1133644211](https://github.com/flathub/us.zoom.Zoom/issues/190#issuecomment-1133644211)

