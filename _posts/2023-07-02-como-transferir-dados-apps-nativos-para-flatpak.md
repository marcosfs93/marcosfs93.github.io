---
title: Como transferir dados de um app nativo para a versão Flatpak
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, transferir, dados, apps, nativo, para, flatpak]
subtitle: Saiba como migrar a configuração dos apps nativos para versão flatpak
category: [Dicas e tutoriais, Linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*j_dQrIKqsa84kNd3.png
share-img: https://cdn-images-1.medium.com/max/800/0*j_dQrIKqsa84kNd3.png
layout: post
---

![](https://cdn-images-1.medium.com/max/800/0*j_dQrIKqsa84kNd3.png)<br/>
Se você tem algum aplicativo **nativo** para Linux e quer usar no lugar dele uma versão em **Flatpak**, talvez você queira usar as mesmas configurações que você já tinha com a versão nativa.

## Diretórios com configurações e dados dos apps
Geralmente quando estamos usando uma versão de software e vamos usar uma outra versão, pode acontecer de você precisar configurar tudo de novo.

Para evitar isso, podemos simplesmente copiar os dados do app que está instalado no sistema e transferir para o aplicativo que está em formato Flatpak.

A versão nativa de um aplicativo pode por padrão armazenar seus dados em até 3 locais da pasta **home** do usuário:

- /home/user/**.cache**/
- /home/user/**.config/**
- /home/user/**.local/share/**

Já a versão flatpak vai armazenar os dados em um local diferente da versão nativa, geralmente em:

- /home/user/**.var/app/**

## Como transferir os dados
Neste exemplo eu vou usar o emulador Yuzu, que tem versão Flatpak e versão tar.gz (código fonte), já que eu mesmo migrei da versão nativa para a versão flatpak, _o que serviu de inspiração para esse artigo_ 👍.

Primeiro basta entrar o diretório do app em flatpak, no caso do Yuzu é:

**/home/marcos/.var/app/org.yuzu_emu.yuzu/**

Dentro dessa pasta vai haver 3 pastas:

- cache
- config
- data

## Configurações do app
1- Primeiro vamos copiar os dados de configurações, entre no diretório

> /home/user/.config

2- Copie a pasta **Yuzu**.

3- Entre no diretório:

> /home/marcos/.var/app/org.yuzu_emu.yuzu/config

4- Colar a pasta Yuzu.

## Dados do App
1- Primeiro vamos copiar os dados de configurações, entre no diretório

> /home/user/.local/share

2- Copie a pasta **Yuzu**.

3- Entre no diretório:

> /home/marcos/.var/app/org.yuzu_emu.yuzu/data

4- Colar a pasta Yuzu.

## Conclusão
Depois disso é só abrir o App, se tudo der certo as configurações do app em flatpak estarão iguais ao da versão nativa, instalada no sistema.

O yuzu é apenas um exemplo, o processo é semelhante com os demais apps que você vai usar.

Existem arquivos que precisam de ser editados, como é o caso do arquivo qt-config.ini

> _/home/user/.var/app/org.yuzu_emu.yuzu/config/yuzu/_**_qt-config.ini_**

Nesse arquivo precisamos localizar e apagar o campo **[Data Storage]**, ao abrir o aplicativo as configurações padrões para flatpak serão aplicadas e o app funcionará normalmente.

Pois esse arquivo da versão nativa do sistema não é compatível com a versão flatpak.

Espero que esse tutorial tenha sido util, até a próxima.
