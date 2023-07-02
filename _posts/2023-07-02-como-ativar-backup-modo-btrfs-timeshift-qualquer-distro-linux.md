---
title: Como ativar o backup em modo BTRFS do Timeshift em qualquer distro Linux
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, ativar, backup, modo, btrfs, timeshift, qualquer, distro]
subtitle: Aprenda a como usar o Timeshift em qualquer distro Linux
category: [linux]
comments: true
---

<p><a href="https://cdn-images-1.medium.com/max/800/0*qzLSKIQsul76GVEl.png" style="text-align: center;"><img alt="Screenshot da interface do Timeshift" src="https://cdn-images-1.medium.com/max/800/0*qzLSKIQsul76GVEl.png" title="Screenshot da interface do Timeshift" /></a></p>
Para quem usa distros como Ubuntu, Linux Mint e Zorin OS, é muito fácil fazer os backups do sistema, seja com RSYNC ou BTRFS, pois nessas distros ao escolher uma partição em BTRFS automaticamente o subvolume **@** é criado.

No timeshift as partições BTRFS precisam do subvolume **@**, qualquer outro nome de subvolume não será aceito no timeshift e daí você só poderá fazer backups em modo RSYNC, mesmo que o sistema esteja em uma partição BTRFS.

Um exemplo disso é o Debian 12 Bookworm, não sei se outras versões do Debian tem essa caracteristica, mas qualquer partição BTRFS que você criar na instalação do sistema vai ter o subvolume **@rootfs**

Daí ao tentar fazer backup BTRFS no timeshift você vai encontrar o erro de subvolume, o Debian usa o subvolume [@rootfs](https://github.com/rootfs) ao invés do subvolume @ e o timeshift só aceita subvolume @ ou [@home](https://github.com/home).

Enfim, no meu caso eu precisei fazer algumas coisas para conseguir fazer o timeshift funcionar no Debian Bookworm.

## Tutorial em vídeo está disponível

<video src='https://www.youtube.com/watch?v=TFhoBYakkY4' width=480></video>

Primeiro eu precisei editar alguns arquivos:

1- **/boot/grub/grub.cfg**

Nesse arquivo precisei substituir todas as palavras “@rootfs” por apenas “@”

2- **/EFI/debian/grub.cfg**

Esse arquivo acima, em questão, está presente na **partição EFI** do sistema, nesse arquivo precisei substituir “@rootfs” por apenas “@”

3- **/etc/fstab**

A mesma coisa, substituir “@rootfs” por apenas “@” referente a partição do sistema.

Com os arquivos editados bastava apenas alterar o nome do subvolume [@rootfs](https://github.com/rootfs) da partição do sistema, como isso não era possivel de se fazer com o sistema rodando, foi necessário obter e dar boot em uma LiveCD do Linux.

Ao dar boot na LiveCD, basta abrir a partição que contem o sistema, é necessário saber qual é o endereço da partição BTRFS.

Aqui no meu PC a partição do sistema está no “endereço” **/dev/sdb3**

Sabendo o endereço do HD, é só usar o próximo comando:

    $ mount -o subvolid=0 /dev/sdb3 /mnt

Depois basta abrir o gerenciador de arquivos e entrar na pasta **/mnt**, assim que você entrar na pasta você verá uma pasta contendo o nome do subvolume atual do sistema, aqui você só precisa alterar o nome dessa pasta.

Para mudar o nome do subvolume, basta usar o comando:

    $ sudo mv [@rootfs](https://github.com/rootfs) @

Após isso basta sair da liveCD e dar boot no sistema, e então o Timeshift e os backups em BTRFS começaram a funcionar.

Caso você já esteja com o subvolume @ e mesmo assim o timeshift não reconhecer, use o comando abaixo:

    $ sudo btrfs subvolume set-default 5 /

## Referencias:

[https://groups.google.com/g/linux.debian.user/c/4Qg3Fxv_pHo](https://groups.google.com/g/linux.debian.user/c/4Qg3Fxv_pHo)
