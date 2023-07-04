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

Este artigo foi atualizado pela ultima vez em **14 de junho de 2022**.

**Conteúdo**

- [- Vídeo tutorial](#video-tutorial)
- 1[ - Requisitos](#requisitos)
- 2 [- Instalar o lutris](#instalar-o-lutris)
- 3 [- Baixar o runner](#baixar-o-runner)
- 4 [- Criar a pasta do MIR4](#criar-a-pasta-do-mir4)
- 5 [- Criar uma configuração do MIR4](#criar-uma-configuração-do-mir4)
- 6 [- Selecionar o Modo Windows XP](#selecionar-o-modo-windows-xp)
- 7 [- Instalar as dependências](#instalar-as-dependências)
- 8 [- Concluindo a configuração e abrindo o jogo](#concluindo-a-configuração-e-abrindo-o-jogo)
- [- Dica para quem já tem o jogo baixado](#dica-para-quem-já-tem-o-jogo-baixado)
- [- Problemas conhecidos](#problemas-conhecidos)
- 1 [- Navegador com o site do captcha não abre](#navegador-com-o-site-do-captcha-não-abre)
- 2 [- Tela de login preta](#tela-de-login-preta)
- 3 [- Quedas de FPS e engasgos](#quedas-de-fps-e-engasgos)
- 4 [- Jogo trava ao invocar livro/pet pela 2ª vez](#jogo-trava-ao-invocar-livropet-pela-2ª-vez)
- [- Considerações finais](#considerações-finais)

### Video tutorial:
[Clique aqui para assistir no Youtube](https://www.youtube.com/watch?v=pjXF-8MocwA)

Continuando...

## Requisitos:

Os seguintes requisitos são obrigatórios para o jogo funcionar:

-   **Driver de vídeo com suporte ao Vulkan** instalado (Driver 510 ou 470 da Nvidia)
-   **Lutris**
-   **GE-Proton7–16** (runner)
-   **Instalador do MIR4** (disponível no site oficial do MIR4)
-   **Wine Mono**
-   Pacote **winetricks**

No momento os requisitos são apenas esses, ainda é necessário instalar o **vcrun2017** mas durante o tutorial esse componente será instalado.

Vale lembrar que o uso do **Wine Mono** só vai ser necessário se o jogo pedir pelo .NET Framework 4.8, mas **não instale o .NET Framework 4.8** para evitar de quebrar o jogo, sempre use o Wine Mono se o jogo pedir pelo .NET Framework.

### Instalar o lutris:
Certo, primeiro trate de instalar o driver da placa de vídeo com suporte ao vulkan e baixar o Lutris, o lutris pode estar disponível nos repositórios oficiais da sua distro e também em flatpak.

Para baixar o lutris nos repositórios oficiais do Ubuntu, Mint e Linux Debian o comando no **Terminal** é esse:

	$ sudo apt update
	$ sudo apt install lutris

Isso vai baixar o lutris e até itens adicionais como o winetricks, é importante que o winetricks também esteja instalado pois será necessário, use o comando abaixo para instalar o winetricks:

	$ sudo apt install winetricks

Depois disso basta abrir o lutris, para abrir ele basta procurar ele no menu de aplicativos na categoria “Jogos” ou rodar via terminar com o comando “lutris”

### Baixar o runner:
Ao abrir o lutris, vamos agora baixar o runner necessário para rodar o MIR4.

Com o lutris aberto, na barra lateral a esquerda, desça até a parte “runner” e clique no ícone destacado na imagem:

![selecionando versão do runner](https://cdn-images-1.medium.com/max/800/0*bqf0ddITlBqig2ne.jpg)

Após isso vai surgir uma janela com uma lista de runners disponíveis, desça até o final da página e baixe o runner **lutris-GE-Proton7–16** destacado na imagem abaixo:

![instalando a versão escolhida](https://cdn-images-1.medium.com/max/800/0*3eyV94Ye5UFV3yjX.jpg)

Após baixar o runner, feche o lutris e reabra-o, com isso já podemos criar uma configuração exclusiva para o MIR4 no lutris.

### Criar a pasta do MIR4
Agora que já temos o runner necessário pra fazer o MIR4 funcionar, vamos criar um prefixo do MIR4 no lutris.

Abra o seu gerenciador de arquivos como o Nautilus ou Nemo (depende da distro) e vá na sua pasta Home ou pasta Pessoal.

Ao entrar na pasta, ative a visualização de arquivos ocultos, pra fazer isso basta usar a combinação de teclas “**Ctrl + H**”.

Após fazer isso, vamos entrar nas seguintes pastas:

**~/.local/share/wineprefixes**

![criando a nova pasta](https://cdn-images-1.medium.com/max/800/0*_R2-HDHJiardnEvD.jpg)

Dentro da pasta **wineprefixes** vamos criar uma nova pasta, essa nova pasta pode se chamar **MIR4**, independente do nome essa pasta será o local onde ficará o jogo junto com os arquivos do runner.

### Criar uma configuração do MIR4
Agora que já criamos a pasta para o MIR4, vamos agora criar uma configuração do jogo para o Lutris.

Volte para o Lutris e clique no botão **adicionar jogo**, que fica no canto superior esquerdo da tela, veja na imagem:

![adicionando o jogo no lutris](https://cdn-images-1.medium.com/max/800/0*9ftVpTJvb2F8gUEe.jpg)

Isso vai abrir uma janela com várias opções, nós devemos escolher a ultima: **Adicionar jogo instalado localmente**:

![selecionando a opcao manual de instalação](https://cdn-images-1.medium.com/max/800/0*JaPqWwETEtnjthh4.jpg)

Depois disso vai surgir uma tela com várias abas, primeiro vamos configurar a parte das **informações do jogo**.

Nessa parte você vai selecionar o tipo de runner e o nome do jogo que vai ser adicionado no Lutris.

Com base na imagem abaixo, o nome pode ser **MIR4** e o runner deve ser o **Wine**:

![configurando informações do jogo](https://cdn-images-1.medium.com/max/800/0*lnzguLOEQbwWXud-.jpg)

A próxima parte são as **opções de jogo**, nessa parte vamos selecionar aquela pasta que nós criamos em wineprefixes e selecionar o instalador do MIR4 que no qual é baixado no site oficial, segue a imagem:

![selecionando as opções do jogo](https://cdn-images-1.medium.com/max/800/0*WdpAEfhQ17mGQfgT.jpg)

Seguindo para a próxima parte nós vamos selecionar o runner que vai rodar o MIR4, nessa parte vamos selecionar aquele runner que baixamos no começo do tutorial e clicar em **SALVAR**:

![selecionando o runner](https://cdn-images-1.medium.com/max/800/0*P-06G9Q3UxNvxZcy.jpg)

Após clicar em salvar, voltando pra tela inicial do lutris, basta selecionar o MIR4 e clicar em **Jogar**.

Isso vai abrir o instalador do MIR4, faça a instalação normalmente, você só precisa clicar em **Next** até concluir a instalação.

### Selecionar o Modo Windows XP
Com isso já preparamos o lutris para instalar o MIR4, mas ainda falta outra configuração que vai ser importante.

Aqui vamos precisar utilizar o modo de compatibilidade e escolher o **Windows XP** pelo Winetricks, o jogo não funciona nos outros modos.

Clique no botão proximo ao icone de taça, indicado na imagem abaixo e clique em Winetricks

![abrindo o winetricks](https://cdn-images-1.medium.com/max/800/0*9oXk8BOmLMB5vT1f.jpg)

Ao fazer isso o Winetricks vai abrir, basta selecionar a opção **MIR4** e clicar em **OK**, que é o nome da pasta que nós criamos dentro da pasta **wineprefixes**.

![selecionando o prefixo do jogo](https://cdn-images-1.medium.com/max/800/0*AKvdpQsxvQnAJVjq.jpg)

Agora selecione a opção **Alterar configurações** e clique em **OK**.

![selecionando a opção alterar configurações](https://cdn-images-1.medium.com/max/800/0*AUx6l7eHGMuJVWGv.jpg)

Agora desça até o final da página e selecione a opção **winxp** e clique em **OK**.

### Instalar as dependências
O MIR4 depende do vcrun2017 e felizmente o instalador do MIR4 já trás essa dependencia com ele, nós só precisamos abrir o **UE4PrereqSetup_x64.exe** que vai instalar o vcrun2017 e outras dependencias do motor gráfico do jogo.

Na tela inicial do lutris, clique no icone ao lado da taça e selecione a opção **Executar EXE dentro do prefixo do Wine**.

![executar exe dentro do prefixo](https://cdn-images-1.medium.com/max/800/0*Wq17Rqin13NuSzez.jpg)

Agora vamos precisar entrar nesse diretório e encontrar o app de instalação:

> _~/.local/share/wineprefixes/MIR4/drive_c/Wemade/Mir4Global/Mir4Launch/Resources/_**_UE4PrereqSetup_x64.exe_**

Com isso vai aparecer o instalador, faça a instalação normalmente.

![instalador UE4PrereqSetup](https://cdn-images-1.medium.com/max/800/0*D9L5Cx7nNAVLzhUZ.jpg)

### Concluindo a configuração e abrindo o jogo
Chegamos na ultima parte, vamos abrir as configurações do lutris novamente e selecionar o launcher do jogo.

Basta voltar para a tela inicial do Lutris, selecionar o jogo e selecionar a opção **Configurar**.

![voltando nas configurações](https://cdn-images-1.medium.com/max/800/0*VL_KKGn2oOZVXAtB.jpg)

Ao abrir a nova janela, vamos para a aba **Opções de jogo** e selecionar o launcher do jogo.

De acordo com a imagem a baixo, o local do launcher é:

> _~/.local/share/wineprefixes/MIR4/drive_c/Wemade/Mir4Global/Mir4Launcher/_**_Mir4Launcher.exe_**

Após selecionar o executavel do launcher, clique em **Salvar**.

![selecionando o executavel do launcher](https://cdn-images-1.medium.com/max/800/0*P282qYgEMc6GMC3w.jpg)

Terminando essa parte basta clicar em **Jogar** que o launcher vai abrir.

Após o launcher abrir, ele vai informar que há nova atualização e depois de clicar em OK ele vai fechar e reabrir sozinho após a barra de progresso enxer.

![pop up de carregamento](https://cdn-images-1.medium.com/max/800/0*dFEkGRNE22SpX9cH.jpg)

Assim que o launcher abrir, a proxima tarefa é clicar em **Options** e selecionar o modo **OpenGL**.

![selecionando modo opengl no launcher](https://cdn-images-1.medium.com/max/800/0*8-SyT_xcGTz2Pt_r.jpg)

Depois de fazer isso pode fechar a janela e clicar em **Install**.

Certamente isso é o suficiente para que o jogo abra e baixe os demais arquivos sem nenhum problema.

**Terminamos**.

## Dica para quem já tem o jogo baixado
Se assim como eu você jogou o MIR4 pelo Windows antes de usar Linux, ou ficou jogando no Windows esperando pelo momento em que o MIR4 também rodasse no Linux, você deve ter o jogo completo.

Pra evitar que você baixe tudo de novo jogando pelo Linux, você pode simplesmente copiar a pasta **Wemade** que está junto com o Windows e colar no diretório abaixo:

> _~/.local/share/wineprefixes/MIR4/_**_drive_c/_**

Nota: Faça a cópia depois de instalar o launcher pelo Lutris

## Problemas conhecidos
Vale lembrar que estamos rodando o MIR4 em outro sistema e por isso vai haver alguns problemas com o jogo, a seguir eu vou listar os problemas já conhecidos do MIR4 no Linux.

Conforme novas versões do **proton** são lançadas, os problemas atuais podem desaparecer.

### Navegador com o site do captcha não abre
No Windows quando abrimos o MIR4 o jogo automaticamente abre uma nova página com o site do captcha, no Linux o problema é que o jogo não abre o navegador e quando isso acontece nós ficamos presos nessa tela:

![janela com erro de autenticação](https://cdn-images-1.medium.com/max/800/0*omi5Ceys_ZXvbEVz.jpg)

Esse é um problema com o runner, eu havia testado outros runners como por exemplo o **lutris-fshack-7.2** e nele o navegador não abre com o captcha, mas no runner lutris-GE-Proton7–16 esse problema não acontece.

Observação: Se o problema acontece até no runner recomendado neste artigo, verifique em sua distribuição se o browser que você usa é o browser padrão para navegação.

### Tela de login preta:
Além do problema de captcha também temos um problema mais complicado que é na tela de logar com a conta do Google, Facebook e Apple.

Com esse problema você fica com uma tela preta que não deixa você fazer login, igual na imagem abaixo:

![bug tela de login preta](https://cdn-images-1.medium.com/max/800/0*2pac_eLHryiYO-3v.jpg)

Como podem ver não há como fazer login com essa tela. Para contornar esse problema nós devemos abrir o MIR4 no Windows mesmo, e de lá copiar os arquivos que são usados no login para o Linux.

O processo é simples, reinicie o seu PC e dê boot no Windows, abra o jogo e faça login normalmente.

Após selecionar o servidor e o personagem, assim que você entrar no mapa, feche o jogo.

Após fechar o jogo, vá no Windows Explorer e acesse essa pasta:

> _C:\Wemade\Mir4Global\Mir4Client\MirMobile\SaveData\Saved\SaveGames_

Ao entrar nessa pasta, basta copiar todos os arquivos e substituir eles na pasta:

> _~/.local/share/wineprefixes/MIR4/drive_c/Wemade/Mir4Global/Mir4Client/MirMobile/SaveData/Saved/SaveGames_

Na verdade, após logar no jogo usando o Windows você só precisa reiniciar o PC e dar boot no Linux, e do linux você pode pegar os arquivos na partição do Windows e colar na pasta MIR4 do lutris.

Para ser mais exato os arquivos de login são:

-   **AccountLocalSave1.sav**
-   **AccountLocalSave2.sav**

Mas por via das dúvidas é bom copiar tudo.

Dependendo do runner, substituir os arquivos não vai ajudar, esse problema também acontece com o runner **lutris-fshack-7.2**, mas no runner lutris-GE-Proton7–16 esse problema não acontece.

Uma vez que você tenha esses arquivos, se esse problema acontecer novamente basta fechar e abrir o jogo novamente que ele não vai pedir para você logar na conta de novo, se não resolver na 2ª tentativa tente logar com o Windows e passar os arquivos acima para o Linux novamente.

Esse problema também aparece ao tentar fundir o DRACO, infelizmente não há como contornar isso no Linux e por isso você deve mexer com draco pelo Windows mesmo. 😐

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
