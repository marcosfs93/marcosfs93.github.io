---
layout: post
title: Tutorial de instalação do Arch Linux simplificado
author: M4rQu1Nh0S
tags: tutorial, arch, linux, simples, resumido, simplificado, instalação.
subtitle: Tutorial simples para instalação do Arch Linux
category: Linux
---

![menu de boot do instalador do arch linux](https://miro.medium.com/v2/resize:fit:700/1*tucba-ygaPv5NH-wHVxgoQ.jpeg)
O guia de instalação no site do Arch Linux é completo, o que torna também um pouco complexo devido aos vários estágios de configuração durante a instalação, incluindo os seus detalhes.

Esse guia aqui vai servir para eu mesmo, já que eu vou acabar instalando o Arch Linux no futuro, basicamente o que eu vou fazer aqui é um resumo dos procedimentos que eu vou fazer para instalar o Arch no meu PC.

Sendo assim o tutorial de instalação vai ser bem mais simplificado e por isso pode ser útil para outras pessoas também.

## **Conteúdo:**

-   [Iniciando a instalação do Arch Linux](#Iniciando-a-instalação-do-Arch-Linux)
-   1.  [Selecionar o layout do teclado](#)
-   2.  [Saber se o PC está rodando em modo BIOS ou UEFI](#)
-   3.  [Verificar se a internet está funcionando](#)
-   4.  [Configure o relógio (se necessário)](#)
-   5.  [Particione o disco](#)
-   - 5.1.  [Alterar tabela de partição do disco, ou manter a atual](#)
-   - 5.2.  [Altere ou crie novas partições para o sistema](#)
-   - 5.3.  [Altere o tipo das partições](#)
-   - 5.4.  [Formate as partições recém criadas](#)
-   - 5.4.1.  [Sistema](#)
-   - 5.4.2.  [Boot](#)
-   - 5.4.3.  [Swap](#)
-   6.  [Monte as partições](#)
-   - 6.1.  [Partição do sistema](#)
-   - 6.2.  [Partição de boot](#)
-   7.  [Instalando o sistema](#)
-   8.  [Configurando o sistema](#)
-   8.1.  [Fuso horário](#)
-   8.2.  [Localização](#)
-   8.3.  [Configuração de rede](#)
-   8.4.  [Criar o initramfs (opcional)](#)
-   8.5.  [Senha do root](#)
-   8.6.  [Instalar o Bootloader](#)
-   [Pós instalação](#)
-   1.  [Adicionando o usuário](#)
-   2.  [Habilitando o comando sudo para o usuário](#)
-   [Acabamos só que não](#)

# Iniciando a instalação do Arch Linux.

# 1- Selecionar o layout do teclado

Depois de fazer um pendrive bootavel e reiniciar o PC para instalar o Arch Linux, vamos usar o comando abaixo para selecionar o tipo layout do teclado:

# loadkeys br-abnt

**OU**

# loadkeys br-abnt2

# 2- Saber se o PC está rodando em modo BIOS ou UEFI

Isso é importante na hora de instalar o bootloader do sistema, precisamos saber se o PC está funcionando neste momento em modo BIOS ou UEFI enquanto o instalador do Arch Linux está rodando.

Basta usar o comando:

# ls /sys/firmware/efi/efivars

Se um diretório existir e não aparecer erros, o PC está em modo UEFI. Se não aparecer um diretório então o PC está BIOS/CSM.

Caso o PC esteja funcionando em um modo BIOS ou UEFI e você não quiser assim, reinicie o PC e tente dar boot no instalador do Arch Linux no modo que preferir, seja UEFI ou BIOS, usando o comando acima pra consultar.

# 3- Verificar se a internet está funcionando

Basta usar o comando:

# ping archlinux.org

Aqui como eu uso a conexão DHCP a internet já fica funcionando por padrão ao dar boot no instalador do arch linux.

Caso o comando ping não estiver funcionando:

Se o comando ping não funcionar, verifique se as interface estão aparecendo no sistema usando o comando:

# ip link

Caso sua conexão seja…

**DHCP**: funciona automaticamente ao iniciar o instalador do Arch Linux  
**Ethernet**:  **conecte o cabo**  no PC  
**Wifi**: Faça login, usando o comando:  **iwctl**  
**Banda larga móvel**: use o comando:  **mmcli**

Com o comando ping funcionando, vamos continuar.

# 4- Configure o relógio (se necessário)

É importante que a hora do sistema está correta, normalmente um PC não fica com a hora desconfigurada a não ser que você tenha feito um reset CMOS da bios ou se você mudou de fuso horário.

De qualquer forma você só precisa de duas coisas: Ajustar a hora e escolher o fuso horário.

Para ajustar a data e a hora, use o comando:

# timedatectl set-time "2012-10-30 18:17:16"  
(Ano-Mes-Dia, nessa ordem e com aspas)

# 5- Particione o disco

Chegou a minha parte mais chata e que motivou a criar esse artigo de hoje, o tutorial do arch linux recomanda usar o  **fdisk**  para particionar os discos, mas eu prefiro usar o  **cfdisk**  pois ele parece mais simples de se usar e mais amigável.

Vamos começar obtendo a lista de discos disponiveis no sistema, use o comando:

# fdisk -l (ou blkid)

## 5.1- Alterar tabela de partição do disco, ou manter a atual

Antes de alterar o disco, você vai criar uma nova tabela de partição do disco? ou seja, vai mudar o disco atual para GPT ou MBR? ou você vai manter a tabela de partição atual e vai apenas mexer com as partições existentes?

Isso é importante, se você vai criar uma nova tabela de partição, o comando que você deve usar é:

# cfdisk -z /dev/sda (exemplo)

Ao mudar a tabela de partição todas as partiçoes deste disco serão excluidas, incluindo todos os dados. Porém se você vai manter a tabela de particionamento do disco e só vai alterar as partições do sistema, o comando deve ser esse:

# cfdisk /dev/sda (exemplo)

Isso vai te permitir excluir somente as partições que você preferir, tipo a partição do sistema, swap e de boot e manter o restante sem alterações.

## 5.2- Altere ou crie novas partições para o sistema

Ao abrir o cfdisk, comece criando as partições do sistema, do bootloader e do swap, se preferir.

Crie 1, 2 ou 3 partições usando a opção  **New**

A primeira partição será do sistema, escolha o tamanho dessa partição e reservando algum espaço para as demais partições

A partição de boot EFI, deve ter em média 300Mb até 1Gb, enquanto a partição de swap pode ter em média de 2 a 4Gb, podendo ser maior conforme preferir.

## 5.3- Altere o tipo das partições

Agora precisamos escolher o tipo de cada partição, selecione a partição da lista e entre na opção  **Type**  do cfdisk.

A partição / do sistema deve ser o tipo:  **83 — Linux**.  
A partição de boot do sistema deve ser do tipo:  **EF — FAT (FAT/12/16/32)**.  
A partição de swap deve ser do tipo:  **82 — Linux swap / Solaris**.

Selecione a partição de boot, e digite a letra:  **B**  para marcar a partição como bootável

Após terminar, entre na opção  **Write**  do cfdisk e escreva  **yes**.

Entre na opção  **Quit**  para sair do cfdisk.

Use comando  **blkid**  para visualizar a lista de partições.

## 5.4- Formate as partições recém criadas

Agora precisamos escolher o formato de cada partição

5.4.1- Sistema

A partição / do sistema aceita vários formatos de partição, escolha ext4, btrfs ou o que preferir. No meu caso vou usar  **btrfs**, portanto o comando será:

# mkfs.btrfs /dev/sda1 (exemplo)

Se fosse ext4 o comando seria:

# mkfs.ext4 /dev/sda1

5.4.2- Boot

A partição de boot do sistema deve ser do tipo FAT32, de preferencia, para formatar essa partição como fat32 use o comando:

# mkfs.fat -F 32 /dev/sda2 (exemplo)

5.4.3- Swap

Quanto a partição de swap, use o comando:

# mkswap /dev/sda3 (exemplo)

# 6- Monte as partições

Agora que todas as partições foram criadas e formatadas, monte elas nos locais especificados.

## 6.1- Partição do sistema:

# mount /dev/sda1 /mnt

Essa parte não é obrigatória, mas se você pretende usar o timeshift e a partição btrfs para o sistema, precisaremos criar um novo subvolume, desmontar a partição do sistema depois montar o subvolume como a raiz. Eins os comandos:

# btrfs subvolume create /mnt/@  
# umount /mnt  
# mount /dev/sda1 -o subvol=@ /mnt

Agora sim podemos continuar montando as outras partições, a próxima é a de boot.

## 6.2- Partição de boot:

# mount --mkdir  /dev/sda2 /mnt/boot

# 7- Instalando o sistema

Vamos usar o pacstrap para instalar o sistema, use o comando:

# pacstrap -K /mnt base linux linux-firmware

Use o comando abaixo para gerar o arquivo  **fstab**:

# genfstab -U /mnt >> /mnt/etc/fstab

# 8- Configurando o sistema

Use o comando abaixo para acessar o sistema, e começar a configura-lo.

# arch-chroot /mnt

## 8.1- Fuso horário

Use o comando

# ln -sf /usr/share/zoneinfo/Região/Cidade /etc/localtime

> _Exemplo:  
> # ln -sf /usr/share/zoneinfo/America/São_Paulo /etc/localtime_

Crie o arquivo /etc/adjtime usando o comando:

# hwclock --systohc

## 8.2- Localização

Usando o nano, edite o arquivo /etc/locale.gen e descomente a linha  **pt_BR.UTF-8 UTF-8**

# nano /etc/locale.gen

Crie um novo arquivo /etc/locale.conf

# nano /etc/locale.conf

Dentro desse arquivo deve ter esse conteúdo:

> _LANG=pt_BR.UTF-8_

Crie um novo arquivo /etc/vconsole.conf

# nano /etc/vconsole.conf

Dentro desse arquivo deve ter esse conteúdo:

> _KEYMAP=br-abnt_

Após isso use o comando:

# locale-gen

## 8.3- Configuração de rede

Crie um novo arquivo /etc/hostname

# nano /etc/hostname

Nesse arquivo coloque o nome do hostname, exemplo:

> _Archlinux_

Provavelmente estará faltando o gerenciador de redes no sistema, sem ele você não vai conseguir conexão com a internet, como eu uso DHCP, é necessário instalar esse pacote no sistema.

Use o comando:

# pacman -S dhcpcd

Além disso é necessário habilitar o inicio automatico da conexão DHCP, para isso use o comando:

# systemctl enable dhcpcd

## 8.4- Criar o initramfs (opcional)

Cria-lo pode não ser necessário pois o mkinitcpio já é criado com o pacstap durante a instalação, mas se você editou esse arquivo para alguma finalidade, pode ser necessário recriar a imagem do initramfs.

# mkinitcpio -P

## 8.5- Senha do root

Crie uma senha para o usuário root com o comando:

# passwd

## 8.6- Instalar Bootloader

Agora falta instalar o bootloader, é ele quem vai fazer o seu sistema dar boot. Vamos instalar o mais popular bootloader, use o comando abaixo para instalar o grub e o efibootmgr

# sudo pacman -S grub efibootmgr

Agora vamos instalar o bootloader na partição de boot do sistema:

# grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=ArchLinux

Caso tenha escolhido o modo BIOS

# grub-install --target=i386-pc /dev/sdX (selecione o disco, não a partição)

Após isso use o comando abaixo para criar o grub.cfg:

# grub-mkconfig -o /boot/grub/grub.cfg

**Reinicie o PC**.

# Pós instalação

A parte mais chata já foi superada, agora que o sistema foi instalado e está dando boot, vamos precisar instalar os drivers de vídeos, a interface gráfica, adicionar usuários, etc.

# 1- Adicionando o usuário

Até agora só temos o usuário root, precisamos adicionar o primeiro usuário comum para o sistema, use o comando para adicionar um novo usuário:

# useradd -m marcos

Agora vamos configurar a senha desse usuário:

# passwd marcos

Depois escolha uma senha para esse usuário.

# 2- Habilitando o comando sudo para o usuário

Agora vamos habilitar a função  **sudo**, para que esse usuário use o comando sudo para conseguir permissão de root para modificar o sistema, etc.

Primeiro precisamos instalar o pacote, use o comando:

# pacman -S sudo

Use o comando

# nano /etc/sudoers

Nesse arquivo desca até o final da página e você vai encontrar a linha:

root ALL=(ALL:ALL) ALL

Abaixo dessa linha coloque o nome do usuário novo e copie o rastante da linha, ficando assim:

root ALL=(ALL:ALL) ALL  
marcos ALL=(ALL:ALL) ALL

Depois salve o arquivo.

# Acabamos só que não

A parte mais dificil ja passou, agora cabe a você continuar a partir daqui, se baseie nos artigos do site do archlinux ou nos foruns da comunidade. A partir daqui é só instalar os drivers da placa de vídeo, a interface desktop e os seus pacotes.
