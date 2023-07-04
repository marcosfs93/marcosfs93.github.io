---
title: Como resolver o Erro 256 no Lutris
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, resolver, erro 256, lutris]
subtitle: Saiba o que fazer para resolver esse erro
categories: [dicas e tutoriais, linux, games]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*4ulw9ndSQOZArfw0.png
share-img: https://cdn-images-1.medium.com/max/800/0*4ulw9ndSQOZArfw0.png
layout: post
---

<p align='center'><img alt='Screenshot do lutris exibindo o erro 256' src="https://cdn-images-1.medium.com/max/800/0*4ulw9ndSQOZArfw0.png"/></p>
Hoje estou aqui para compartilhar uma das soluções para resolver esse erro que pode acontecer pra quem usa o Lutris no Linux.

Com esse erro, na hora de abrir o jogo pelo Lutris nada acontece, você só consegue entender o que está havendo ao observar o arquivo de log onde no final do arquivo aparece a mensagem **Exit with return code 256**.

Eu passei por isso ao tentar jogar o KOF XV no Linux com o Lutris, o jogo funcionou normalmente após configurar o Lutris e depois não rodou mais.

**Conteúdo**

1. [O que fiz para resolver o problema](#o-que-fiz-para-resolver-o-problema)
2. [Como montar HDs automaticamente no sistema](#como-montar-hds-automaticamente-no-sistema)
3. [Como criar um link simbólico da pasta de um jogo](#como-criar-um-link-simbólico-da-pasta-de-um-jogo)
4. [Considerações finais](#considerações-finais)

## O que fiz para resolver o problema
A solução que eu encontrei para o meu caso foi fazer com que o disco contendo o jogo seja montado automaticamente, pra isso eu configurei o arquivo **/etc/fstab** e criei um link simbólico da pasta do jogo para dentro da minha pasta **home**.

Normalmente o Linux só monta os discos do sistema de forma automática, os HDs secundários e que não fazem parte do sistema só são montados pelo usuário manualmente no momento que abrimos um gerenciador de arquivos e acessamos o disco.

Por alguma razão o Lutris não roda o jogo em um HD externo que foi montado manualmente e as dicas podem te ajudar a conseguir resolver esse problema.

_Lembrando que o erro 256 pode ser causado por mais de um fator, por isso as dicas aqui podem não funcionar 100%, mas vale a pena tentar._

## Como montar HDs automaticamente no sistema
Primeiro nós precisamos fazer com que o HD que contém a pasta do jogo seja montado automaticamente pelo sistema.

Pra isso precisamos adicionar uma configuração no arquivo **/etc/fstab**, abra o terminal e digite o comando:

    $ sudo nano /etc/fstab

Ao abrir o nano, basta incluir no final do arquivo uma nova linha como essa:

`UUID=8C16067116065C98 /media/marcos/8C16067116065C98 ntfs nls-utf8,umask-0222,uid-1000,gid-1000,rw 0 0`

Imagem:

![terminal com o comando executado](https://cdn-images-1.medium.com/max/800/1*4WayV0nd2uylmLOEVMdhZA.jpeg)

No seu caso você deve colocar no seu arquivo **fstab**:

- O **UUID do HD** que contém o jogo
    Exemplo: **8C16067116065C98**
- O local onde o disco vai ser montado
    Exemplo: **/media/marcos/8C16067116065C98**.
- O tipo de formatação que o HD usa
    Exemplo: **ntfs**.
- As permissões de acesso do disco
    Exemplo: **nls-utf8,umask-0222,uid-1000,gid-1000,rw 0 0**

Para você descobrir qual é o UUID do disco, basta rodar esse comando aqui:

    $ lsblk -o NAME,MAJ:MIN,RM,SIZE,RO,TYPE,MOUNTPOINT,UUID

Imagem:

![terminal exibindo a lista de discos](https://cdn-images-1.medium.com/max/800/1*ZNIKXQuMIkSDNSA2doNqPA.jpeg)

Após saber o UUID do seu disco, é só adicionar uma nova linha no final do arquivo para montar o HD automaticamente, conformo foi explicado acima.

Depois de configurar o arquivo /etc/fstab, use as teclas **Ctrl + X** e digitar **S** ou o **Y** para salvar as mudanças no arquivo.

Reinicie o PC e tente configurar o Lutris novamente para rodar o jogo que está no HD

## Como criar um link simbólico da pasta de um jogo
Se montar o HD automaticamente não foi o suficiente pra fazer o jogo funcionar e o erro 256 persiste, talvez seja necessário **criar um link** da pasta que está no HD alternativo para a sua pasta **/home/usuário**.

Pode ser que o Lutris simplesmente não aceita que os jogos estejam fora do HD do sistema e criar um link simbólico possa contornar o problema, pelo menos no meu caso ajudou a fazer o jogo rodar.

Usando o KOF XV como exemplo, primeiro precisamos saber o diretório onde está a pasta “THE KING OF FIGHTERS XV”

No meu caso, essa pasta está em:

`/media/marcos/8C16067116065C98/THE KING OF FIGHTERS XV/`

Dentro dessa pasta vai existir os arquivo do jogo.

Imagem:

![arquivos da pasta do jogo](https://cdn-images-1.medium.com/max/800/1*dDJqd5r4E3G5MnpcLyO5ag.jpeg)

Sabendo o local onde está a pasta do jogo, precisamos criar um link para a pasta **home** onde ela vai ser direcionada para a pasta original.

No caso o comando a ser usado é esse:

    $ ln -s "/media/marcos/8C16067116065C98/THE KING OF FIGHTERS XV"  **~/KOFXV**

Após isso vai aparecer na pasta home uma nova pasta chamada **KOFXV** e ela vai ter os mesmos arquivos que estavam na pasta **THE KING OF FIGHTERS XV** do outro HD.

Imagem:

![abrindo o diretorio pelo link criado](https://cdn-images-1.medium.com/max/800/1*HskMhbtXeu5_sKGkiuvUKw.jpeg)

Com isso temos a impressão de que a pasta do jogo está no mesmo HD onde está o sistema, mas na verdade é um atalho para o outro HD onde essa pasta que está na home seja redirecionada para a pasta do outro HD.

Depois disso é só abrir o Lutris e selecione o executável do jogo através da pasta KOFXV que está na pasta home do usuário.

No meu caso ficou assim:

![lutris com o executavel selecionado nas opções do programa](https://cdn-images-1.medium.com/max/800/1*MyN57-W5XzWGlq_0FKPyIw.jpeg)

Após isso é só tentar rodar o jogo, se assim como eu dar certo o jogo vai finalmente abrir.

### Considerações finais:
Bom pessoal, espero que essa dica tenha te ajudado, caso não tenha dado certo eu sugiro que você tente mais uma vez procurar ajuda nos fóruns oficiais do Lutris pois como eu havia dito no começo do post: “o problema pode ser causado por outros fatores” que podem exigir outros tipos de configurações.

