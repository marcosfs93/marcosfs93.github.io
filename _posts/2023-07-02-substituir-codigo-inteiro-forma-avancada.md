---
title: Como substituir um codigo no Notepad++ de forma avançada
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, substituir, codigo, notepad++, metodo, avançado]
subtitle: Substitua qualquer parte do código de forma avançada
category: [Dicas e tutoriais]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*ukFOU5MlqIgfPRiI
share-img: https://cdn-images-1.medium.com/max/800/0*ukFOU5MlqIgfPRiI
layout: post
---

<p align='center'><img alt='logo notepad++' src="https://cdn-images-1.medium.com/max/800/0*ukFOU5MlqIgfPRiI"/></p>
Olá pessoal, hoje eu trago um tutorial bem interessante com o **Notepad++**, com ele vamos aprender a como substituir um código inteiro, mesmo que o conteúdo dentro desse código seja diferente.

Substituir vários códigos de uma vez não é possível usando a função de **Substituir textos**, geralmente para a substituição funcionar você tem que digitar **exatamente** o que deve ser substituído.

Até agora eu falei sobre a substituição comum, algo que todo editor de texto faz, porém o que vamos usar aqui é a **Substituição Avançada**, com ela a gente pode usar **Expressões Regulares** que vão nos permitir aplicar regras avançadas de procura e substituição de textos.

## Exemplo com a tag
Veja no exemplo a seguir, a tag vai aparecer mais de uma vez, porem cada tem um conteúdo diferente:

> _<link rel=’replies’
> type=’text/html’
> href=’_[_https://sitemrcs.blogspot.com/2021/07/firefox-como-importar-os-dados-do-brave.html#comment-form'_](https://sitemrcs.blogspot.com/2021/07/firefox-como-importar-os-dados-do-brave.html#comment-form%27)_
> title=’0 Comentários’/>_
>
> _<link rel=’edit’
> type=’application/atom+xml’
> href=’_[_https://www.blogger.com/feeds/5579190642679812527/posts/default/6310289833593844013'/>_](https://www.blogger.com/feeds/5579190642679812527/posts/default/6310289833593844013%27/%3E)
>
> _<link rel=’self’
> type=’application/atom+xml’
> href=’_[_https://www.blogger.com/feeds/5579190642679812527/posts/default/6310289833593844013'/>_](https://www.blogger.com/feeds/5579190642679812527/posts/default/6310289833593844013%27/%3E)
>
> _<link rel=’alternate’
> type=’text/html’
> href=’_[_https://sitemrcs.blogspot.com/2021/07/firefox-como-importar-os-dados-do-brave.html'_](https://sitemrcs.blogspot.com/2021/07/firefox-como-importar-os-dados-do-brave.html%27)_
> title=’Firefox — Como importar os dados do Brave
> Browser’/>_

No caso, eu quero que o editor faça o seguinte:

Procurar por todas as tags <link> e ao encontrar todas elas, apagar tudo, deixando o restante do arquivo inalterado.

Fazer isso com a substituição normal de texto não será possível, então vamos usar o modo “Expressão regular” para aplicar um filtro que vai encobrir toda a tag <link> do inicio até o final do código (‘/>).

## Utilizando expressão regular para encontrar o código

Com o Notepad++ aberto, aperte **Ctrl + H**, e selecione a opção “expressão regular”

![selecionando a opcao 'expressao regular'](https://cdn-images-1.medium.com/max/800/1*ih4zZBVPzIazeJYGyvxYrw.jpeg)

Em **localizar**, escreva: **(?s-i)<link( |).*?/>**

Em **Substituir por**, deixe em branco, e clique em **Substituir todos**

Ao clicar em “Substituir todos”, o editor fará o seguinte:

Vai procurar tudo que começa com **<link** e termina com **/>**, e ao encontrar… vai substituir pelo texto que eu colocar em “Substituir por:” mas como deixei em branco, o texto será apagado.

Você também pode aplicar essa regra para códigos <script> que terminam com </script>:

> _<script type=’text/javascript’>_
>
> _BLOG_CMT_createIframe(‘<data:post.appRpcRelayPath/>’);_
>
> _</script>_

A expressão regular no caso, será essa:

    **_(?s-i)<(script)( |>).*?</\1>_**

## Considerações finais:
Graças as expressões regulares, podemos automatizar a substituição de códigos e textos com bastante eficiência e economia de tempo, eu tinha descoberto isso recentemente ao procurar formas de apagar códigos específicos em um arquivo.

Era isso que eu tinha a compartilhar com vocês, até a próxima.

## Referencia:
-  [https://community.notepad-plus-plus.org/topic/13669/finding-html-tags-and-everything-between-them-on-multiple-lines/](https://community.notepad-plus-plus.org/topic/13669/finding-html-tags-and-everything-between-them-on-multiple-lines/)

