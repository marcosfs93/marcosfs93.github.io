---
title: Como exibir o ícone de volume no Arch Linux com KDE
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, exibir, aparecer, icone, volume, arch linux, kde]
subtitle: Saiba como fazer para o icone aparecer novamente
categories: [dicas e tutoriais, linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*i_FkgnXCMMTFNJtf.png
share-img: https://cdn-images-1.medium.com/max/800/0*i_FkgnXCMMTFNJtf.png
layout: post
---

<p align='center'><img alt='Imagem do icone de volume na area de notificação do KDE' src="https://cdn-images-1.medium.com/max/800/0*i_FkgnXCMMTFNJtf.png"/></p>
Além do icone de redes, o icone de volume também estava faltando na area de notificação do KDE, que instalei no Arch Linux.

Esse problema é resolvido instalando um o pacote `plasma-pa`, use esse comando para instalar esse pacote:

    $ sudo pacman -S plasma-pa

Depois disso é só sair da sessão e logar novamente no sistema

Caso você tenha instalado o **pipewire** como servidor de audio, talvez seja necessário instalar o pacote `pipewire-pulse`, mas tente fazer isso apenas se a instalação do pacote `plasma-pa` não resolver o problema.

Caso tenha instalado esse pacote também, recomendo reiniciar o PC.

Se está com problemas com o icone de redes da area de notificação, veja este artigo:
[Como exibir o ícone de rede no Arch Linux com KDE](https://marcosfs93.github.io/2023-07-02-como-exibir-icone-rede-kde-arch-linux/)

