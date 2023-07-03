---
title: Como criar link dos tópicos nas postagens
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, criar, link, tópicos, indice, postagem]
subtitle: Aprenda a criar um link dos tópicos nos seus artigos
category: [Dicas e tutoriais]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*W0mxFx22nxSHq9dh.png
share-img: https://cdn-images-1.medium.com/max/800/0*W0mxFx22nxSHq9dh.png
layout: post
---

<p align='center'><img alt='Ilustração de uma lista formatado em html' src="https://cdn-images-1.medium.com/max/800/0*W0mxFx22nxSHq9dh.png"/></p>
Olá pessoal, hoje estou aqui pra trazer uma dica rápida sobre como criar um [índice](https://pt.wikipedia.org/wiki/%C3%8Dndice_de_conte%C3%BAdo) ou sumário com ancoras nas suas postagens. Usar tópicos são úteis tanto para postagens grandes como também para usuários que estão procurando apenas uma parte dos artigos.

Além do índice, que fica no começo das postagens, ser um elemento útil para os leitores que vão saber quais tópicos vão ser abordados ao decorrer da leitura, as ancoras são mais úteis ainda, pois com elas e com um único click o leitor vai parar direto na parte que lhe interessa.

## Tags usadas no índice e nos elementos da página
A ideia usada na criação dos links no índice e as ancoras para os elementos da página é bem simples:

Para os índices, que vão ficar no topo da página, deve ser usado a **tag html href**

> _exemplo: <h3>_**_<a href=”parte1">_**_Índice_**_<a>_**_</h3>_

Para os elementos da página, como o titulo do tópico, deve ser usado a **tag html ID**

> _exemplo:_ **_<h3 id=”parte1">_**_Título_**_<h3>_**

## Entendendo a lógica
Se você olhar as duas tags acima com cuidado, vai perceber que existe uma lógica ali.

O conteúdo na tag **href** e na tag **id** são praticamente iguais, a única diferença ali é a **cerquilha** **(#)** que está presente na tag href e ausente na tag id.

Com isso podemos concluir que:

- Nos índices devemos usar a tag href e o símbolo “#” deve estar presente
- Nos elementos da página devemos usar a tag id e o símbolo # não pode estar presente
- O valor da tag href e id devem ser iguais, caso contrário a ancoragem não vai funcionar.
- A tag href é um link que direciona o usuário para uma parte da página
- A tag ID é um identificador de um elemento.
- Quando um link href é clicado, ele leva o usuário até a parte onde se encontra o destino, que no caso é o ID que foi definido.

## Colocando a lógica em prática:
Agora que já entendemos como isso funciona, vamos criar os índices.

Na parte dos índices, que é uma lista de tópicos, vamos adicionar as tags href com valores únicos.

Veja esse exemplo abaixo:

### Exemplo 1:

```
<h2>Índice:</h2>

<ul>

<h3><a href="#parte1">Tutorial - Parte 1</a></h3>

<h3><a href="#parte2">Tutorial - Parte 2</a></h3>

<h3><a href="#parte3">Tutorial - Parte 3</a></h3>

<h3><a href="#parte4">Tutorial - Parte 4</a></h3>

</ul>
```

No exemplo acima criamos um índice onde cada tópico tem uma tag href única e todas elas tem o símbolo **#** presente ali.

Agora veja o exemplo abaixo:

### Exemplo 2:

```

<h3 id="parte1">Tutorial - Parte 1</h3>

<p>Bem vindos, esta é a parte 1 do tutorial...</p>

<br/>

<h3 id="parte2">Tutorial - Parte 2</h3>

<p>Nessa segunda parte faremos o seguinte</p>

<br/>

<h3 id="parte3">Tutorial - Parte 3</h3>

<p>Agora que terminamos a segunda parte, precisamos fazer isso...</p>

<br/>

<h3 id="parte4">Tutorial - Parte 4</h3>

<p>Chegamos na 4ª e ultima parte do tutorial, com isso terminamos</p>
```
Neste segundo exemplo, é simulado o restante da página que é o artigo em si e que vem depois da parte dos Índices.

Da forma em que construimos os dois exemplo, se no **exemplo 1** eu clicar no índice “**Tutorial — Parte 1**” eu vou ser levado até a parte onde está o exemplo 2 e minha leitura começa na parte “Tutorial — Parte 1” onde está o parágrafo “**Bem vindos, esta é a parte 1 do tutorial…**”

## Links não estão funcionando
Tenha em mente que a ID precisa ser única, quando não funciona é sinal de que o ID já está sendo usado por outra parte do site, em casos assim mudar o nome do ID resolve mas se o problema persistir é importante verificar se a construção do código está certa.

Bom pessoal, esse foi o tutorial de hoje, espero ter ajudado.
