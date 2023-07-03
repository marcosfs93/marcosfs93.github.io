---
title: Como restaurar o Windows Boot Manager do Windows 10
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, recuperar, restaurar, boot, manager, windows 10]
subtitle: Aprenda a reparar o carregador de boot do sistema
category: [Dicas e tutoriais, Windows]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*ypiGhPzvghyDSeXt.jpg
share-img: https://cdn-images-1.medium.com/max/800/0*ypiGhPzvghyDSeXt.jpg
layout: post
---

<p align='center'><img alt='Tela azul do Windows após erro no boot' src="https://cdn-images-1.medium.com/max/800/0*ypiGhPzvghyDSeXt.jpg"/></p>
Não lembro quantas vezes eu já me deparei com esse tipo de erro, geralmente é algo que vem a acontecer durante os processos de dual boot com outro sistema operacional, na ultima vez que isso aconteceu comigo foi ao manter o Windows em um SSD em GPT e usar outro sistema em outro SSD em MBR.

Eu não sei se é conflito da BIOS com o UEFI mas o **Windows Boot Manager**, que é o responsável por iniciar o boot do Windows, desapareceu da lista de boot que aparece ao ligar o PC após passar alguns dias usando outro sistema.

Enfim, hoje quero compartilhar os procedimentos para restaurar o boot do Windows, eu pude restaurar o boot do Windows usando **Discos de recuperação** como o excelente Hiren’s BootCD PE.

**Conteúdo**
-  [Como restaurar o boot do Windows](#como-restaurar-o-boot-do-windows)
-  [- Como recuperar o Windows com o Hiren’s BootCD](#como-recuperar-o-windows-com-o-hirens-bootcd)
-  [- Restaurando o Windows via CMD](#restaurando-o-windows-via-cmd)
-  [Dicas](#dicas)
-  [Considerações finais](#considerações-finais)

## Como restaurar o boot do Windows
O problema de boot do Windows pode ter dois cenários, um em que você é capaz de usar o Prompt de comando do Windows, e o outro não. Nesse segundo caso é necessário usar ferramentas alternativas ou até mesmo o disco de instalação do Windows.

Considerando que você não tenha o mesmo disco que usou pra instalar o seu windows, devemos usar discos de recuperação mesmo, de terceiros, aqui eu recomendo o Hiren’s BootCD PE ou abreviando: HBCD

## Como recuperar o Windows com o Hiren’s BootCD
Primeiro você precisa gravar o HBCD em alguma midia, seja pen drive ou CD/DVD, baixe o HBCD nesse link a seguir:

**Para fazer DVD bootável do HBCD, baixe a ISO aqui:**
[https://www.hirensbootcd.org/download/](https://www.hirensbootcd.org/download/)

**Para fazer um pendrive de boot do HBCD, baixe a ferramenta aqui:**
[https://www.hirensbootcd.org/usb-booting/](https://www.hirensbootcd.org/usb-booting/)

Segundo, com o HBCD já disponivel para recuperação do sistema, reinicie o seu PC e dê boot na midia do HBCD.

Como você verá após iniciar o HBCD, perceberá que o HBCD nada mais é do que uma LiveCD do Windows com várias ferramentas uteis, isso é muito bom pois nada melhor do que um outro Windows, seja LiveCD ou não, para recuperar um PC com outro Windows.

## Restaurando o Windows via CMD
Enfim, após iniciar o HBCD abra o seu prompt de comando e siga as instruções:

1- Vá no menu iniciar e simplesmente digite:

	cmd

2- Use o comando abaixo:

	diskpart

3- Use o comando abaixo:

	sel disk 0

4- Use o comando abaixo:

	list vol

5- Nessa parte vamos precisar escolher na lista que apareceu no CMD a partição onde está o Windows Boot Manager, geralmente o Windows Boot Manager fica em uma partição FAT32 com cerca de 100Mbs de tamanho.

Assim que você identificar o numero do volume relacionado a partição de boot do Windows, coloque o numero do volume no comando abaixo:

	sel vol <numero do volume>

Exemplo: sel vol 1

6- Além da partição de boot do Windows estar particionado em FAT32 e ter o tamanho do 100Mb, essa partição não tem uma letra de disco, precisamos atribuir uma letra para essa partição.

Escolha uma letra de unidade (que não esteja em uso) e coloque junto no comando abaixo:

	assign letter=Z:

**Nota:** a letra Z é um exemplo, escolha qualquer letra que não esteja em uso, mas se o J estiver disponível… use.

7- Use o comando abaixo:

	exit

8- Agora chegou a hora de recuperar efetivamente o boot do Windows, use os comandos abaixo para concluir a recuperação do boot.

	cd /d  Z:\EFI\Microsoft\Boot\

	bootrec /FixBoot

	bcdboot c:\Windows /l pt-br /s  Z:  /f ALL

Com isso terminamos, reinicie o seu PC e veja se o Windows está de volta.

## Dicas:

### “BFSVC Error: Could not open the BCD template store.Status=[c000000f]”
Esse erro pode aparecer no momento de executar o ultimo comando da lista acima, para resolver é só entrar no diretório “C:\Windows\system32”.

Para entrar no diretório use o comando:

	cd /d C:\Windows\system32

## Considerações finais
Pra ser sincero eu fiz esse tutorial para mim mesmo, existe diversos tutoriais sobre o assunto mas há muitos que não abordam a utilização de discos de recuperação, espero que essa dica tenha te ajudado.

