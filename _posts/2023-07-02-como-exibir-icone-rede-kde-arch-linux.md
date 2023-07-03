---
title: Como exibir o ícone de redes no Arch Linux com KDE
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, exibir, aparecer, icone, redes, arch linux, kde]
subtitle: Saiba como fazer para o icone aparecer novamente
category: [Dicas e tutoriais, Linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*hR6iAwV4ZLmNGI8y.png
share-img: https://cdn-images-1.medium.com/max/800/0*hR6iAwV4ZLmNGI8y.png
layout: post
---

![](https://cdn-images-1.medium.com/max/800/0*hR6iAwV4ZLmNGI8y.png)<br/>
Recentemente eu instalei o Arch Linux e escolhi o KDE como interface gráfica, porém eu instalei o KDE usando o comando:

    $ sudo pacman -S plasma-desktop

Esse comando faz o sistema instalar apenas o minimo do KDE, sem blotwares. Após terminar de instalar os demais aplicativos, eu percebi que na área de notificação o ícone de redes, que costuma aparecer no KDE em outras distros, estava faltando.

Para resolver isso, eu precisei fazer 3 coisas:

1- Instalar o plasma-nm

    $ sudo pacman -S plasma-nm

2- Iniciar e permitir o autostart do serviço NetworkManager

    $ sudo systemctl enable --now NetworkManager

3- Sair da sessão e logar novamente no sistema

Com isso o icone de redes volta a aparecer na area de notificações do KDE, se você passou por isso, deixe seu comentário.

Se está com problemas com o icone de volume da area de notificação, veja este artigo:
[Como exibir o ícone de volume no Arch Linux com KDE](https://marcosfs93.blogspot.com/2023/06/como-exibir-o-icone-de-volume-no-arch.html)
