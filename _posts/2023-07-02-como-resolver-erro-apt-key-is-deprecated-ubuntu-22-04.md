---
title: Como resolver erro 'apt-key is deprecated' no Ubuntu 22.04
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, resolver, erro, apt-key is deprecated, ubuntu, 22.04]
subtitle: Aprenda a como resolver esse erro
category: [Dicas e tutoriais, linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*PewwIs2RCbdTEKLR.png
share-img: https://cdn-images-1.medium.com/max/800/0*PewwIs2RCbdTEKLR.png
layout: post
---

<p align='center'><img alt='Terminal mostrando o manual do apt' src="https://cdn-images-1.medium.com/max/800/0*PewwIs2RCbdTEKLR.png"/></p>
Quem está usando o Ubuntu 22.04 e tentou instalar algum repositório PPA ou qualquer outro repositório de pacotes, deve ter começado a receber as mensagem sobre o apt-key ao rodar o comando ‘apt update’:

> _Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8))._

Eu percebi esse problema ao tentar usar os repositórios do Linux Mint e o PPA do Lutris no Ubuntu 22.04.

## Causa do problema
O problema acontece ao tentarmos adicionar um repositório usando o comando **add-apt-repository** com um PPA.

Exemplo:

	$ sudo add-apt-repository ppa:lutris-team/lutris

O comando **add-apt-repository** vai adicionar um arquivo .list no diretório /etc/apt/sources.list.d/ com o nome do repositório e vai adicionar a chave gpg do ppa no arquivo **trusted.gpg** (/etc/apt/trusted.gpg).

Acontece que o arquivo trusted.gpg não é mais usado para guardar as chaves gpg dos repositórios, e qualquer chave que for adicionada nesse arquivo vai provocar aquela mensagem de erro toda vez que você usar o apt update.

## Como resolver:
### Repositórios PPA
Enquanto a solução não chega, devemos remover as chaves do arquivo trusted.gpg e coloca-las em seus devidos lugares.

1- `$ sudo add-apt-repository ppa:autor/projeto`
2- `$ apt-key list`
3- `$ gpg --export <chave-assinatura> | sudo tee /usr/share/keyrings/nome-repositorio.gpg`

Exemplo:

> _gpg — export 1234567890123456789012345678901234567890 | sudo tee /usr/share/keyrings/nome-repositorio.gpg_

4- `$ sudo nano /etc/apt/sources.list.d/nome-repositorio.list`
5- Procure e substitua conforme o exemplo:

> _deb_ [_http://ppa.launchpad.net/autor/projeto/ubuntu_](http://ppa.launchpad.net/autor/projeto/ubuntu) _jammy main_

Para

> _deb [signed-by=/usr/share/keyrings/nome-repositorio.gpg]_ [_http://ppa.launchpad.net/autor/projeto/ubuntu_](http://ppa.launchpad.net/autor/projeto/ubuntu) _jammy main_

6- Salve o arquivo com as alterações e depois rode novamente o comando **apt update**.

Outros repositórios:

Para adicionar repositórios de outras fontes, você pode fazer igual eu fiz quando eu queria usar os repositórios do Linux Mint 21 no Ubuntu 22.04

1- Adicione o repositório que você quer

Exemplo:

```
$ sudo add-apt-repository -y "deb [signed-by=/usr/share/keyrings/mint_vanessa.gpg] http://packages.linuxmint.com vanessa main upstream import backport"
```

Detalhe, o arquivo mint_vanessa.gpg ainda não existe, mas vamos cria-lo depois porque agora vamos precisar saber a ID da chave que vai ser adicionada no trusted.gpg primeiro.

2- Rode o comando apt update

	$ sudo apt update

Ao fazer isso você vai ver essa mensagem enquanto o apt atualiza a base de dados:

> _W: Falhou ao buscar_ [_http://packages.linuxmint.com/dists/vanessa/Release.gpg_](http://packages.linuxmint.com/dists/vanessa/Release.gpg) _As assinaturas a seguir não puderam ser verificadas devido à chave pública não estar disponível:_ **_NO_PUBKEY A6616109451BBBF2_**_._

A mensagem de erro acima informou a ID da chave que precisamos pra criar o arquivo **mint_vanessa.gpg**

3- Rode os dois comandos abaixo:

	$ gpg --recv-keys --keyserver keyserver.ubuntu.com  A6616109451BBBF2

	$ gpg --export  A6616109451BBBF2  | sudo tee /usr/share/keyrings/mint_vanessa.gpg

Esses comandos vão procurar a assinatura da chave pelo ID e com o mesmo ID vai extrair a assinatura da chave e transformar em um arquivo no formato aceito do APT.

4- Rode o comando **apt update**, a mesagem deverá sumir.

## Considerações finais:
O problema ja foi passado para a canonical e será uma questão de tempo até esse problema desaparecer, até então os repositórios adicionados pelo usuário terão de passar por esses procedimentos a ponto do repositório e sua respectiva chave estejam dentro dos conformes de segurança do sistema.

Espero ter ajudado, até a próxima.
