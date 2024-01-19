---
title: Como resolver o erro 0x80070643 da atualização KB5034232 do Windows 10
date: 2024-01-19
author: M4rQu1Nh0S
tags: [windows 11, windows update]
subtitle: Saiba como resolver este erro do Windows Update
categories: [windows 11]
comments: true
#cover-img: 
thumbnail-img: https://marcosfs93.github.io/assets/img/posts/winre/img1.png
share-img: https://marcosfs93.github.io/assets/img/posts/winre/img1.png
layout: post
---
Após fazer um upgrade no PC eu aproveitei e reinstalei o Windows 10, e para deixar o sistema redondo eu optei por deixar o sistema atualizar por completo primeiro, e em seguida instalar e configurar meus aplicativos.

Porém por algum motivo o Windows Update dava o erro 0x80070643, no meu caso este erro estava acontecendo na atualização KB5034232.

Essa atualização serve para atualizar o sistema de recuperação do Windows, porém o sistema precisa atender a alguns requisitos, caso contrário a atualização vai falar. Isso pode acontecer se você instalou uma versão não oficial do sistema ou por métodos alternativos.

Caso não saibam, é possivel instalar o Windows de outro jeito via WinNTSetup. No site e no youtube temos um guia ensinando isso, caso você não esteja conseguindo instalar o Windows normalmente: https://marcosfs93.github.io/2023-07-02-metodo-alternativo-instalar-windows/

Enfim, após investigar o problema eu descobri que era necessário fazer uma adequação manual na partição que contem o sistema de recuperação do Windows, que é atualizado nesse pacote. Hoje estou aqui trazer o procedimento que usei para resolver o problema.

## Como resolver o problema
1- Vá no menu iniciar, digite cmd e abra-o como **Administrador**

2- Use o comando `reagentc /info` para exibir as informações do WinRE.
Se o recurso estiver instalado, as informações como o local de instalação vão aparecer.

<p align='center'><img alt='Checando status do WinRE' src="https://marcosfs93.github.io/assets/img/posts/winre/img1.png"/></p>

3- Vamos desativar o WinRE temporariamente, use o comando `reagentc /disable`

A partir daqui vamos ter duas situações no sistema, ou o sistema ele já tem uma partição do WinRE ou o sistema não vai ter essa partição. Com base nisso siga os procedimentos baseado na situação da sua máquina.

Primeiro vamos verificar se o sistema tem ou não a partição:

1- Abra o CMD como Administrador
2- Use o comando `diskpart`
3- Use o comando `listdisk`
4- Use o comando `select disk` e depois o numero de disco do sistema
5- Use o comando `list partition` para mostrar as partições do disco.

O comando vai mostrar várias partições, precisamos saber qual delas é a do WinRE

6- Use o comando `detail partition` e o numero de cada partição até encontrar a partição chamada **Windows RE** conforme a imagem abaixo:

<p align='center'><img alt='Visualizando os detalhes da partição' src="https://marcosfs93.github.io/assets/img/posts/winre/img2.png"/></p>

### Caso o sistema já tenha a partição
Basicamente vamos apagar e criar uma nova partição novamente.

1- Use o comando `diskpart`
2- Use o comando `select disk` e depois o numero de disco do sistema
3- Use o comando `select partition` e o numero da partição do WinRE
4- Use o comando `delete partition override`

5- Agora vamos recriar a partição do WinRE, mas antes verifique se o sistema está instalado em um disco em formato GPT ou MBR.

Basicamente ao usar o comando `list disk` vai haver um asterisco (*) que vai indicar se o disco está em GPT, se tiver asterisco no lado do disco é GPT, e se não haver asterisco o disco é MBR.

Se o disco estiver em GPT, o comando será:
`create partition primary id=de94bba4-06d1-4d40-a16a-bfd50179d6ac`
e depois:
`gpt attributes =0x8000000000000001`

Se o disco estiver em MBR, o comando será:
`create partition primary id=27`

6- Agora vamos formatar a partição, use o comando:
`format quick fs=ntfs label=”Windows RE tools”`

7- Depois disso use o comando `reagentc /enable` e reinicie o PC, após iniciar tente atualizar o Windows novamente.

### Caso o sistema não tenha a partição:
Provavelmente você terá que reduzir a partição do sistema para permitir a criação da nova partição do WinRE.

1- Use o comando `diskpart`
2- Use o comando `select disk` e depois o numero de disco do sistema
3- Use o comando `select partition` e o numero da partição do sistema
4- Use o comando `shrink desired=250 minimum=250` para reduzir o tamanho da partição do sistema.
5- Agora vamos recriar a partição do WinRE, mas antes verifique se o sistema está instalado em um disco em formato GPT ou MBR.

Basicamente ao usar o comando `list disk` vai haver um asterisco (*) que vai indicar se o disco está em GPT, se tiver asterisco no lado do disco é GPT, e se não haver asterisco o disco é MBR.

Se o disco estiver em GPT, o comando será:
`create partition primary id=de94bba4-06d1-4d40-a16a-bfd50179d6ac`
e depois:
`gpt attributes =0x8000000000000001`

Se o disco estiver em MBR, o comando será:
`create partition primary id=27`

6- Agora vamos formatar a partição, use o comando:
`format quick fs=ntfs label=”Windows RE tools”`

7- Depois disso use o comando `reagentc /enable` e reinicie o PC, após iniciar tente atualizar o Windows novamente.

## Conclusão
Praticamente é isso, para resolver o problema nós precisamos alterar a partição do WinRE manualmente. Depois de feito os procedimentos e reiniciar a máquina você será capaz de atualizar o Windows normalmente, assim como eu consegui.

Espero que tenha sido util, caso tenha duvidas não deixe de usar os comentários, fui!

#### Referencias:
- https://support.microsoft.com/pt-br/topic/kb5028997-instru%C3%A7%C3%B5es-para-redimensionar-manualmente-sua-parti%C3%A7%C3%A3o-para-instalar-a-atualiza%C3%A7%C3%A3o-do-winre-400faa27-9343-461c-ada9-24c8229763bf