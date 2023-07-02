---
title: Como instalar o .NET Framework no Windows 11
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, instalar, .net framework, windows 11]
subtitle: Saiba como instalar
category: [Dicas e tutoriais, Windows 11]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*tXibQ12giB31EbTg.png
share-img: https://cdn-images-1.medium.com/max/800/0*tXibQ12giB31EbTg.png
layout: post
---

![logo .NET framework](https://cdn-images-1.medium.com/max/800/0*tXibQ12giB31EbTg.png)
Por um momento eu fiquei preocupado já que eu passei alguns minutos tentando instalar o .NET Framework 3.5 e não estava conseguindo. Ao pesquisar um pouco eu vi que o processo de instalação do Framework é igual do Windows 10.

Meu objetivo nesse post não é pra falar sobre a utilidade e necessidade do Framework, creio que você também só precisa instalar e usar os seus aplicativos certo? bom, antes de passar os procedimentos **é necessário ter a ISO/DVD de instalação do Windows 11**, atualmente a unica forma de instalar o Framework é usando a ISO de Instalação.

### Agora sim, vamos aos procedimentos

## Passo 1

Precisamos usar aplicativos que permitam extrair o conteúdo da ISO do Windows 11, eu mais uma vez recomendo usar o **Ultra ISO**. Esse app é capaz de criar um driver virtual de disco, e com ele podemos instalar o Framework.

Instale e abra o Ultra ISO, quando o App abrir aperte **F6**

Aqui no meu caso o driver virtual era o **Disco (K:)**, lembre bem da letra do disco que apareceu na sua tela, pois você vai precisar.

Em **Image File:** clique nos **[…]** e selecione a ISO do Windows 11.

Selecione a ISO, depois clique em **Abrir** e voltando na janela anterior… clique em **Montar**

## Passo 2:

Recomendo que você tente entrar no driver com a ISO do Windows para ver se está tudo Ok.

Após conferir… abra o CMD como administrador, pra isso basta abrir o Menu da barra de tarefas, digitar CMD, e abaixo do icone dele… clicar em **Executar como Administrador**

Feito isso o CMD vai aparecer, agora insira o comando abaixo e aperte Enter:

> _dism /online /enable-feature /featurename:NetFx3 /All /Source:_**_K_**_:\sources\sxs /LimitAccess_

**Atenção, substituia o “K:\” pela letra relacionada ao driver com a ISO do Windows 11,** aqui no meu PC é a letra K mesmo.

![](https://cdn-images-1.medium.com/max/800/1*pUb_5hbuhcHATtcNIP84Rw.png)

Depois disso é só esperar a barra carregar os 100% e apresentar a mensagem: **The Operation completed successfully.** Pronto, instalado o NET Framework 3.5, ele já acompanha as versões anteriores (2.0 e 3.0).
