---
title: Como instalar Windows 11 sem TPM 2.0 em qualquer PC
date: 2023-07-02
author: M4rQu1Nh0S
tags: [como, instalar, windows 11, sem tpm, em, qualquer, computador]
subtitle: Aprenda a instalar o Windows 11 em qualquer PC
categories: [dicas e tutoriais, windows 11]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*fRMgrP8Nzaimzegq.png
share-img: https://cdn-images-1.medium.com/max/800/0*fRMgrP8Nzaimzegq.png
layout: post
---

<p align='center'><img alt='Logo Windows 11' src="https://cdn-images-1.medium.com/max/800/0*fRMgrP8Nzaimzegq.png"/></p>
**Novidade:** Criei recentemente um novo post compartilhando uma **ISO já pronta** com o Windows 11 sem TMP, [**clique aqui**](https://marcosfs93.github.io/2023-07-02-windows-11-2h22-iso-modificada-sem-tpm/) para saber mais!

Eu uso o Windows desde a época do XP, até o Windows 10 teve historias de incompatibilidades de hardware, mas todas as edições do Windows contavam com requisitos comuns: Processador de tal frequência ou superior… Tantos GB de memória RAM… Determinado espaço disponível no HD… etc, requisitos até simples.

### Conteúdo

- [Windows 11 e seu novo requisito obrigatório](#windows-11-e-seu-novo-requisito-obrigatório)
- [Baixe as ISOs](#baixe-as-isos)
- [- Windows 10](#windows-10)
- [- Windows 11](#windows-11-dev-channel)
- [Como criar uma ISO do Windows 11 sem o recurso TPM obrigatório](#como-criar-uma-iso-do-windows-11-sem-o-recurso-tpm-obrigatório)
- 1[. Extrair o arquivo install.wim do Windows 11](#1-extrair-o-arquivo-installwim-do-windows-11)
- 2[. Escolha a edição do Windows para extrair](#2-escolha-a-edição-do-windows-para-extrair)
- 3[. Faça a extração da edição que foi escolhida](#3-faça-a-extração-da-edição-que-foi-escolhida)
- 4[. Adicione a edição do Windows 11 para a ISO do Windows 10](#4-adicione-a-edição-do-windows-11-para-a-iso-do-windows-10)
- 5[. Grave a ISO modificada para o seu pendrive](#5-grave-a-iso-modificada-para-o-seu-pendrive)
- 6[. Reinicie o PC e faça o boot do Instalador do Windows](#6-reinicie-o-pc-e-faça-o-boot-do-instalador-do-windows)
- [Minhas impressões sobre o sistema](#minhas-impressões-sobre-o-sistema)

## Windows 11 e seu novo requisito obrigatório

O Windows 11 veio com um grande requisito que na qual somente alguns PCs tem tal atributo, o **TPM 2.0**. Eu não lembro ao certo, mas o Windows 10 tinha o requisito do **TPM 1.2**, mas pelo que me lembro não era tão difícil instalar o Windows 10 como está sendo hoje com o Windows 11.

Eu digo isso porque eu tentei diversos tutoriais em portugues pra fazer a instalação e não dava certo, no final eu acabei achando a solução no site **nerdschalk.com**, um site gringo.

Se você também tentou vários sites e não conseguiu instalar o Windows 11… Eu estou aqui com uma nova alternativa e que parece funcionar em qualquer PC, não vamos depender de coisas como mexer no regedit e nem mexer com a tal dll appraiserres.dll.

O método para poder instalar o Windows 11 no PC é **modificando a ISO do Windows 10.**

## Baixe as ISOs:

Infelizmente você terá que baixar duas ISOs (caso não tenha), uma do Windows 10 e outra do Windows 11. O que vamos fazer aqui é transferir o arquivo com Windows 11 e substituir o arquivo existente na ISO do Windows 10, mas calma, pois eu vou explicar em etapas.

Vamos aos procedimentos. Baixe as ISOs de acordo com o link abaixo:

**A** **ISO do Windows 10 PRECISA ser em ingles**. Se você usar o arquivo do Windows 11 (que só está em ingles) em uma ISO de Windows 10 em Portugues a instalação não vai dar certo. **Ambos as ISOs precisam estar em ingles!**

### Windows 10:

-   [ISO Windows 10 Ghost Spectre](https://ouo.io/9iXagA)
    Essa ISO é uma versão modificada do Windows 10 serve muito bem para Instalar o Windows 11

Caso não confie nessas ISOs modificadas, acesse o site da microsoft para baixar o Windows 10 em inglês

### Windows 11 Dev Channel:

-   [Download da ISO do Windows 11](https://ia801503.us.archive.org/25/items/win11build21996/21996.1.210529-1541.co_release_CLIENT_CONSUMER_x64FRE_en-us%20%281%29.iso)
-   [Download da ISO do Windows 11 (link 2)](https://ia801503.us.archive.org/25/items/win11build21996/21996.1.210529-1541.co_release_CLIENT_CONSUMER_x64FRE_en-us%20%281%29.iso)
-   [Download 64 Bits via Google Drive](https://ia801503.us.archive.org/25/items/win11build21996/21996.1.210529-1541.co_release_CLIENT_CONSUMER_x64FRE_en-us%20%281%29.iso)
-   [Download via Google Driver (link 2)](https://drive.google.com/file/d/1DJAJFNINnLrgQBC5PJ2RhYoNOL-qnVa_/view)
-   [Download via Mega](https://mega.nz/folder/XDoGDYKJ#oQ23isfPIL8cKXr1r0-Rvw)

_Links divulgados pelo site_ [tnteu.in](https://tnteu.in/windows-11-iso-file-download.html) (créditos)

A seguir você acompanhará as instruções de modificação da ISO do Windows 10 com o objetivo de instalar o Windows 11 sem restrições.

> _Se quiser ler a_ postagem completa e original, aqui o link:

> [_Windows 11 Without TPM: How To Bypass the TPM Requirement and Install the OS_](https://nerdschalk.com/windows-11-without-tpm-how-to-bypass-tpm-requirement-and-install-the-os/#case-2-bypass-tpm-when-installing-using-an-iso-file)

## Como criar uma ISO do Windows 11 sem o recurso TPM obrigatório.

### 1. Extrair o arquivo install.wim do Windows 11

Abra a ISO do Windows 11, na pasta **source** vai existir o arquivo **install.wim**

Ao encontrar o arquivo, extrair ele em para uma nova pasta. Recomendo que extraia esse arquivo na pasta:
_*C:\WimMod*_

Agora que o **install.wim** está dentro da pasta **C:\WimMod**, abra o CMD como **Administrador**

_Ele pode ser executado através do Win+S e digitando a palavra “CMD”_

### 2. Escolha a edição do Windows para extrair

Após o CMD abrir, digite o comando abaixo e depois tecle ENTER

    cd C:\WimMod

e depois execute esse comando:

    dism /Get-WimInfo /WimFile:C:\WimMod\install.wim

Ao fazer isso o CMD vai listar todas as edições que estão disponíveis dentro desse arquivo, **cada edição tem um INDEX de indicação**, veja a imagem abaixo:

![janela do cmd mostrando a lista Index](https://cdn-images-1.medium.com/max/800/0*D78y_4UXwJ9Kyco1.png)

Reprodução: [https://nerdschalk.com](https://nerdschalk.com/)

Observe que em **Index : 1** o nome da edição é **Windows 11 Home**, **Index 2** é o **Windows 11 Home N**, a **Index 3** é **Windows 11 Home Single Language…** e assim segue o esquema.

É necessário que você decore o Index do Windows 11 Pro que na qual é a edição que eu recomendo instalar, Aqui o Index dele é **Index : 6** (**Indice : 6**). Na janela do CMD do seu PC decore o numero de index do Windows **Pro**.

Vamos continuar:

### 3. Faça a extração da edição que foi escolhida

Digite o comando abaixo e aperte Enter:

    dism /export-image /SourceImageFile:"C:\WimMod\install.wim" /SourceIndex:6 /DestinationImageFile:"C:\WimMod\install.esd" /Compress:recovery /CheckIntegrity

**_Lembre-se, no comando acima o “/SourceIndex:” eu coloquei 6, pois é referente ao Windows 11 Pro_**  **_que eu tenho_**_, se no seu caso_ **_seu CMD apresentou outro numero, coloque-o no lugar do 6_** _(Exemplo:_ `_/SourceIndex:7_` _)_

Aperte a tecla **Enter** para executar um comando que vai exportar a edição escolhida, esse arquivo novo será o **Install.esd**.

Depois de executar o comando acima, o CMD vai realizar a extração do Windows 11. Esse novo arquivo **Install.esd** vai estar dentro da pasta **C:\WimMod** (ou outra pasta que você escolheu).

### 4. Adicione a edição do Windows 11 para a ISO do Windows 10.

Vamos pegar esse arquivo **Install.esd** e vamos adiciona-lo na **ISO do Windows 10**.

Para fazer isso precisamos usar programas que permitam modificar uma ISO e poder grava-la com as alterações, nesse exemplo vou usar o **Ultra ISO**.

Abra o Ultra ISO e entre na ISO do Windows 10. Em seguida entre no diretório **Sources** e aí apague o arquivo **Install.ESD ou Install.WIM** que já está lá.

![deletar o arquivo antigo](https://cdn-images-1.medium.com/max/800/1*QCpocELK0PfHUSkFsHCVCg.png)

Agora vamos navegar na pasta C:\WimMod e adicionar **o novo** Install.ESD para dentro da ISO do Windows 10, no local onde tava o antigo Install.ESD/WIM.

![Adicionar o novo arquivo.](https://cdn-images-1.medium.com/max/800/1*ObJZefmZ3XIWme6erym24A.png)

Salve as alterações com **Ctrl + S** e espere o Ultra ISO salvar a imagem de disco do Windows 10.

![Clique em salvar](https://cdn-images-1.medium.com/max/800/0*mDw3JEd-GDz92u4d.png)

Basicamente é isso, qualquer programa que permita alterar arquivos dentro de uma ISO é capaz de criar um disco de instalação do Windows 11, ImgBurn é outro exemplo de app capaz de realizar essa tarefa.

### 5. Grave a ISO modificada para o seu pendrive

Depois que o Ultra ISO terminar de salvar as alterações na ISO, use o programa **Rufus** ou qualquer outro que grave a ISO num pendrive com o **formato GPT**, já que a instalação **só pode ser feita em UEFI**

![print do rufus](https://cdn-images-1.medium.com/max/800/1*o1Lg7-yMXWvf2zTC8msBCQ.png)

Ao abrir o Rufus, basta clicar em **Select** e selecionar a ISO modificada do Windows 10 (Windows 11, na verdade)

Depois em **Dispositivo** selecione o Pendrive que você vai gravar a ISO

E por Ultimo clique no botão **INICIAR** para iniciar a gravação da ISO.

Quando terminar, reinicie o PC e pelo menu da BIOS selecione o Pendrive **no Modo UEFI**

### 6. Reinicie o PC e faça o boot do Instalador do Windows

Essa parte você já conhece, instale o Windows normalmente, a instalação vai dar a sensação de que você está instalando o Windows 10. Mas na verdade é só o visual do instalador é de Windows 10 mas… quando você acabar de completar a primeira parte de instalação e reiniciar o PC… Você verá o Windows 11 dando continuidade na instalação.

**Esse post ainda vai passar por alterações conforme necessário.**

## Minhas impressões sobre o sistema:

O Windows 11 mesmo no estágio beta está me impressionando, a velocidade do sistema é a evolução mais nítida que eu tive além do belo visual do sistema. É importante manter a ISO original do Windows 11 pois pode ter recursos no futuro que vão depender da ISO do Windows 11. até o próximo post!

