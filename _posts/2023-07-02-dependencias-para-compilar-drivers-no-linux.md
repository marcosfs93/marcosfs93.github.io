---
title: Dependências para compilar driver no linux
date: 2023-07-02
author: M4rQu1Nh0S
tags: [dependências, para, compilar, drivers, linux, pacotes]
subtitle: Saiba quais os pacotes que você precisa para compilar drivers
categories: [dicas e tutoriais, linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*2IY9plLOxzdYSJYo.png
share-img: https://cdn-images-1.medium.com/max/800/0*2IY9plLOxzdYSJYo.png
layout: post
---

<p align='center'><img alt='Placa de rede ilustrativa' src="https://cdn-images-1.medium.com/max/800/0*2IY9plLOxzdYSJYo.png"/></p>
r8168 é um driver de rede para placas realtek, no linux um driver é um módulo do kernel.

Se você precisa compilar este driver, é importante saber quais as dependencias são necessárias antes de compilar, pois sem as dependencias você vai encontrar erros no momento da compilação do driver.

Neste artigo vou informar quais as dependencias dependendo da distro usada.

## Dependências:
**Para Debian/Ubuntu:**

    $ apt install make gcc linux-headers dkms build-essentials

**Para Arch Linux:**

    $ pacman -S dkms glibc linux-headers make

**Para Fedora:**

    $ yum -y kernel-devel gcc make dkms

Assim que as dependencias são instaladas o driver pode ser instalado usando o comando:

    $ sudo ./autorun.sh
