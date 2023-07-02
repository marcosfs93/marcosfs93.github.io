---
title: Como compilar o kernel do Linux
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, compilar, kernel, linux]
subtitle: Saiba o que fazer para compilar o kernel
category: [Dicas e tutoriais, Linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*6JpRF629V9_NL4i6.png
share-img: https://cdn-images-1.medium.com/max/800/0*6JpRF629V9_NL4i6.png
layout: post
---

![](https://cdn-images-1.medium.com/max/800/0*6JpRF629V9_NL4i6.png)
Olá pessoal, hoje estou trazendo o meu método para fazer a compilação do kernel Linux para a sua distribuição. Já existe diversos sites que ensinam a como compilar o kernel, mas acredite, eu demorei horas pra achar um tutorial que me ajudasse a fazer isso sem problemas.

Claro, não vai ser um tutorial de minha exclusividade pois estarei usando dicas já existentes, o que estou fazendo aqui é compartilhar a forma que deu certo pra mim, o propósito é compartilhar um tutorial que funciona para vocês e para mim também, para o caso de eu precisar recompilar o kernel no futuro e não ter que perder horas só pra achar o tutorial que funciona.

_No final desse post vou estar incluindo todos sites que me baseei na criação deste tutorial aqui_

Agora que eu já desabafei fiz a introdução ao post de hoje, vamos aos procedimentos para a compilação do Kernel, mas antes vale lembrar que não vou ser muito didático nesse tutorial e por isso não vou explicar em detalhes todos os procedimentos, somente o mínimo necessário para a compilação.

#### **Conteúdo**

1.  [Preparos iniciais para a compilação do kernel](#b342)
    1.1. [Instalação das dependências](#397f)
    1.2. [Baixando e descompactando o código-fonte do kernel](#68fd)
    1.3. [Realizando configurações e modificações do kernel](#2aca)
2.  [Compilando o kernel](#a4cb)
3.  [Instalando o kernel no sistema](#instalando-o-kernel-no-sistema)

## 1- Preparos iniciais para a compilação do kernel
### 1.1- Instalação das dependências

A compilação do kernel exige ferramentas que não vem pré instaladas nas distribuições e por isso é necessário baixar e instalar as dependências primeiros.

Para distribuições baseadas no Debian/Ubuntu:

	$ sudo apt install git fakeroot build-essential ncurses-dev xz-utils libssl-dev bc flex libelf-dev bison

### 1.2- Baixando e descompactando o código-fonte do kernel
Após instalar as dependências, só falta baixar o código-fonte do Kernel, para baixar o kernel acesse o site abaixo:

[https://kernel.org](https://kernel.org/)

Ao acessar o site acima, você poderá escolher 3 versões do kernel para compilar, a versão estável, a em desenvolvimento e a versão com suporte estendido.

Recomendo baixar a versão estável, então baixe a versão **stable** do site, que na data de hoje é a **“5.17.6**” e consequentemente o arquivo a ser baixado será **“linux-5.17.6.tar.xz**”.

_A partir desse ponto vamos usar a versão 5.17.6 como exemplo do tutorial, sempre ao ver o 5.17.6 substitua pela versão que você vai instalar, a não ser que você queira instalar exatamente essa versão._

Ao terminar o download, vá na pasta de downloads que geralmente fica em _/home/seu_usuário/Downloads_, ainda no terminal use o comando para entrar na pasta de Download:

	$ cd ~/Downloads

No terminal, digite o comando **ls** para listar o conteúdo da pasta ‘Downloads’, se for a pasta certa o terminal vai listar o arquivo baixado do kernel.

Vamos precisar descompactar o kernel baixado, use o comando para fazer a extração do arquivo:

	$ tar -xvf  **linux-5.17.6.tar.xz**

Ao terminar a extração, uma pasta chamada ‘**linux-5.17.6**’ vai surgir, digite o comando abaixo para entrar nessa pasta:

	$ cd linux-5.17.6

### 1.3- Realizando configurações e modificações do kernel
Para começar, vamos usar o comando abaixo para importar as configurações atuais do kernel para o novo kernel a ser compilado:

	$ cp -v /boot/config-$(uname -r) .config

Após isso, se quiser você pode fazer mais modificações nas configurações do novo kernel, para prosseguir use o comando abaixo.

	$ make menuconfig

Faça o que tiver que fazer e saia selecionando o botão **Exit** do menu inferior.

A partir desse ponto vamos precisar prosseguir o restante da compilação usando o usuário **root**, use o comando abaixo:

	$ sudo su

Agora você pode modificar os arquivos do kernel, antes de fazer a compilação faça todas as modificações que você precise fazer nos arquivos antes de continuar

## 2- Compilando o kernel

Agora que estamos com o usuário root, use o comando **make** para iniciar a compilação do kernel:

**_Dica:_** _Você pode usar mais cores do processador para deixar a compilação do kernel mais rápida, use o argumento_ **_‘-j’_** _junto com o numero de processadores do seu processador_

Para você saber quantos cores existem no processador, basta usar esse comando no terminal:

	$ nproc

Aqui o resultado foi 8, sendo assim são 8 nucleos, para usar todos os nucleos o comando vai ser…

	# make -j8 bzImage

Vamos verificar se está tudo certo até aqui, usa o comando abaixo para verificar se o arquivo **bzImage** existe:

	# ls arch/x86_64/boot/

Vamos agora compilar os módulos do kernel, use o comando abaixo para continuar:

	# make -j8 modules

Após usar esse comando o kernel será compilado, essa parte pode demorar dependendo do processador e numero de cores serão usados na compilação do kernel.

## 3- Instalando o kernel no sistema
Chegou a hora de instalar o kernel recém compilado no sistema, use o comando abaixo para realizar esse processo:

	# make modules_install

e em seguida

	# make install

Com isso o kernel será instalado e logo em seguida o carregador de inicialização será atualizado.

