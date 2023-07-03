---
title: Converter BTRFS de volta para EXT4 sem reinstalar o sistema
date: 2023-07-02
author: M4rQu1Nh0S
tags: [reverter, btrfs, para, ext4, sem, formatar, reinstalar, sistema]
subtitle: Saiba como voltar para EXT4 após migrar para BTRFS
category: [Dicas e tutoriais, Linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*Gd1vzT36SspCkhdI.jpg
share-img: https://cdn-images-1.medium.com/max/800/0*Gd1vzT36SspCkhdI.jpg
layout: post
---

<p align='center'><img alt='Foto de um SSD com a legenda BTRFS para EXT4' src="https://cdn-images-1.medium.com/max/800/0*Gd1vzT36SspCkhdI.jpg"/></p>
Hoje é possível trocar o sistema de arquivos EXT4 para BTRFS sem precisar formatar o sistema do zero, pra isso usamos o utilitário de conversão **btrfs-convert.**

Usando o **btrfs-convert** além de você trocar o formato EXT4 para BTRFS você ainda pode reverter a conversão caso não tenha gostado, porque o utilitário cria um backup do sistema de arquivos antigo para uma pasta chamada **ext2_saved.**

No meu caso, eu acabei perdendo essa pasta, portanto eu perdi a possibilidade de reverter a conversão do sistema de arquivos, e agora?

Existem muitos tutoriais que ensinam a converter EXT4 para BTRFS sem perder dados e sem precisar reformatar o PC, mas **converter BTRFS pra EXT4** é diferente, parece que não existe um utilitário pra isso igual aquele btrfs-convert.

Muitos sites simplesmente recomendam formatar o HD e reinstalar o sistema, mas eu procurei meios de trocar o sistema de arquivos sem precisar pelo menos reinstalar o sistema, hoje estou aqui para compartilhar um método para trocar o sistema de arquivos BTRFS de volta para EXT4 sem precisar reinstalar o sistema.

**Conteúdo**

1. [Backup](#1-backup)
2. [Live CD do sistema](#2-live-cd-do-sistema)
3. [Formatar o HD do sistema](#3-formatar-o-hd-do-sistema)
4. [Monte a partição formatada](#4-monte-a-partição-formatada)
5. [Restaure o backup dos arquivos](#5-restaure-o-backup-dos-arquivos)
6. [Reconfigurar o fstab](#6-reconfigurar-o-fstab)
7. [Reconfigurar o grub do sistema](#7-reconfigurar-o-grub-do-sistema)
8. [Usando o Chroot para acessar o sistema](#8-usando-o-chroot-para-acessar-o-sistema)
9. [Referencias](#referencias)

## 1. Backup
Primeiro nós precisaremos fazer o backup dos arquivos que estão no HD onde o sistema está instalado.

Há várias opções para se fazer isso, mas vamos usar o comando **rsync** que vai fazer isso de maneira simples.

Precisamos **abrir o terminal** e usar esse comando:

	$ sudo rsync -aAXv / –exclude={“/dev/“,”/proc/“,”/sys/“,”/tmp/“,”/run/“,”/mnt/“,”/media/“,”/lost+found”}  <destino>

troque pelo endereço do diretório onde vamos salvar esse backup.

Por exemplo: **/media/marcos/HD/bkp_ssd_linux/** (uma pasta que está em **outro HD/partição**)

No meu caso o comando vai ficar assim:

	$ sudo rsync -aAXv / –exclude={“/dev/“,”/proc/“,”/sys/“,”/tmp/“,”/run/“,”/mnt/“,”/media/“,”/lost+found”}  /media/marcos/HD/bkp_ssd_linux/

## 2. Live CD do sistema
Depois de fazer o backup, vamos precisar usar uma LiveCD de alguma distro, com ela vamos formatar a partição do sistema, restaurar os arquivos e reconfigurar o GRUB, etc.

Enfim, baixe alguma LiveCD ou use a ISO do sistema que você instalou no PC, no meu caso será o KDE Neon 22.04

## 3. Formatar o HD do sistema.

Depois de dar boot no LiveCD do sistema, vamos ter que usar alguma ferramenta para formatar o HD, eu costumo usar o **gparted**. O objetivo aqui é simples, vamos apagar a partição do sistema que está em BTRFS e criar uma outra em EXT4.

No meu caso, a partição do sistema fica em /dev/sdb2.

## 4. Monte a partição formatada
Depois que de criar a partição com o formato EXT4, basta fazer a montagem.

No terminal use o comando:

	$ sudo mount /dev/sdb2 /mnt

A partição do sistema (/dev/sdb2) vai ser montada no diretório **/mnt**

## 5. Restaure o backup dos arquivos
Agora que a partição do sistema está montada, vamos restaurar os arquivos do sistema.

Abra o terminal e use o comando:

	$ sudo rsync -aAXv <origem_backup> <destino>

é o local de backup dos diretórios do sistema (/bin /etc /lib… entre outros).

será o diretório onde a partição do sistema está montada (/mnt)

**Veja como fica no meu caso:**

	$ sudo rsync -aAXv /media/marcos/HD/bkp_ssd_linux/ /mnt

Aguarde a conclusão do processo.

## 6. Reconfigurar o fstab
Depois de restaurar os arquivos do sistema na partição do sistema, que agora está em EXT4, vamos precisar editar o arquivo **/etc/fstab** e atualizar as informações referente a partição do sistema, principalmente o **UUID** e o **sistema de arquivos**.

Edite o arquivo **fstab** com o comando:

	$ sudo nano /mnt/etc/fstab

Procure por algo assim:

>UUID=6bb86066–5a14–42b2-b2cb-c5d2ae4303d0 / **btrfs** defaults 0 0

Aqui vamos precisar trocar o UUID e substituir o **btrfs** por **ext4**, ficando assim:

>UUID=30bb1f16-f4c7–4807-bfa5-ed8b872304b5 / **ext4** defaults 0 0

_Para descobrir o atual UUID basta usar o comando:_

	$ sudo blkid /dev/sdb2

_/dev/sdb2 é um exemplo_

Depois de fazer as alterações, aperte **Ctrl + X** e depois **Y ou S** para salvar.

## 7. Reconfigurar o grub do sistema
Depois de editar o arquivo **fstab** só falta reconfigurar o grub do sistema.

Abra o terminal e digite:

	$ kate /mnt/boot/grub/grub.cfg

**_kate_** _é o nome do editor de texto que eu uso no KDE, se você usa GNOME então o é_ **_gedit_**_, no MATE é o_ **_xed_**_, etc._

Ao abrir o arquivo, basta substituir todos os **“insmod btrfs**” por **“insmod ext2**” (é ext2 mesmo)

Depois salve o arquivo.

## 8. Usando o Chroot para acessar o sistema
Agora só falta acessar o sistema da partição restaurada para reconfigurar o boot.

Use os comandos abaixo:

	# touch /mnt/.autorelabel

	# mount -t proc none /mnt/proc && mount -t sysfs none /mnt/sys && mount -o bind /dev /mnt/dev && mount -o bind /dev/pts /mnt/dev/pts

	# chroot /mnt bash

Com isso estamos acessando o bash do sistema do sistema restaurado, agora podemos atualizar o boot do sistema.

Use o comando abaixo:

### Para BIOS Legacy/CSM:

	# grub-install --target=i386-pc /dev/sdb1 (exemplo)

(**/dev/sdb1** partição de boot, costuma estar em FAT32 e sua capacidade é 8Mb, pode variar dependendo do sistema)

### Para UEFI:

	# mount /boot/efi

	# grub-install --efi-directory=/boot/efi

	# grub-mkconfig -o /boot/grub/grub.cfg

Reinicie o PC

Com isso está terminado, seu sistema está em uma partição EXT4 e deverá dar boot normalmente.

Pode ser necessário reconfigurar a **Memória** **SWAP**, recomendo seguir os procedimentos no artigo do Diolinux, tal artigo serviu como referencia para este tutorial.

[Como converter EXT4 para BTRFS sem perder dados](https://diolinux.com.br/tutoriais/converter-ext4-para-btrfs.html)

## Referencias:
- [https://diolinux.com.br/tutoriais/converter-ext4-para-btrfs.html](https://diolinux.com.br/tutoriais/converter-ext4-para-btrfs.html)
- [https://www.pcguia.pt/2020/07/terminal-linux-fazer-backup-em-linux-com-rsync/](https://www.pcguia.pt/2020/07/terminal-linux-fazer-backup-em-linux-com-rsync/)

