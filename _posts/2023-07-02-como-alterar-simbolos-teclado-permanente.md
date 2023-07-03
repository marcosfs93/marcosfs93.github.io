---
title: Como alterar os símbolos do teclado permanentemente
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, alterar, simbolos, teclado, permanente]
subtitle: Saiba como tornar permanente a personalização dos atalhos de simbolos
category: [Dicas e tutoriais, Linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/1*idDyqOx-pFuDU2n6UX3-WA.jpeg
share-img: https://cdn-images-1.medium.com/max/800/1*idDyqOx-pFuDU2n6UX3-WA.jpeg
layout: post
---

<p align='center'><img alt='Imagem layout de teclado comum' src="https://cdn-images-1.medium.com/max/800/1*idDyqOx-pFuDU2n6UX3-WA.jpeg"/></p>
Dependendo do modelo do teclado que você está usando, alguns símbolos podem estar faltando ou serem diferentes. Por exemplo, no meu teclado, não existem atalhos para os símbolos `|` e `\`

Para resolver esse problema, já publiquei dois artigos sobre o assunto:

- [Como adicionar simbolos que não tem no teclado](https://marcosfs93.blogspot.com/2023/03/como-alterar-os-simbolos-do-teclado.html)
- [Como criar um atalho da barra vertical no Linux](https://marcosfs93.blogspot.com/2023/03/como-criar-um-atalho-da-barra-vertical.html)

Mas hoje, estou aqui para ensinar como você pode aplicar essas alterações de forma permanente, diretamente no mapa do teclado, sem a necessidade de usar scripts.

## Descobrindo o nome do símbolo
Para fazer isso, primeiro, você precisa saber o nome do símbolo que deseja adicionar ao teclado.

Para isso, basta acessar o seguinte site:

[https://wiki.linuxquestions.org/wiki/List_of_Keysyms_Recognised_by_Xmodmap](https://wiki.linuxquestions.org/wiki/List_of_Keysyms_Recognised_by_Xmodmap)

Nesse site, você pode procurar o símbolo que deseja adicionar e descobrir o seu nome. Por exemplo, se você quiser adicionar o símbolo `|`, o nome desse símbolo é `“bar”`.

## Veja como editar o arquivo referente ao mapa do teclado:
1- Antes de começar, faça o backup do arquivo **/usr/share/X11/xkb/symbols/br** para garantir que você possa reverter as mudanças, se necessário.

2- Em seguida, abra o arquivo **/usr/share/X11/xkb/symbols/br** e procure pela chave e letra que você deseja atribuir um novo símbolo.

2.1 É importante notar que algumas teclas podem não aparecer no arquivo br, pois ele contém apenas adaptações baseadas no teclado US. Se esse for o caso, abra o arquivo **/usr/share/X11/xkb/symbols/us** e procure pela letra desejada. Recomendamos começar a procurar a partir da **linha 990** do arquivo **us**.

Quando encontrar a letra, copie a linha inteira correspondente e cole-a no arquivo **br**.

3- Em seguida, cole a linha copiada na linha 34 do arquivo **br**.

4- Após editar o arquivo, reinicie o computador. Ao pressionar a combinação de teclas correspondente, o novo símbolo deve aparecer.

## Considerações finais:
É importante lembrar que a maioria dos símbolos importantes já está disponível nos teclados padrão, portanto, apenas faça alterações se for necessário para suas atividades específicas. E, ao comprar um novo teclado, verifique se as teclas e símbolos necessários já estão disponíveis. Até a próxima!

### Referencias:
- [https://wiki.linuxquestions.org/wiki/List_of_Keysyms_Recognised_by_Xmodmap](https://wiki.linuxquestions.org/wiki/List_of_Keysyms_Recognised_by_Xmodmap)
- [https://superuser.com/questions/1460984/how-to-get-a-list-of-valid-x11-names-for-characters](https://superuser.com/questions/1460984/how-to-get-a-list-of-valid-x11-names-for-characters)

