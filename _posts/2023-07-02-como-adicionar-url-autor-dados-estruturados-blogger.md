---
title: Como adicionar a URL de autor nos dados estruturados do Blogger
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, adicionar, url, autor, dados, estruturados, blogger]
subtitle: Neste artigos vamos ensinar a como fazer isso
category: [Dicas e tutoriais, blogger]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*Dyh7HTMabBMnQuXS.jpg
share-img: https://cdn-images-1.medium.com/max/800/0*Dyh7HTMabBMnQuXS.jpg
layout: post
---

Hoje vou ensinar a colocar uma URL de Autor na parte de Dados Estruturados no seu Blog

Pra quem usa blogger é muito comum essa mensagem de erro aparecer, embora ter uma URL de autor seja opcional a mensagem de aviso sempre vai aparecer ao usar a ferramenta [**Teste de pesquisa aprimorada**](https://search.google.com/test/rich-results)

<p align='center'><img alt='Screenshot com o erro aparecendo' src="https://cdn-images-1.medium.com/max/800/0*Dyh7HTMabBMnQuXS.jpg"/></p>

Infelizmente no blogger não há uma função que nos permite adicionar uma url de autor facilmente, por isso vamos precisar editar o código HTML do blogger e fazer umas alterações simples.

## Procedimentos:
1- Vá no painel do blogger. basta entrar no endereço [https://blogger.com](https://blogger.com/)

No painel, vá em **Tema**, ao lado do botão **Personalizar** clique na seta ao lado e então clique na opção **Editar HTML**:

_Faça o backup do seu tema antes de fazer as alterações_

![Mostrando como abrir o editor html](https://cdn-images-1.medium.com/max/800/0*vI0v8RFCBsfLRiAN.png)

Ao abrir a janela contendo o código fonte do blog, dê um **Ctrl + F** e procure pelo seguinte código:

	<b:include data='post' name='postMetadataJSON'/>

O objetivo aqui é encontrar exatamente esse código:
```
<b:includable id='postMeta' var='post'>
<b:include data='post' name='postMetadataJSON'/>
</b:includable>
```
Ao encontrar esse código, substitua esse código acima pelo código abaixo:
```
<b:includable id='postMetadataJSON' var='post'>
<script type='application/ld+json'>
{
  "@context": "http://schema.org",
  "@type": "BlogPosting",
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "<data:post.url.canonical.jsonEscaped/>"
  },
  "headline": "<data:post.title.jsonEscaped/>",
  "description": "<b:eval expr='(data:post.body snippet { length: 150, links: false, linebreaks: false, ellipsis: true }).jsonEscaped'/>",
  "datePublished": "<data:post.date.iso8601.jsonEscaped/>",
  "dateModified": "<data:post.lastUpdated.iso8601.jsonEscaped/>",
  <b:include name='postMetadataJSONImage'/>
  <b:include name='postMetadataJSONPublisher'/>
  "author": {
    "@type": "Person",
    "url": "https://meuperfil.com",
    "name": "<data:post.author.name.jsonEscaped/>"
  }
}
</script>
</b:includable>
```

Substitua `"https://meuperfil.com"` pela URL do seu perfil de autor, no meu caso a URL vai ser essa:

[https://www.blogger.com/profile/05090528416485896825](https://www.blogger.com/profile/05090528416485896825)

Após definir a URL, basta salvar o tema e testar a ferramenta “teste de pesquisa aprimorada” do Google.

## Diferenças do código atual e do novo
Não há diferenças entre o código antigo e o novo, só que colocando a versão completa do código nos daria a possibilidade de adicionar um elemento a mais e que estava faltando no código original, que era a URL de autor nos dados estruturados

## Considerações finais
É isso, basta testar a ferramenta e se deparar com o resultado:

![Screenshot da ferramenta sem erros](https://cdn-images-1.medium.com/max/800/0*Mw9PM0Md3ExD7GWX.jpg)

Isso é tudo, até a próxima.
