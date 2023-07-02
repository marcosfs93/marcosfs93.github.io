---
title: Como dar boot manualmente e recuperar o GRUB EFI no Linux
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, dar, boot, manualmente, recuperar, grub, efi, linux]
subtitle: Saiba como dar boot manual e restaurar o carregador do sistema
category: [Dicas e tutoriais, Linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*oeZgTQmlUkHEhAlo.jpg
share-img: https://cdn-images-1.medium.com/max/800/0*oeZgTQmlUkHEhAlo.jpg
layout: post
---

![](https://cdn-images-1.medium.com/max/800/0*oeZgTQmlUkHEhAlo.jpg)<br/>
Um problema que me fez perder horas e horas até encontrar a solução, hoje vamos aprender a como fazer o boot manualmente pelo GRUB e também a como recuperar o boot EFI do Linux.

Pode acontecer de você fazer alterações no sistema que podem quebrar o boot, seja uma alteração direta no inicializador do sistema, das entradas do sistema UEFI ou simplesmente alguma alteração indireta no GRUB.

Esse tutorial está separado em 3 partes, na parte 1 vamos aprender a como fazer o boot manualmente pelo grub rascue, na parte 2 vamos aprender a reparar o inicializador do grub para que o sistema volte a dar boot automaticamente quando o PC iniciar e por fim a parte 3, nessa parte vamos aprender a recriar a partição EFI do zero e os arquivos EFI de inicialização.

**Conteúdo**

- 1. [Conseguindo dar boot pelo Grub Rascue](#)
- 1.1. [Procurando o disco onde se encontra o sistema](#)
- 1.2. [Iniciando o boot manualmente](#)
- 2. [Restaurando o carregador de boot do sistema](#)
- 2.1. [Encontrando a partição EFI](#)
- 2.2. [Encontrando os arquivos de boot .efi](#)
- 3. [O que fazer se a partição EFI foi apagada](#)
- 3.1. [Como recriar a partição EFI](#)
- 3.1.1. [Se quiser excluir a partição EFI atual](#)
- 3.1.2. [Para criar uma nova partição EFI](#)
- 3.2. [Registrando a nova partição EFI no Fstab](#)
- 3.2.1. [Encontrando a UUID da partição EFI](#)
- 3.2.2. [Atualizando o fstab](#)
- 3.3. [Instalando o GRUB na nova partição EFI](#)
- [Considerações finais](#)
- [Referencias](#)

## 1- Conseguindo dar boot pelo Grub Rascue

![](https://cdn-images-1.medium.com/max/800/0*OMdl3QCbDpMahwB3.jpg)

A primeira e única coisa que você verá quando o boot da sua distro está com problemas, é essa tela aí em cima.

Quando chegar nessa parte, nós devemos tentar dar boot no sistema **manualmente** e pra isso vamos precisar saber quais os discos que estão disponíveis.

### 1.1. Procurando o disco onde se encontra o sistema:

Vamos começar, use o comando **ls** para listar os discos:

> _grub>_ **_ls_**

Fazendo isso vai aparecer uma mensagem, vai ser mais ou menos assim:

> **_(hd0) (hd1) (hd1,gpt1) (hd1,gpt2) (hd2) (hd2,gpt1) (hd2,gpt2) (hd3,msdos1) (hd3,msdos2)_**

Com o comando **ls** nós podemos visualizar o interior dos discos disponíveis, com ele precisamos descobrir em qual dos discos disponíveis está o Linux instalado.

Na pratica vamos usar o comando dessa forma:

> _grub>_ **_ls (hd1,1)/_**

Após isso devemos procurar pela pasta **/boot**, ela está presente na raiz da partição onde está o sistema, junto com as pastas outras pastas da raiz, exemplo:

> _grub>_ **_ls (hd1,2)/_**
>
> _/bin_ **_/boot_** _/dev /efi /etc /grub /home /lib /lib32 /lib64 /libx32 /lost+found /media /mnt /opt /proc /program_files /root /run /sbin /snap /srv /swapfile /sys /tmp /usr /var_

_Dica: Ao invés de usar o comando_ **_ls (hd1,gpt2)_** _você pode simplesmente usar no lugar o comando_ **_ls (hd1,2)_**_, não é necessário incluir os nomes_ **_gpt_** _e nem_ **_msdos_** _entre os números._

Se você tiver mais de uma distro instalada no PC, olhar só a raiz não vai ajudar, precisamos saber se essa raiz que estamos vendo agora é da distro que você precisa recuperar o boot ou não.

Pra isso vamos usar o comando **cat** e puxar as informações do arquivo **/etc/issue**, exemplo:

> _grub> ls (hd1,2)/etc/issue_

Resultado:

> _grub> cat (hd1,2)/etc/issue
> _**_Ubuntu 22.04 LTS \n \l_**

Enfim, após encontrar o disco e a partição certa, vamos continuar dando o boot do sistema.

### 1.2 Iniciando o boot manualmente

Essa parte é bem simples, após encontrar o disco do sistema use os comandos abaixo:

> _grub> set prefix=_**_(hd1,2)_**_/boot/grub_
>
> _grub> insmod normal_
>
> _grub> normal_

Depois disso o menu do sistema vai aparecer, com isso o sistema vai iniciar.

## 2- Restaurando o carregador de boot do sistema
Depois de ter conseguido dar boot manualmente no sistema, precisamos recuperar o carregador do grub, porque se você reiniciar o PC sem ter resolvido isso, o grub rascue vai te dar um oi de novo 😉.

Alias, essa foi a parte que mais me travou porque eu tentei várias dicas que não deram certo para resolver essa parte.

Vamos continuar, precisaremos instalar o pacote do **efibootmgr** que vai ser usado para recuperar as entradas de boot.

Para Ubuntu/Debian e suas distros baseadas:

	$ sudo apt install efibootmgr

### 2.1 Encontrando a partição EFI
A partição EFI é separada da partição do sistema, e por isso precisamos cuidadosamente saber qual é a partição e aplicar as mudanças no carregador de boot para ele funcione sem problemas.

Use o comando **lsblk** para listar os discos e os pontos de montagem.

Exemplo com resultado:

![](https://cdn-images-1.medium.com/max/800/0*ngHEcPM8LhuRBq2u.jpg)

Com isso nós já encontramos a partição EFI, no meu caso a partição é **/dev/sdb1** que já foi montada no local **/boot/efi**.

Se a partição EFI não está montada no seu sistema, monte-a.

Use o comando a baixo para montar a partição EFI em /boot/efi

	$ sudo mount /dev/sdb<numero> /home/boot

Para saber qual é a partição EFI, basta se orientar pelo tamanho da partição, formato (FAT32,vfat).

Use o comando abaixo para ter uma lista mais detalhada das partições disponiveis:

	$ lsblk -o name,path,size,fstype,uuid,mountpoint | grep 'sd\|vfat'

### 2.2 Encontrando os arquivos de boot .efi

O objetivo agora é encontrar o local onde se encontrar os arquivos de boot do sistema.

----------

Se você não tem mais a partição EFI ou os arquivos foram removidos, [clique aqui](https://marcosfs93.blogspot.com/2023/03/como-dar-boot-manualmente-e-recuperar-o.html#user-content-312---para-criar-uma-nova-parti%C3%A7%C3%A3o-efi) para pular para a parte 3 onde eu ensino a recriar a partição EFI e os arquivos .EFI.

----------

Depois de ter encontrado a partição EFI, que no meu caso ela já está montada no /boot/efi/, vamos precisar encontrar o arquivo **grubx64.efi**, que é carregado ao iniciar o PC.

Entre no diretório **/boot/efi** com o comando **cd**:

	$ cd /boot/efi

Agora vamos usar o comando **tree**, ele vai listar o restante do conteúdo a partir daqui.

	$ tree -L 3

**Resultado do comando:**

![](https://cdn-images-1.medium.com/max/800/0*c4Vo-gRBRC1zecki.jpg)

Sendo assim o caminho completo é:

> _/EFI/BOOT/_**_grubx64.efi_**

Sabendo disso o comando abaixo será esse, com base nas informações obtidas:

	$ sudo efibootmgr --create --disk /dev/sdb --part 1 --loader /EFI/BOOT/grubx64.efi --label "Ubuntu 22.04 LTS" --verbose

_Observações: o trecho_ **_“ — disk /dev/sdb — part 1*_**_”* é uma referencia ao disco_ **_/dev/sdb1_** _que é justamente a partição EFI, que estava montada em_ **_/boot/efi_**_._

**Resultado:**

![](https://cdn-images-1.medium.com/max/800/0*IHJypNGdl8D_lcrd.jpg)

Pronto, agora é só reiniciar o PC e testar.

## 3- O que fazer se a partição EFI foi apagada:
A parte 2 desse tutorial não ajuda quem teve a partição EFI apagada ou que não tem mais os arquivos do grub.

Nessa parte nós vamos aprender a recriar a partição EFI e os arquivos de boot do sistema.

Recomendo que façamos isso usando o **gparted**.

Esse utilitário pode ser baixado com o comando **“sudo apt install gparted”** em distribuições baseadas no Ubuntu/Debian.

Você também pode encontrar ele na Loja de Aplicativos da sua distro.

### 3.1 Como recriar a partição EFI:

#### 3.1.1 Se quiser excluir a partição EFI atual:
Se a partição EFI estiver corrompida e você quer criar uma nova, siga os procedimentos abaixo:

Abra o **gparted**.

1- Primeiro selecione o disco a ser gerenciado, no meu caso é o **/dev/sdb**.

2- Na lista de partições, selecione a partição EFI que deve ser excluída e clique com o botão direito sobre ela, para abrir o menu de ação.

3- Clique em **Delete**.

Imagem:

![](https://cdn-images-1.medium.com/max/800/0*cFcFrXZqbRpf_ela.jpg)

Após excluir a partição, clique em **Apply**.

#### 3.1.2 — Para criar uma nova partição EFI

Criando uma nova partição FAT32:

1- Clique na partição **unallocated**.

2- Clique em **New**.

Imagem:

![](https://cdn-images-1.medium.com/max/800/0*_h-R_50vH4Rdjo2m.jpg)

3- Clique na caixa de seleção em **file system**

4- Selecione o formato **fat32** e e clique em **“+ Add”**.

Com isso já conseguimos criar a nova partição EFI para o sistema, agora só falta marcar as flags **boot** e **esp**.

5- Selecione a partição FAT32 da lista de partições e clique com o botão direito do mouse.

6- Selecione a opção **Manage Flags**.

![](https://cdn-images-1.medium.com/max/800/0*Pcz1UfrjPRYj7J7v.jpg)

Nessa parta você só precisa marcar as flags, selecione as **flags boot** e **esp** e clique em Close para fechar essa janela.

![](https://cdn-images-1.medium.com/max/800/0*egH-p7oKi_pFcDbY.jpg)

Pronto, sua partição EFI já foi criada.

### 3.2 — Registrando a nova partição EFI no Fstab
> _No Linux todas as partições usadas pelo sistema devem ser listadas em_ [_/etc/fstab_](https://pt.wikipedia.org/wiki/Fstab)_. Esse arquivo contém os pontos de montagem das partições (onde elas se encontram na estrutura do sistema de arquivos), como elas devem ser montadas, quais opções especiais (automáticas ou não, se os usuários podem montá-las ou não, etc.) “Citação:_ [_Gentoo Linux — Wiki_](https://wiki.gentoo.org/wiki/Handbook:Parts/Installation/System/pt-br)_”_

A partição EFI é uma partição que também deve estar presente no fstab junto com as outras, nele a partição EFI é configurada para ser montada em **/boot/efi** automaticamente.

No **modo BIOS** as partições são listadas no fstab através do bloco de arquivos presentes no diretório /dev, o arquivo fstab segue esse padrão:

Exemplo

> **_/dev/sda1_** _/ ext4 defaults 0 1
> /dev/sda2 /home ext4 defaults 0 0_

Já em **modo UEFI** as partições são listadas no fstab através de UU**ID**, o arquivo fstab segue esse padrão:

> **_UUID=4227846c-18e8–4c51-b827-bc2838fbb4fe_** _/ ext4 defaults 0 1
> UUID=8ecc4ffe-a3b5–4261–848c-ffc01eda093f /home ext4 defaults 0 0_

As UUID são únicas, quando uma partição é deletada e recriada, **um novo UUID é gerado**.

Sendo assim, a partição EFI que nós criamos anteriormente tem uma UUID diferente da partição anterior, e que estava registrada no fstab.

Sabendo disso nós precisamos abrir o arquivo fstab e atualizar a UUID da partição EFI.

#### 3.2.1 Encontrando a UUID da partição EFI
Rode o comando abaixo:

	$ lsblk -o name,path,size,fstype,uuid,mountpoint | grep 'sd\|vfat'

![](https://cdn-images-1.medium.com/max/800/0*j6-4scibrS5P4ulD.jpg)

Esse comando vai listar de discos que começam com **‘/dev/sd’** e que estejam no format **‘vfat’**.

Essa lista vai conter as informações sobre nome, tamanho, formato, e principalmente o UUID das partições, nessa lista devemos descobrir o UUID da partição EFI que nós criamos.

#### 3.2.2 Atualizando o fstab
Após descobrir a UUID da nova partição basta abrir o arquivo fstab.

Roda o comando abaixo:

	$ sudo nano /etc/fstab

![](https://cdn-images-1.medium.com/max/800/0*o2-ZXsWGdsvTc0j6.jpg)

Basta substituir a UUID ao lado do /boot/efi.

Depois disso aperte **Ctrl + X** para fechar e aperte **Y** para salvar.

### 3.3. Instalando o GRUB na nova partição EFI:
Após atualizar o fstab, vamos agora montar a partição EFI no local /boot/efi e instalar o GRUB nela.

Volte ao terminal e use o comando a seguir para montar a partição EFI no local /boot/efi:

	$ sudo mount /boot/efi

Use o comando abaixo para recriar os arquivos do grub da partição EFI:

	$ sudo grub-install --efi-directory=/boot/efi

Use o comando abaixo que vai atualizar o grub do sistema

	$ sudo update-grub

Pronto, chegamos ao fim da parte 3, nessa parte fomos capazes de criar uma nova partição de boot, de obter a nova UUID dessa partição para atualizar o arquivo fstab e recriar os arquivos de boot, principalmente os arquivos do grub.

----------

Se você tinha pulado a parte 2.2 para recuperar a partição EFI, [clique aqui](https://marcosfs93.blogspot.com/2023/03/como-dar-boot-manualmente-e-recuperar-o.html#user-content-22-encontrando-os-arquivos-de-boot-efi) para continuar de onde parou, porque na parte 2 eu ensinei a como atualizar o carregador de boot do sistema, que precisa dos arquivos EFI da partição EFI.

----------

## Considerações finais:
Esse é foi um dos tutoriais mais complexos e trabalhosos de se produzir nesse blog, espero que ele tenha sido util e tenha te ajudado a resolver o problema.

Se você descobriu algum erro nesse tutorial, comente, sua colaboração será muito util e poderá ajudar mais pessoas a resolver esse problema.

## Referencias:
- [https://askubuntu.com/questions/831216/how-can-i-reinstall-grub-to-the-efi-partition](https://askubuntu.com/questions/831216/how-can-i-reinstall-grub-to-the-efi-partition)
- [https://askubuntu.com/questions/1394708/accidentally-deleted-efi-partition-system-is-still-running](https://askubuntu.com/questions/1394708/accidentally-deleted-efi-partition-system-is-still-running)
- [https://manjariando.com.br/recuperar-grub-efi/](https://manjariando.com.br/recuperar-grub-efi/)
- [https://wiki.gentoo.org/wiki/Efibootmgr](https://wiki.gentoo.org/wiki/Efibootmgr)

