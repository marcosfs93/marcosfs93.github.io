---
title: Tutorial - Como rodar MIR4 no Linux
date: 2023-07-02
author: M4rQu1Nh0S
tags: [tutorial, guia, como, rodar, mir4, linux]
subtitle: Saiba o que fazer para o jogo funcionar no Linux
categories: [dicas e tutoriais, games]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*XziR1_3Bo3ciu7sT.png
share-img: https://cdn-images-1.medium.com/max/800/0*XziR1_3Bo3ciu7sT.png
layout: post
---

<p align='center'><img alt='banner do tutorial' src="https://cdn-images-1.medium.com/max/800/0*XziR1_3Bo3ciu7sT.png"/></p>
Olá pessoal, trago finalmente o tutorial para fazer o MIR4 funcionar no Linux, além do tutorial que será apresentado a seguir, um vídeo do tutorial também já está disponível no YouTube, assim você tem duas versões do tutorial disponível pra você.

Antes de mais nada, é importante afirmar que este tutorial não é 100% garantido de funcionar, justamente por questões de hardware e configurações especificas de cada distribuição do Linux, tenha isso em mente, embora eu tenha testado isso em várias distros e não tive problemas.

**Atenção:** Esse artigo vai ser atualizado sempre que houver novidades, não deixe de visitar a página para não perder dicas e soluções futuras para os problemas de desempenho do jogo.

Este artigo foi atualizado pela ultima vez em **07 de julho de 2023**.

**Conteúdo**

- [- Vídeo tutorial](#video-tutorial)
- 1[ - Requisitos](#requisitos)
- 2 [- Baixe o instalador do jogo:](#baixe-o-instalador-do-jogo)
- 3 [- Instalar o lutris](#instalar-o-lutris)
- 4 [- Baixar o runner:](#baixar-o-runner)
- 5 [- Criar a pasta do MIR4](#criar-a-pasta-do-mir4)
- 6 [- Criar uma configuração do MIR4](#criar-uma-configuração-do-mir4)
- 7 [- Selecionar o Modo Windows XP](#selecionar-o-modo-windows-xp)
- 8 [- Instalar o jogo e as dependências](#instalar-o-jogo-e-as-dependências)
- 9 [- Concluindo a configuração e abrindo o jogo](#concluindo-a-configuração-e-abrindo-o-jogo)
- [- Dica para quem já tem o jogo baixado](#dica-para-quem-já-tem-o-jogo-baixado)
- [- Problemas conhecidos](#problemas-conhecidos)
- 1 [- Navegador com o site do captcha não abre](#navegador-com-o-site-do-captcha-não-abre)
- 2 [- Tela de login preta](#tela-de-login-preta)
- 3 [- Quedas de FPS e engasgos](#quedas-de-fps-e-engasgos)
- 4 [- Jogo trava ao invocar livro/pet pela 2ª vez](#jogo-trava-ao-invocar-livropet-pela-2ª-vez)
- [- Considerações finais](#considerações-finais)

### Video tutorial:
Versão 2023
[Clique aqui para assistir no Youtube](https://youtu.be/ULk4E9Fa6E8)

Continuando...

## Requisitos:

Os seguintes requisitos são obrigatórios para o jogo funcionar:

-   Driver GPU com suporte ao Vulkan
-   Lutris
-   GE-Proton8-10 (runner)
-   Instalador do MIR4 (disponível no site oficial do MIR4)
-   Wine Mono (opcional)

O uso do **Wine Mono** só vai ser necessário se o jogo pedir pelo **.NET Framework 4.8**, mas não instale o .NET Framework 4.8 para evitar de quebrar o jogo, sempre use o Wine Mono **se** o jogo pedir pelo .NET Framework.

### Baixe o instalador do jogo:

Entre no site do Mir4 e faça o download do jogo standalone para Windows
[https://www.mir4global.com/](https://www.mir4global.com/)

Se preferir clique aqui para baixar diretamente o instalador do jogo
[https://live-dl.mir4global.com/global-launcher/Mir4Launcher_Install.exe](https://live-dl.mir4global.com/global-launcher/Mir4Launcher_Install.exe)

### Instalar o lutris:
Certo, primeiro trate de instalar o driver da placa de vídeo com suporte ao vulkan e baixar o Lutris, o lutris pode estar disponível nos repositórios oficiais da sua distrok.

Para baixar o lutris nos repositórios oficiais da sua distro:

	$ sudo apt install lutris # ubuntu e debian
	$ sudo dnf install lutris # fedora e redhat
	$ sudo zypper in lutris # opensuse
	$ sudo pacman -S lutris # arch linux

Depois disso basta abrir o lutris, para abrir ele basta procurar ele no menu de aplicativos na categoria “Jogos” ou rodar via terminar com o comando “lutris”

### Baixar o runner:
Ao abrir o lutris, vamos agora baixar o runner necessário para rodar o MIR4.

Com o lutris aberto, na barra lateral a esquerda, desça até a parte “runner” e clique no ícone destacado na imagem:

![selecionando versão do runner](/assets/img/posts/runner.png)

Após isso vai surgir uma janela com uma lista de runners disponíveis, desça até o final da página e baixe o runner **lutris-GE-Proton8–10** destacado na imagem abaixo:

![instalando a versão escolhida](/assets/img/posts/8-10.png)

Após baixar o runner, feche o lutris e reabra-o, com isso já podemos criar uma configuração exclusiva para o MIR4 no lutris.

### Criar a pasta do MIR4
Agora que já temos o runner necessário pra fazer o MIR4 funcionar, vamos criar uma pasta onde o MIR4 será instalado.

Você pode criar essa pasta em qualquer lugar, eu por exemplo instalei na minha pasta home

	/home/marcos/Mir4

![criando a nova pasta](/assets/img/posts/mirhome.png)

### Criar uma configuração do MIR4
Agora que já criamos a pasta para o MIR4, vamos agora criar uma configuração do jogo para o Lutris.

Volte para o Lutris e clique no botão "Adicionar jogo", que fica no canto superior esquerdo da tela, nós devemos escolher a ultima opção: "Adicionar jogo instalado localmente"":

![selecionando a opcao manual de instalação](/assets/img/posts/addgame.png)

Depois disso vai surgir uma tela com várias abas, primeiro vamos configurar a parte das **informações do jogo**.

Nessa parte você vai selecionar o tipo de runner e o nome do jogo que vai ser adicionado no Lutris.

Com base na imagem abaixo, o nome é Mir4 e o runner é o Wine:

![configurando informações do jogo](/assets/img/posts/gameinfo.png)

A próxima parte são as **opções de jogo**, nessa parte vamos selecionar aquela pasta que nós criamos, segue a imagem:

![selecionando as opções do jogo](/assets/img/posts/gameopcao.png)

Seguindo para a próxima parte nós vamos selecionar o runner que vai rodar o MIR4 e clicar em SALVAR:

![selecionando o runner](/assets/img/posts/opcaorunner.png)

### Selecionar o Modo Windows XP
Aqui vamos precisar utilizar o modo de compatibilidade e escolher o **Windows XP** para que o jogo funcione.

Clique no botão proximo ao icone de taça, indicado na imagem abaixo e clique em "Configuração do Wine"

Na proxima janela, em "Versão do Windows", escolha na lista o Windows XP. Clique em aplicar e depois em Ok para fechar.

![selecionando o modo windows xp](/assets/img/posts/modoxp.png)

### Instalar o jogo e as dependências
Depois de criar uma pasta para o jogo e também selecionar o modo Windows XP, vamos instalar o jogo pelo instalador.

Na tela inicial do lutris, clique no icone ao lado da taça e selecione a opção **Executar EXE dentro do prefixo do Wine**.

Isso vai abrir uma janela, basta selecionar o app "Mir4Launcher_Install.exe" e fazer a instalação do jogo.

![Instalador do jogo](/assets/img/posts/mir4installer.png)

Depois de instalar o jogo, vamos agora executar o instalador "UE4PrereqSetup_x64.exe" que vém com o jogo, ele traz as dependencias vcrun2017 (Visual Studio).

Na tela inicial do lutris, clique no icone ao lado da taça e selecione a opção "Executar EXE dentro do prefixo do Wine".

Agora vamos precisar entrar nesse diretório e encontrar o app de instalação:

> _/home/marcos/Mir4/drive_c/Wemade/Mir4Global/Mir4Launch/Resources/_**_UE4PrereqSetup_x64.exe_**

Com isso vai aparecer o instalador, faça a instalação normalmente.

![instalador UE4PrereqSetup](/assets/img/posts/ueprereqsetup.png)

Basta instalar normalmente.

### Concluindo a configuração e abrindo o jogo
Chegamos na ultima parte, vamos abrir as configurações do lutris novamente e selecionar o launcher do jogo.

Basta voltar para a tela inicial do Lutris, selecionar o jogo e selecionar a opção **Configurar**.

Ao abrir a nova janela, vamos para a aba **Opções de jogo** e selecionar o launcher do jogo.

Após selecionar o executavel do launcher, clique em **Salvar**.

De acordo com a imagem a baixo, o local do launcher é:

> _/home/marcos/Mir4/drive_c/Wemade/Mir4Global/Mir4Launcher/_**_Mir4Launcher.exe_**

![voltando nas configurações](/assets/img/posts/addlauncher.png)

Terminando essa parte basta clicar em **Jogar** que o launcher vai abrir.

Assim que o launcher abrir, a proxima tarefa é clicar em **Options** e selecionar o modo **OpenGL**.

![selecionando modo opengl no launcher](https://cdn-images-1.medium.com/max/800/0*8-SyT_xcGTz2Pt_r.jpg)

Depois de fazer isso pode fechar a janela e clicar em **Install**.

Certamente isso é o suficiente para que o jogo abra e baixe os demais arquivos sem nenhum problema.

**Terminamos**.

Se a tela de login ficar preta, siga essa dica:


## Dica para quem já tem o jogo baixado
Se assim como eu você jogou o MIR4 pelo Windows antes de usar Linux, ou ficou jogando no Windows esperando pelo momento em que o MIR4 também rodasse no Linux, você deve ter o jogo completo.

Pra evitar que você baixe tudo de novo jogando pelo Linux, você pode simplesmente copiar a pasta **Wemade** que está junto com o Windows e colar no diretório abaixo:

> _/home/seu_user/Mir4/_**_drive_c/_**

Nota: Faça a cópia depois de instalar o launcher pelo Lutris

## Problemas conhecidos
Vale lembrar que estamos rodando o MIR4 em outro sistema e por isso vai haver alguns problemas com o jogo, a seguir eu vou listar os problemas já conhecidos do MIR4 no Linux.

Conforme novas versões do **proton** são lançadas, os problemas atuais podem desaparecer.

### Navegador com o site do captcha não abre
No Windows quando abrimos o MIR4 o jogo automaticamente abre uma nova página com o site do captcha, no Linux o problema é que o jogo não abre o navegador e quando isso acontece nós ficamos presos nessa tela:

![janela com erro de autenticação](https://cdn-images-1.medium.com/max/800/0*omi5Ceys_ZXvbEVz.jpg)

Esse é um problema com o runner, você consegue resolver escolhendo outra versão do runner, aqui no caso não houve esse problema com o ProtonGE8-10.

Observação: Se o problema acontece até no runner recomendado neste artigo, verifique em sua distribuição se o browser que você usa é o browser padrão para navegação.

### Tela de login preta:
Além do problema de captcha também temos um problema mais complicado que é na tela de logar com a conta do Google, Facebook e Apple.

Com esse problema você fica com uma tela preta que não deixa você fazer login, igual na imagem abaixo:

![bug tela de login preta](https://cdn-images-1.medium.com/max/800/0*2pac_eLHryiYO-3v.jpg)

Como podem ver não há como fazer login com essa tela. Para contornar esse problema nós devemos abrir o MIR4 no Windows mesmo, e de lá copiar os arquivos que são usados no login para o Linux.

O processo é simples, reinicie o seu PC e dê boot no Windows, abra o jogo e faça login normalmente.

Após selecionar o servidor e o personagem, assim que você entrar no mapa, feche o jogo.

Após fechar o jogo, vá no Windows Explorer e acesse essa pasta:

> _C:\Wemade\Mir4Global\Mir4Client\MirMobile\SaveData\Saved_

Ao entrar nessa pasta, basta copiar todos os arquivos e substituir eles na pasta:

> _/home/seu_user/Mir4/drive_c/Wemade/Mir4Global/Mir4Client/MirMobile/SaveData/Saved_

Na verdade, após logar no jogo usando o Windows você só precisa reiniciar o PC e dar boot no Linux, e do linux você pode pegar os arquivos na partição do Windows e colar na pasta MIR4 do lutris.

Dependendo do runner, substituir os arquivos não vai ajudar, caso aconteça com você tente outro runner e tente novamente o processo.

Depois de fazer isso o jogo não vai pedir para você logar na conta de novo.

Esse problema de tela preta também vai aparecer ao tentar fundir o DRACO, infelizmente não há como contornar isso no Linux e por isso você deve mexer com draco pelo Windows mesmo. 😐

### Quedas de FPS e engasgos
Esse é um problema que acontece, mas só dura nos primeiros minutos de jogo, acredito que seja uma característica do OpenGL, após alguns minutos o jogo roda tranquilamente.

Observado também que o problema começa a acontecer no Ubuntu 22.04, até a versão 20.04 LTS o jogo roda com um ótimo desempenho.

### Jogo trava ao invocar livro/pet pela 2ª vez
Esse é um problema sem solução, ele acontece ao tentar invocar espíritos e pets nas invocações diárias, aquelas que custam 60k, 120k e 240k de cobre:

![screenshot da invacao de espiritos](https://cdn-images-1.medium.com/max/800/0*V9F2ZVvuMJRM2xhh.jpg)

**Causa do problema:** O jogo trava se der um clique rápido no botão de sair

**Solução:** Ao apertar no botão **sair**, segure um pouco o clique no botão, evite de dar um clique rápido no botão de sair. Testado com lutris-GE-Proton7–16 e sem problemas seguindo esse conselho.

## Considerações finais:
Bom pessoal, esse foi o tutorial completo de MIR4 rodando no Linux, estamos quase lá gente, não falta muito para o jogo funcionar tão bem no Linux como funciona no Windows.

Eu vi muita gente tentando sem sucesso e estou aqui pra compartilhar o método que funciona, espero ter ajudado.
