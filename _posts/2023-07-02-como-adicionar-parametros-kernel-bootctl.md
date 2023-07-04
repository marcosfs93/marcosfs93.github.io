---
title: Como adicionar parâmetros de kernel no bootctl
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, adicionar, parametros, kernel, bootctl, opções]
subtitle: Aprenda a como adicionar parametros e opções no bootctl
categories: [dicas e tutoriais, linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*kkDV351ft6x-EGfy.png
share-img: https://cdn-images-1.medium.com/max/800/0*kkDV351ft6x-EGfy.png
layout: post
---

<p align='center'><img alt='Screenshot do manual do bootctl' src="https://cdn-images-1.medium.com/max/800/0*kkDV351ft6x-EGfy.png"/></p>
Nem todas as distribuições Linux usam o GRUB como carregador de inicialização do sistema, o Pop! OS por exemplo usa no lugar do GRUB o **bootctl** do systemd, principalmente quando você instala o sistema em modo UEFI.

Enquanto no GRUB editamos o arquivo /etc/default/grub, adicionamos parâmetros do kernel e então usamos o comando **update-grub** no terminal, com o bootctl o processo é diferente.

Nesse artigo de hoje eu vou mostrar pra vocês como se faz para editar e adicionar parâmetros de kernel em distros que usam o bootctl, como é o caso do Pop OS.

Adicionar parâmetros no kernel permitem inicializar módulos específicos, no meu caso eu uso dois, um que me permite limitar o nivel C-State da CPU e outro que força a ativação do módulo DRM, da minha placa de vídeo Nvidia.

## Criando uma nova entrada no bootctl

Por exemplo no Pop OS, que usa o bootctl, vamos precisar mexer com dois arquivos: **loader.conf** e **Pop_OS-current.conf**

1.  Abra o arquivo loader.conf, o local dele é **/boot/efi/loader/loader.conf**
2.  Substitua a linha “**default Pop_OS-current**” por “**default Pop_OS-custom**”
3.  Salve o arquivo.

Agora vamos precisar criar uma cópia do arquivo **Pop_OS-current.conf** e depois **mudar o nome do arquivo**

1.  Vá para diretório **/boot/efi/loader/entries/**
2.  Faça uma cópia do arquivo **Pop_OS-current.conf**, você pode fazer isso usando Ctrl + C e Ctrl + V.
3.  Depois disso mude o nome desse arquivo para **Pop_OS-custom.conf**
4.  Abra o arquivo **Pop_OS-custom.conf**

Ao abrir o arquivo você verá algo mais ou menos assim:

>title Pop!_OS
linux /EFI/Pop_OS-5b86ca34-a90e-4394-8049-c81207d92cf7/vmlinuz.efi
initrd /EFI/Pop_OS-5b86ca34-a90e-4394-8049-c81207d92cf7/initrd.img
options root=UUID=5b86ca34-a90e-4394-8049-c81207d92cf7 ro quiet loglevel=0 systemd.show_status=false splash

Para adicionar parametros de kernel é só acrescentar eles após a ultima parte da linha **options**, veja como fica no meu caso:

>title Pop!_OS
linux /EFI/Pop_OS-5b86ca34-a90e-4394-8049-c81207d92cf7/vmlinuz.efi
initrd /EFI/Pop_OS-5b86ca34-a90e-4394-8049-c81207d92cf7/initrd.img
options root=UUID=5b86ca34-a90e-4394-8049-c81207d92cf7 ro quiet loglevel=0 systemd.show_status=false splash **intel_idle.max_cstate=2 nvidia-drm.modeset=1**

O que eu fiz foi colocar opçãos adicionais no final da linha **options**, que no caso foi `intel_idle.max_cstate=2` e `nvidia-drm.modeset=1`

Pronto, na proxima vez que você reiniciar o sistema, os parametros serão carregados junto com o Linux.

**Nota:** Você não deve editar o proprio arquivo **Pop_OS-current.conf** pois ele é “resetado” toda vez que o kernel é atualizado, ou quando o sistema roda o **update-initramfs**. É por isso que precisamos criar uma cópia dele com outro nome.

Bom pessoal, acredito que seja apenas isso mas se você encontrar algum problema ou queira colaborar com o artigo é só deixar o seu comentário, até a próxima e um bom 2023 a todos.

