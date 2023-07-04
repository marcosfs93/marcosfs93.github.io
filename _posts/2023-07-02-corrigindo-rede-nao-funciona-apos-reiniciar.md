---
title: Corrigindo o problema de rede que não funciona ao reiniciar o Linux
date: 2023-07-02
author: M4rQu1Nh0S
tags: [rede, não funciona, após, reiniciar, linux]
subtitle: Saiba como fazer para corrigir o problema
categories: [dicas e tutoriais, linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*RM3u9CIlhfOW2YpF.png
share-img: https://cdn-images-1.medium.com/max/800/0*RM3u9CIlhfOW2YpF.png
layout: post
---

<p align='center'><img alt='logo do linux e da realtek r8168' src="https://cdn-images-1.medium.com/max/800/0*RM3u9CIlhfOW2YpF.png"/></p>
Assim como já aconteceu comigo no Windows, o meu driver de rede desaparecia ao reiniciar o sistema e reaparecia ao reiniciar novamente, um problema que vai e volta cada vez que o PC é reiniciado pelo sistema.

Hoje eu vou ensinar a como resolver esse problema no Linux, a solução é quase igual a do Windows bastando trocar o “driver” de rede por um outro sem esse problema, mas como sabemos o Linux não trabalha com drivers, e sim com módulos de kernel.

## Um problema já conhecido no Windows
Se você usa Linux e tem uma placa de rede realtek, é quase certo que o modulo que está sendo usado pelo sistema é o **r8169**, embora seja um módulo abrangente que funciona com várias placas de rede da realtek, a minha em especifico fica com esse problema de sumir ao reiniciar o sistema.

Depois de pesquisar muito e até pedir ajuda em fóruns, eu consegui resolver o problema instalando o módulo **r8168** que não faz parte do kernel do Linux, em outras palavras é um módulo a parte e disponibilizado diretamente pela realtek.

## Compilando e instalando o módulo r8168
Infelizmente por ser um módulo a parte, nós temos que recompilar o kernel para poder instalar o módulo r8168, dito isso, precisamos baixar o módulo r8168 e também ter o código fonte do kernel no sistema.

O processo de instalação é bem simples na verdade, basta baixar o pacote e rodar o comando **./autoinstall.sh** via terminal para que a compilação comece.

Você pode [baixar o r8168 através do repositório do mtorromeo](https://github.com/mtorromeo/r8168) no github, pelo visto esse repositório é um espelho do pacote disponibilizado no site da realmente, ou você pode baixar o r8168 através do meu repositório.

No meu repositório, o driver r8168 também funciona com o meu dispositivo, o de ID **10ec:8136**

03:00.0 Ethernet controller [0200]: Realtek Semiconductor Co., Ltd. RTL810xE PCI Express Fast Ethernet controller [10ec:8136] (rev 05)

Se o seu dispositivo tiver o mesmo ID que o meu, então eu recomendo baixar o pacote r8168 do meu repositório.

## Instalando possiveis dependencias
Antes de compilar o módulo r8168 é necessário ter instalado em sua distribuição ao menos dois desses pacotes:

	build-essential linux-headers

Os nomes desses pacotes variam com a distribuição. Por exemplo no ubuntu/debian podemos instalar eles com o comando:

	$ sudo apt install build-essentials linux-headers

## Baixando o pacote do repositório:
Vamos fazer tudo pelo **terminal,** abra ele e rode o seguinte comando:

	$ cd ~/

_Para entrar na sua pasta home_

	$ wget -c https://github.com/M4rQu1Nh0S/r8168/archive/refs/tags/8.050.00m.tar.gz

_Para baixar o pacote com o wget_

	$ tar xvzf r8168-8.050.00m.tar.gz

_Para extrair o conteudo do pacote_

	$ cd r8168-8.050.00m

_Para entrar na pasta extraída do pacote_

	$ sudo su

_Para entrar no modo root_

	# ./autorun.sh

_Para rodar o compilador do módulo_

Pronto, isso vai compilar o r8168, remover o r8169 e reativar a sua placa de rede com o novo módulo, rode o comando abaixo para ver se o módulo está ativo:

	$ lsmod | grep r8168
	r8168

Ao rodar o comando, a palavra **r8168** deverá aparecer logo abaixo do comando, se isso não acontecer é porque o módulo ainda não está funcionando, independente do resultado reinicie o seu computador ao menos duas vezes e depois disso tente rodar o comando acima novamente, ou se quiser, reinicie outra vez sua maquina para conferir se o driver está funcionando ou não.

Isso é tudo, espero que isso tenha sido útil.

## Referencias:
[https://github.com/M4rQu1Nh0S/r8168](https://github.com/M4rQu1Nh0S/r8168)
[https://github.com/mtorromeo/r8168](https://github.com/mtorromeo/r8168)

