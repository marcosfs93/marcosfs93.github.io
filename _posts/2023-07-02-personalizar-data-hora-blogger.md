---
title: Personalize a formatação de data e hora do Blogger
date: 2023-07-02
author: M4rQu1Nh0S
tags: [personalizar, data, hora, blogger]
subtitle: Aprenda a personalizar os formatos de data e hora
category: [Dicas e tutoriais, Blogger]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*xBVty8DQGuY4hs7-.png
share-img: https://cdn-images-1.medium.com/max/800/0*xBVty8DQGuY4hs7-.png
layout: post
---

<p align='center'><img alt='screenshot das configurações de formatação de data' src="https://cdn-images-1.medium.com/max/800/0*xBVty8DQGuY4hs7-.png"/></p>
Olá pessoal, bem vindos a mais um post exclusivo aqui do site, hoje vou mostrar como personalizar ainda mais a formatação de data e hora, que aparecem logo abaixo do titulo das postagens, páginas e também nos comentários dos leitores.

Eu achei necessário abordar esse assunto porque nas configurações do blogger, sem alguma razão aparente, a formatação de data segue uma ordem que é comum no exterior: o mes aparece primeiro e depois o dia do mês:

![lista de formatos de data](https://cdn-images-1.medium.com/max/800/0*YU_4zREq31Unmg3g.png)

Caso ainda não entenderam exatamente do que eu estou falando, basta olhar a imagem acima, e em alguns exemplos a seguir o mês vem antes do dia:

-   setembro 06, 2021
-   segunda-feira, setembro 06, 2021
-   9/06/2021
-   etc

O problema disso é que aqui no país a nossa formatação de data começa com o dia, depois o mês e por fim o ano:

-   06 setembro, 2021
-   segunda-feira, 06 setembro, 2021
-   06/9/2021
-   etc

Pelo que eu me lembro, o Blogger até então sempre tinha opções que deixavam a data começar com o dia e depois o mes, mas eu não sei quando isso mudou. De qualquer forma o blogger não tem muitas opções de formato que começam com o dia, então é aqui que o tutorial começa, vamos procurar outros meios de personalizar o formato da data.

## Procedimentos

Isso vai envolver modificações no código-fonte do seu blog, então vamos para o editor html do blog:

1- Vá no painel do blogger. basta entrar no endereço [https://blogger.com](https://blogger.com/)

No painel, vá em **Tema**, ao lado do botão **Personalizar** clique na seta ao lado e então clique na opção **Editar HTML**:

_Faça o backup do seu tema antes de fazer as alterações_

![mostrando como editar o codigo-fonte do blog](https://cdn-images-1.medium.com/max/800/1*7ugvRKRObPv4VJYWdxefKQ.png)

Ao abrir a janela contendo o código fonte do blog, dê um **Ctrl + F** e procure pelo seguinte código:

	<data:post.date/>

Depois de encontrar esse código, basta inserir o código abaixo:

	<b:eval expr='data:post.date format "dd MMMM yyyy"'/>

Parte desse código eu destaquei em vermelho, é aqui onde o formato da data será definido.

**dd** = dia do mês, será exibido 2 dígitos (Ex: 29)

**MMMM** = mês do ano, será exibido o nome do mês por extenso (Ex: Agosto)

**yyyy** = Ano do calendário, será exibido 4 dígitos referente ao ano (Ex: 1993)

## Adicionando separadores

Uma data que deveria ser, por exemplo, “08 **de** setembro **de** 2021” vai aparecer como “08 setembro 2021”, algo que não seria natural de se ler. Para contornar isso vamos modificar o código anterior.

Vamos precisar substituir o código por este código:

> _<b:eval expr=’data:post.date format “dd MMMM yyyy”’/>_ **_de_** _<b:eval expr=’data:post.date format “dd MMMM yyyy”’/>_ **_de_** _<b:eval expr=’data:post.date format “dd MMMM yyyy”’/>_

Dessa forma, ao visualizar uma postagem a data que vai aparecer será por exemplo **08 de setembro de 2021** e não mais “08 setembro 2021”.

## Considerações finais

Há diversas outras opções de formatação e todas elas estão listadas nesse link:

[https://www.unicode.org/reports/tr35/tr35-dates.html#Date_Field_Symbol_Table](https://www.unicode.org/reports/tr35/tr35-dates.html#Date_Field_Symbol_Table)

Basicamente é isso, o código aparecerá mais de uma vez no código-fonte do seu blog, dependendo do tema do blog você poderá substituir todos os códigos pelo código acima.

Espero que este artigo tenha sido útil para você, até a próxima.
