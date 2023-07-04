---
title: Como resolver o Erro no servidor (5xx) do Blogger
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, resolver, erro, 5xx, blogger]
subtitle: Saiba como resolver esse erro
categories: [dicas e tutoriais, Blogger]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/1*GxxIhvaoXQQ8NBLpG5xIAQ.png
share-img: https://cdn-images-1.medium.com/max/800/1*GxxIhvaoXQQ8NBLpG5xIAQ.png
layout: post
---

<p align='center'><img alt='imagem mostrando o tal erro 5xx' src="https://cdn-images-1.medium.com/max/800/1*GxxIhvaoXQQ8NBLpG5xIAQ.png"/></p>
Na ferramenta Search Console do Google existe um erro de servidor que pode afetar blogs na plataforma Blogger, esse tipo de erro é temporário e por isso não tinha o que se fazer a respeito desse problema além de esperar a equipe do Google resolver.

Mas como até hoje não vi uma solução e o SEO do meu blog estava péssimo, já que minhas páginas não apareciam no google, eu decidi tentar algumas coisas, e parece que consegui ao menos “amenizar” o problema.

A seguir, vou mostrar pra vocês o que eu fiz pra resolver esse problema, quer dizer, desde que eu fiz isso até agora eu não me deparei mais com o erro 5xx. Pode ser uma coincidência ou de fato os procedimentos aqui deram certo.

1- A primeira coisa que devemos fazer é entrar no Blogger e acessar as configurações do seu blog.

![mostrando como ativar robots.txt personalizados](https://cdn-images-1.medium.com/max/800/1*Jht8gweQELH15hw1eGm8Dw.png)

Vamos em configurações, descer a pagina até chegar na parte **Rastreadores e indexação** e ativar os recursos: “**Ativar robots.txt personalizado”** e **“Ativar as tags personalizadas de cabeçalho de robos”**

Depois de ativarmos esses dois, dê um click sobre o **robots.txt personalizado**.

Ao fazer isso vai abrir um pequeno campo de texto, nele você deve colocar o seguinte texto:

> _User-agent: Mediapartners-Google_
> _Disallow:_
>
> _User-agent: *_
> _Disallow: /search_
> _Allow: /_
>
> _Sitemap:_ _https://url_do_seu_blog/sitemap.xml_

lembre-se de substituir o **https://url_do_blog/sitemap.xml** pela a URL do seu blog ein!

![Area de criação do robots.txt personalizado.](https://cdn-images-1.medium.com/max/800/1*sO-tF6JZr2GTxA4nGte13Q.png)

Clique em SALVAR para gravar as alterações.

2- Agora vamos mexer nas **tags personalizadas**, clique em **Tags de página inicial** e habilite apenas as tags **All** e **Noodp** e depois clique em salvar:

![selecionar as tags para a home page](https://cdn-images-1.medium.com/max/800/1*UZIpWvKVB9JD8Y-7l2w8jA.png)

3- Vamos agora mexer nas **Tags de páginas de pesquisa e arquivo**, aqui você deve habilitar apenas as tags **NoIndex** e **Noodp:**

![selecionando as tags noindex e noodp](https://cdn-images-1.medium.com/max/800/0*q1ilFWTnZofD6cqd.png)

4- Por ultimo vamos mexer nas **Tags de Página e Postagens**, aqui você vai deixar habilitado apenas as tags **All** e **Noodp**:

![selecionando as tags all e noodp](https://cdn-images-1.medium.com/max/800/0*tPQ0nfwQxsaCvkI1.png)

Clique em salvar, isso conclui as alterações necessárias no Blogger, pois vamos precisar ir lá no Search Console porque lá existe uma configuração importante e que pode ter sido a causa do erro 5xx, essas mudanças do blogger servem para garantir que as devidas configurações estejam em vigor no momento que o seu blog for rastreado pelos motores de busca.

Agora vem a parte mais importante, vamos configurar a [**Taxa de Rastreamento**](https://support.google.com/webmasters/answer/48620?hl=pt)

> _O termo_ **_taxa de rastreamento_** _representa o número de solicitações por segundo que o Googlebot faz para seu site ao rastreá-lo (por exemplo, cinco solicitações por segundo)._

Provavelmente a taxa padrão de rastreamento esteja causando problemas de **disponibilidade** do blog para o motor de busca, vamos precisar diminuir essa taxa para que isso amenize o problema de erro 5xx.

Porem o recurso acima só funciona para propriedades do tipo **Prefixo de URL**, se o seu blog está incluso no Search Console como **Dominio**, ele não vai funcionar. Você pode remover o seu blog do search console e adicionar novamente:

![imagem recomendando criar como Prefix de URL](https://cdn-images-1.medium.com/max/800/1*tTgXeCRIwq-YRIjxrpj-TQ.png)

Bom, depois de verificar e constatar que o seu blog está registrado no Search Console como **Prefixo de URL**, podemos prosseguir com o proximo passo, clique no link abaixo para ir na configuração na Taxa de rastreamento:

[https://www.google.com/webmasters/tools/settings](https://www.google.com/webmasters/tools/settings)

Depois disso é só deixar a taxa de rastreamento igual na imagem abaixo:

![configurando a taxa de rastreamento](https://cdn-images-1.medium.com/max/800/0*mU-eWdwDLjIwJJzR.png)

É só deixar a taxa no mais baixo possível e salvar, como podem ter notado essa mudança não é permanente, após aplicar as alterações será contado 3 meses e depois voltar pra taxa padrão de rastreamento.

Eu decidi fazer essa alteração já que somente o Search Console apresentava erro 5xx, os demais motores não tinham esse problema e parece que o problema era esse. Agora é só aguardar pelo menos 24 hores e testar as suas páginas no Search Console e ver se o erro 5xx foi resolvido ou menos frequentes.

Se você teve que remover e adicionar o seu site no Search Console, lembre-se de adicionar o sitemap novamente.

