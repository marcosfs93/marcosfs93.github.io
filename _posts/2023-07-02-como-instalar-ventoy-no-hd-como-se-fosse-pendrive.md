---
title: Como instalar o Ventoy em um HD como se fosse um pendrive
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, instalar, ventoy, no hd, se fosse, invés, pendrive]
subtitle: Aprenda a instalar o ventoy no HD substituindo os pendrives
category: [Dicas e tutoriais]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*co4tQYQ1me_XTiKA.png
share-img: https://cdn-images-1.medium.com/max/800/0*co4tQYQ1me_XTiKA.png
layout: post
---

![](https://cdn-images-1.medium.com/max/800/0*co4tQYQ1me_XTiKA.png)<br/>
O Ventoy é um aplicativo diferente dos outros quando se fala de criar um pen drive bootável de um sistema operacional, com ele você simplesmente pode copiar e colar um arquivo .ISO diretamente no pen drive sem ter que ficar formatando.

Isso é bem diferente daquele outro processo de pegar um arquivo .ISO de um sistema operacional e grava-lo com um app gravador de imagem como o **Rufus**, pois pra cada ISO gravada no pen drive, uma formatação é exigida.

O conceito de multiboot ajudou a amenizar a necessidade de ficar formatando um pen drive e de ficar perdendo tempo gravando uma ISO de cada vez, com multiboot você gravar mais sistema de uma vez só.

Porém mesmo com multiboot você precisa de pen drive e precisa formata-lo, sem falar que dependendo da ferramenta de multiboot o processo pode ser um pouco complicado.

**Conteúdo**

- [- A maior vantagem Ventoy](#1b7f)
- 1[. Regras para instalar o Ventoy no HD](#2546)
- 1.2. [Não pode existir espaço livre antes da 1ª partição do HD](#0a3d)
- 1.3. [A 1ª partição deve usar o sistema NTFS ou sistemas EXT2/3/4](#b429)
- 1.4. [A 1ª partição deve ter espaço livre, para armazenas as ISOs](#6c1b)
- 2[. Como particionar o HD manualmente](#caf7)
- 3[. Como instalar o Ventoy no HD interno](#1fcd)
- 4[. Corrigindo problemas de escrita](#bd51)
- 4.1. [Para partições sem Windows instalado](#5c09)
- 4.2. [Para partições com o Windows instalado](#7efe)
- [- Considerações finais](#364d)
- [- Referencias](#c9a8)

## A maior vantagem Ventoy
Com o Ventoy você só formata o seu pen drive **uma única vez**, e você pode simplesmente copiar e colar um arquivo ou vários arquivos .ISO diretamente no pen drive, simples assim, sinônimo de facilidade, praticidade e que preserva a vida útil do dispositivo pois você evita de formata-lo.

Mas em todos os cenários acima, o pen drive se faz presente. Seria interessante se o Ventoy fizesse parte do HD nativamente, não é? Pois assim poderíamos aposentar o pen drive e usar o HD para dar boot em imagens de disco de sistema ou utilitário.

Hoje vamos aprender a como usar o HD interno no lugar do Pen drive para dar boot em imagens de disco.

Antes de começarmos é importante que você **tenha feito o backup do HD** que será usado, pois há riscos de perder os dados nesse processo.

## 1- Regras para instalar o Ventoy no HD
Em teoria o processo é simples, o Ventoy usa a 1ª e a 2ª partição do HD para funcionar, sendo que a primeira partição é usada para guardar os arquivos de imagem .ISO e a segunda partição é do boot EFI que é obrigatória em PCs com o UEFI.

![](https://cdn-images-1.medium.com/max/800/0*8dwa0PGRYSvvYWBn.png)

Além disso existe requisitos bem estritos para conseguir tornar o HD elegível para ter conseguir instalar o Ventoy, e elas são:

### 1.1- Não pode existir espaço livre antes da 1ª partição do HD
Não pode existir um espaço livre não particionado antes da 1ª partição no HD

Além disso existe uma limitação para os formatos MBR e GPT:

-   Partições MBR, havendo 4 partições que já existem no HD o Ventoy não poderá ser instalado em modo de não-destrução.
-   Partições GPT, havendo 128 partições que já no HD o Ventoy não poderá ser instalado em modo de não-destruição.

_O modo de não-destrução é um método de instalação do Ventoy que não vai apagar os dados das outras partições que existem no HD_.

### 1.2- A 1ª partição deve usar o sistema NTFS ou sistemas EXT2/3/4
De preferência NTFS, já que o Windows em si não reconhece certos sistemas de arquivos.

No caso do Linux, os pacotes abaixo precisam estar presentes, dependendo do formato escolhido para a 1ª partição:

-   Se for NTFS, o pacote **ntfs-3g** precisa ser instalado.
-   Se for EXT2/3/4, o pacote **e2fsprogs** precisa ser instalado.

Eu particularmente recomendo usar **exfat**, pois é um formato suportado em vários sistemas.

-   Para exFAT no linux, o pacote **exfat-utils** precisa ser instalado.

### 1.3- A 1ª partição deve ter espaço livre, para armazenas as ISOs.
A primeira partição é onde vai estar as .ISO dos sistemas, pense nela como o “pendrive interno”, eu por exemplo tenho 12GB de espaço nela.

## 2- Como particionar o HD manualmente
Agora que já foi explicado os requisitos, agora vamos informar como o HD deve ser particionado corretamente.

1 — Abra o **Gparted**, você pode usar outras ferramentas se quiser.

2 — Selecione o HD a ser particionado, meu caso será o **/dev/sdc**

3 — Apague todas as partições ou reduza o tamanho das partições existentes para que a parte inicial do HD seja reservada para as partições do Ventoy.

4 — Por exemplo a configuração das partições será essa, seguindo os requisitos que o Ventoy exige para ser instalado:

Exemplo:

![](https://cdn-images-1.medium.com/max/800/1*cAIgAw5musbJUhdbPKCLMA.jpeg)

A 1ª partição (**/dev/sdc1**) deve ter espaço livre, iniciando no 1º Mb do disco e em formato NTFS.

Quanto a partição **/dev/sdc2**, ela será usada como partição EFI do Ventoy

A 3ª partição é a minha partição pessoal, ela ou novas partições deveram começar a partir da partição **sdc3** em diante, pois as partições **sdc1** e **sdc2** devem ser reservadas para o Ventoy.

5- Nessa parte eu vou trocar o formato da partição para **exfat** e excluir a partição **sdc2**:

![](https://cdn-images-1.medium.com/max/800/1*FiFiZlUxZsYtIsLMDbHcpw.jpeg)

Essas modificações foram necessárias por dois motivos:

O formato **exfat** tem mais compatibilidade nos sistemas operacionais do que o formato NTFS, e a partição **/dev/sdc2** é refeita pelo script de instalação do ventoy.

Quem deve criar a partição 2 é o Ventoy e não o usuário, no caso o usuário deve apenas reservar um espaço livre de 32Mb entre a partição 1 e a partição 3.

_PS: Por alguma razão o GParted não tinha a opção de formatar a partição em_ **_exfat_**_, daí eu tive que usar o comando abaixo pra formatar de outro jeito:_

	$ sudo mkfs.exfat  -n "VENTOY HDD" /dev/sdc1

_Esse comando formata a partição em formato exfat e criar um nome para ela, no caso VENTOY HDD._

## 3- Como instalar o Ventoy no HD interno
Para instalar o Ventoy no HD, precisamos usar o script **Ventoy2Disk.sh** que está dentro da pasta do Ventoy.

1- Abra o terminal e vá no diretório do Ventoy

2 — Execute o comando abaixo **informando o HD correto**

	$ sudo sh Ventoy2Disk.sh -i -n  /dev/sdc

Você verá algo assim:

![](https://cdn-images-1.medium.com/max/800/1*LqTExy4kXKIeRNG5vceLWA.jpeg)

3- Pronto, o Ventoy já está instalado no HD e agora só precisamos **ativar as flags de boot** da partição efi, você só precisa deixar a partição igual a **/dev/sdc2** da imagem abaixo:

![](https://cdn-images-1.medium.com/max/800/1*-b7ar3oS1z4B4SrBFNGjRg.jpeg)

4- Reinicie o PC e faça o teste, no meu caso eu tive que apertar F11 pra selecionar o disco de boot e selecionei o HD com o Ventoy, rodou perfeitamente.

## 4- Corrigindo problemas de escrita
Pode acontecer da partição que contém os seus dados pessoais ficar em modo somente leitura, quando isso acontece você não será capaz de editar e criar qualquer arquivo dentro na tal partição.

### 4.1- Para partições sem Windows instalado
Se a sua partição é separada da partição do Windows, use um comando como esse para corrigir esse problema

Exemplo:

	$ sudo ntfsfix /dev/sdc3

Após esse comando reinicie o PC e relogue no Linux.

### 4.2- Para partições com o Windows instalado
Para partições que tem o Windows instalado a recomendação é desmontar a partição está em somente leitura e monta-la novamente sem essa restrição.

Você pode usar esse comando para tentar montar a partição de novo.

Exemplo:

	$ sudo umount /dev/sdZ4 (sdZ4 é o exemplo)
	$ sudo mkdir -p /media/HDD
	$ sudo mount /dev/**sdZ4** -t ntfs-3g -o permissions /media/HDD

## Considerações finais
Embora pareça complicado, instalar o Ventoy no HD não é algo tão dificil, originalmente o ventoy foi desenvolvido para ser usado com pen drives mas a forma como ele funciona nos permite explorar outras alternativas.

Depois disso você pode continuar usando o HD normalmente e quando precisar instalar outro sistema, é só colar a ISO do sistema na partição 1 e reiniciar.

O Ventoy constantemente recebe melhorias e tem novas versões lançadas, felizmente você consegue atualizar o Ventoy do HD sem ter que passar por tudo isso de novo bastando rodar o App, selecionar o disco e atualizar:

![](https://cdn-images-1.medium.com/max/800/1*6o51wDWCH8L8hb4AJsFbbg.jpeg)

É importante ter uma partição pequena só para as .ISO no Ventoy, pois no momento em que rodamos uma live cd de um sistema linux, a partição que contem a ISO fica ocupada e daí não teria como gerenciar outros arquivos dessa partição.

Caso queira colaborar com mais informações ou informar problemas, deixe seu comentário abaixo.

Como eu não vi ninguém ensinando a instalar o Ventoy usando um HD interno eu decidi encontrar uma forma de fazer isso e agora estou aqui compartilhando com vocês, espero ter ajudado. Até a próxima!

### Referencias:
-[https://www.ventoy.net/en/doc_disk_layout_gpt.html](https://www.ventoy.net/en/doc_disk_layout_gpt.html)
-[https://www.ventoy.net/en/doc_non_destructive.html](https://www.ventoy.net/en/doc_non_destructive.html)

