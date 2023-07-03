---
title: Como criar um atalho da barra vertical no Linux
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, criar, atalho, pipe, barra, vertical, linux]
subtitle: Aprenda a como criar um atalho para esse caractere
category: [Dicas e tutoriais, linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/1*bRKAyByI6YXvaSXAk5xiaA.png
share-img: https://cdn-images-1.medium.com/max/800/1*bRKAyByI6YXvaSXAk5xiaA.png
layout: post
---

Hoje vamos aprender a criar um atalho de símbolos para o teclado no Linux, principalmente no ambiente desktop KDE, em que o atalho Ctrl Shift U não funciona igual no GNOME.

Alguns dias atrás eu publiquei um artigo sobre “[Como adicionar símbolos que não tem no teclado](https://marcosfs93.github.io/2023-07-02-como-adicionar-simbolos-faltando-teclado/)” em que usamos o código de referencia dos símbolos com a tabela ASCII e Unicode.

Porém é inegável que ficar decorando código de símbolo é algo chato e nada intuitivo para usuários novos que estão migrando para o Linux.

Além disso naquele artigo ensinamos a usar o atalho Ctrl + Shift + U para inserir os símbolos, mas pra quem usa o KDE esse tipo de comando não funciona.

Sendo assim, eu estou aqui hoje para ensinar a como criar um atalho simples para inserir símbolos facilmente e que não tem no teclado.

Eu sou um exemplo de usuário que tem um teclado que não tem todos os atalhos de símbolos, principalmente a **barra invertida** `\` e **barra vertical** `|`.

Atualmente eu tenho esse teclado:

<p align='center'><img alt='Imagem de teclado gamer com iluminação' src="https://cdn-images-1.medium.com/max/800/1*bRKAyByI6YXvaSXAk5xiaA.png"/></p>

Observando com atenção você pode notar que a **barra invertida** `\` e **barra vertical** `|` está faltando nesse teclado, pelo menos olhando nas teclas dele.

**Conteúdo:**

1. [Visualizando o layout do teclado](#visualizando-o-layout-do-teclado)
2. [Como remapear uma tecla do teclado](#como-remapear-uma-tecla-do-teclado)
3. [Como descobrir o código de identificação de uma tecla](#como-descobrir-o-código-de-identificação-de-uma-tecla)
4. [Descobrindo o nome do símbolo para usar no xmodmap](#descobrindo-o-nome-do-símbolo-para-usar-no-xmodmap)
5. [Descobrindo o mapeamento atual da tecla](#descobrindo-o-mapeamento-atual-da-tecla)
6. [Criando um atalho com o xmodmap](#criando-um-atalho-com-o-xmodmap)
7. [Como tornar o atalho permanente](#como-tornar-o-atalho-permanente)
8. [Considerações finais](#considerações-finais)
9. [Referencias](#referencias)

## Visualizando o layout do teclado
No Windows eu podia usar os atalhos **Alt + 92** e **Alt + 124** para inserir essas barras, no Linux isso não funciona.

Pra esse tipo de teclado que eu tenho, a configuração usada no KDE é essa:

Modelo de teclado usado no KDE é: `Generic | Generic 105-key PC (intl.)`.

![Screenshot das configurações de teclado do KDE](https://cdn-images-1.medium.com/max/800/1*v8OjNq7jyZD4bqWa5LCORQ.jpeg)

Quanto ao **Layout** eu uso o pt-br padrão:

![Imagem mostrando como adicionar mais layouts](https://cdn-images-1.medium.com/max/800/1*PrxzeCY3hjUh0hpmCh_dGA.jpeg)

Como eu havia dito, o meu teclado, pelo menos visto superficialmente não tem a barra em pé e a contra barra, mas ao visualizar o mapa do Layout há mais atalhos para símbolos do que aqueles que estão marcados nas teclas físicas.

Para visualizar o mapa do layout é só clicar em **+ Adicionar** (conforme a imagem acima), selecionar o teclado pt-br e clicar em **Visualizar**, conforme a imagem abaixo.

![Selecionando o tipo de layout](https://cdn-images-1.medium.com/max/800/1*EZNgQFfBI-3H0KK7y0niTg.jpeg)

Esse é o mapa do layout pt-br visualizado no KDE:

![Screenshot do mapa do layout](https://cdn-images-1.medium.com/max/800/1*idDyqOx-pFuDU2n6UX3-WA.jpeg)

Em comparação com as teclas físicas, pelo mapa do layout podemos ver que existem mais atalhos de símbolos em quase todas as teclas, os simbolos podem ser ativados usando a tecla **AltGr** e também **AltGr** + **Shift** que podemos chamar de modificadores de 3º e 4º nível.

Mesmo que esse layout nos dê acesso há mais símbolos, a barra em pé `|` continua faltando.

Felizmente, conforme eu marquei na imagem acima, a tecla **N** não tem um símbolo próprio, nem de 3º e nem de 4º nível, isso significa que podemos usar essa tecla para adicionar o símbolo que tá faltando.

A barra em pé e a barra vertical são importantes já que no terminal, por exemplo, precisamos dela para certos [comandos que adicionam entradas de boot EFI](https://marcosfs93.github.io/2023-07-02-como-dar-boot-manualmente-recuperar-grub-efi-linux/) na BIOS e também em conjunto com o comando grep (`dmesg | grep nvidia`, por exemplo).

## Como remapear uma tecla do teclado
Enfim, o objetivo de exemplo nesse tutorial é criar um atalho para a **barra vertical** através da tecla **N**, pra isso vamos usar o comando **xmodmap**.

Com o xmodmap podemos remapear as teclas do nosso teclado, o primeiro passo é saber a identificação da tecla que vamos usar e saber o nome de referencia do símbolo que vamos usar.

## Como descobrir o código de identificação de uma tecla
O xmodmap precisa da identificação da tecla que vai ser usada, ou seja a **keycode**, para que o xmodmap crie o atalho para a tecla que a gente quer usar.

Pra isso devemos usar o comando **xev** que vai abrir uma mini janela e o terminal vai trazer várias informações de acordo com a tecla digitada:

![Screenshot do terminal rodando o comando xev](https://cdn-images-1.medium.com/max/800/1*Thao9xC9GXdMpmSlnYqibQ.jpeg)

No meu caso eu quero saber a keycode da tecla n, e o terminal vai informar conforme eu marquei na imagem acima, sendo assim a tecla **N é keycode 57.**

Sabendo disso nós já podemos usar o comando xmodmap e criar um atalho para o símbolo.

Mas antes disso vamos precisar de duas coisas: descobrir o mapeamento atual e o nome do símbolo a ser usado.

## Descobrindo o nome do símbolo para usar no xmodmap
Vamos começar descobrindo o nome do símbolo que a gente quer usar, no meu caso eu quero usar o símbolo da barra vertical (|) mas o nome dela precisa ser do tipo reconhecido pelo xmodmap.

No caso tem essa pagina aqui com uma lista de símbolos e nomes usados:

[https://wiki.linuxquestions.org/wiki/List_of_Keysyms_Recognised_by_Xmodmap](https://wiki.linuxquestions.org/wiki/List_of_Keysyms_Recognised_by_Xmodmap)

Com base nela, o nome da barra vertical é **bar**.

## Descobrindo o mapeamento atual da tecla
Agora que descobrimos qual é o nome do símbolo que é reconhecido pelo xmodmap, precisamos descobrir como é o mapeamento atual da tecla que nós vamos usar, afinal de contas não queremos prejudicar as outras funções da tecla, não é?

Pra isso nós usamos o comando **xmodmap -pke** que vai trazer a lista completa com as teclas mapeadas do layout e como já sabemos a **keycode** da tecla n, é só ir até essa parte do keycode 57:

![Encontrando o keycode da letra N](https://cdn-images-1.medium.com/max/800/1*_LFprdAQ-n2pmxcISxzV-Q.jpeg)

Certo, no caso da tecla N o mapeamento atual é esse:

> _“keycode 57 = n N n N”_

Agora nós podemos usar o xmodmap e criar um atalho para a tecla N.

## Criando um atalho com o xmodmap
O comando a ser usado para isso é:

    $ xmodmap -e "keycode 57 = n N n N bar"

Como eu havia dito no começo, a tecla N era a única que não tinha um atalho de símbolo e justamente por isso só bastou acrescentar uma palavra no final para adicionar o atalho do símbolo `|`.

Esse símbolo vai ser ativado quando eu usar o **AltGr + N**, ou seja, um atalho de 3º nivel e eu ainda tenho a opção de colocar outro atalho para ser usado a combinação **AltGr + Shift + N**, ou seja, de 4º nível.

Após o comando a tecla já vai funcionar e o símbolo será ativado quando você quiser, mas essa alteração com o xmodmap só dura até reiniciar o sistema.

## Como tornar o atalho permanente
Na verdade o que vamos fazer aqui não é uma alteração permanente, na verdade é um workaround onde nós configuramos um **autostart** em que esse atalho é aplicado após logar no sistema.

Primeiro nós precisamos criar um arquivo executável, com o comando xmodmap dentro dele.

1- Abra o terminal e digite:

    $ echo '#!/bin/bash sleep 10 && xmodmap -e “keycode 57 = n N n N bar” exit;' | sudo tee /usr/bin/remap57.sh_


2- Depois use o comando:

    $ sudo chmod a+x /usr/bin/remap57.sh

3- Agora é só ir nas configurações do KDE

**Configurações do sistema > Inicialização e desligamento > Iniciar Automaticamente**

Clique em **Adicionar script…**

Selecionar o caminho do script, /usr/bin/remap57.sh

![Screenshot das opções de auto start no KDE](https://cdn-images-1.medium.com/max/800/1*YHJOYwqIe3Wj_Oen23HhTw.jpeg)

Vale lembrar que há mais formas de automatizar a execução do script ao iniciar o sistema, o exemplo acima foi um dos exemplos disponíveis.

## Considerações finais
Tenho que agradecer a [Natália](https://dev.to/nfo94) pelo seu [artigo](https://dev.to/nfo94/como-remapear-teclas-no-linux-46p8) sobre o assunto, com ele eu pude resolver o meu problema e criar um atalho novo para simbolos no teclado.

Certamente essa é uma forma mais pratica de inserir símbolos do que usar o comando Ctrl + Shift + U junto com o código hexadecimal dele.

### Referencias:

- [https://dev.to/nfo94/como-remapear-teclas-no-linux-46p8](https://dev.to/nfo94/como-remapear-teclas-no-linux-46p8)
- [https://wiki.archlinux.org/title/xmodmap#Introduction](https://wiki.archlinux.org/title/xmodmap#Introduction)
- [https://wiki.linuxquestions.org/wiki/List_of_Keysyms_Recognised_by_Xmodmap](https://wiki.linuxquestions.org/wiki/List_of_Keysyms_Recognised_by_Xmodmap)

