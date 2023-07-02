---
title: Método alternativo para instalar o Windows
date: 2023-07-02
author: M4rQu1Nh0S
tags: [metodo, alternativo, instalar, windows, winntsetup]
subtitle: Conheça outra forma de instalar o Windows
category: [Dicas e tutoriais, Windows]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*UNEI9_isS64RuAlA.png
share-img: https://cdn-images-1.medium.com/max/800/0*UNEI9_isS64RuAlA.png
layout: post
---

![](https://cdn-images-1.medium.com/max/800/0*UNEI9_isS64RuAlA.png)<br/>
As vezes, dependendo das circunstâncias, não é possível instalar o Windows e no geral os problemas são referentes ao disco que será usado para instalar o sistema.

Se você tem mais de um HD/SSD e algum deles estiver em algum formato não suportado pelo Windows, você não conseguirá fazer a instalação, mesmo que o HD a ser usado seja diferente, mas essa não é uma regra e dependendo do dispositivo você pode não passar por problemas.

Mas se você está tentando instalar o Windows e de alguma forma você não está conseguindo, por causa do Instalador apresentando erros, eu estou aqui pra compartilhar um outro método de se instalar o Windows, através da ferramenta **WinNTSetup**.

**Conteúdo**

- 1[. Tutorial em vídeo](#tutorial-em-vídeo)
- 2[. Requisitos](#requisitos)
- 3[. Links de Download](#links-de-download)
- 4[. Crie uma Live CD](#crie-uma-live-cd)
- 5[. Instalando o Windows com o WinNTSetup](#instalando-o-windows-com-o-winntsetup)
- 5.1[. Sistema BIOS Legado](#sistema-bios-legado)
- 5.2[. Sistema UEFI](#sistema-uefi)
- [- Considerações finais](#considerações-finais)

## Tutorial em vídeo:
[Se preferir, clique aqui para assitir o tutorial no YouTube](https://www.youtube.com/watch?v=bDkzT9v8lCI)

Continuando...

## Requisitos:
Nesse tutorial nós vamos usar os seguintes itens:

1. **PowerISO Portable**, para manipular arquivos **.ISO**.
2. **WinNTSetup**, para instalar o Windows.
3. **AOMEI PE Builder**,para criar uma “live cd” do Windows.
4. **ISO do Windows**, o disco de instalação do Windows.

## Links de Download:

### PowerISO Portable:
[https://www.poweriso.com/download.htm](https://www.poweriso.com/download.htm)

### WinNTSetup:
[https://www.majorgeeks.com/files/details/winntsetup.html](https://www.majorgeeks.com/files/details/winntsetup.html)

### AOMEI PE Builder:
[https://www.ubackup.com/pe-builder.html](https://www.ubackup.com/pe-builder.html)

### ISO do Windows:
[Windows 11](https://www.microsoft.com/pt-br/software-download/windows11)
[Windows 10](https://www.microsoft.com/pt-br/software-download/windows10ISO)

Outras versões podem ser encontradas no site da Microsoft.

## Crie uma Live CD

1- Faça o download de todos os itens requisitados e instale o **AOMEI PE Builder**.

2- Extraia os arquivos .rar referentes ao **PowerISO Portable** e **WinNTSetup**.

3- Execute o app PowerISO e abra o arquivo .ISO do Windows

4- Após isso acesse o diretório **Sources** e de lá vamos extrair o arquivo **install.wim** ou **install.esd** que estiver presente, para extrair selecione o arquivo e clique em **Extract** e então clicar em **Ok**.

Selecione o local onde será extraído o arquivo, pode ser na Área de trabalho por exemplo.

![](https://cdn-images-1.medium.com/max/800/0*azDKTN5_RShDRkn1.png)

5- Agora vamos abrir o app **AOMEI PE Builder**, assim que o programa abrir clique em **Next** até chegar nessa parte:

![](https://cdn-images-1.medium.com/max/800/0*3w6RVHfpov1HxqnY.png)

Aqui vamos selecione a arquitetura 32 ou 64 bits do Windows PE (Live CD, entre áspas) e depois clicar em **Next**.

6- Enquanto isso, vá na pasta onde você extraiu o WinNTSetup e execute o app dele, vamos precisar fazer o download dos arquivos necessários, aqui é só clicar em **Ok**.

![](https://cdn-images-1.medium.com/max/800/0*pv42cQOYelO9HX7x.png)

7- Depois disso o WinNTSetup vai aparecer, e então clicamos em sair, pois o objetivo aqui era apenas obter os arquivos necessários para o app rodar sem problemas.

8- Voltando ao AOMEI PE Builder, devemos estar nessa parte:

![](https://cdn-images-1.medium.com/max/800/0*cXXoQyM3U3G7ZXSE.png)

Nessa parte devemos clicar em **Add Files**, e na mini janela que vai aparecer em seguida devemos selecionar a pasta onde o WinNTSetup.rar foi extraído.

No final teremos algo parecido com isso:

![](https://cdn-images-1.medium.com/max/800/0*N8cEsLF_3fb9YpQx.png)

Após adicionar a pasta com o WinNTSetup, clique em **Ok**.

9- Por fim chegaremos nessa parte, aqui vamos escolher a ultima opção e selecionar o local onde será criado a iso da livecd, escolha o local e o nome do arquivo .iso.

No caso será livecd.iso e será salva na Desktop:

![](https://cdn-images-1.medium.com/max/800/0*MtWf5NLAaWKUk6-o.png)

Clique em **Next** e o programa vai começar a criar o arquivo .iso.

O processo pode demorar alguns minutos, já que além de ser criado o arquivo .iso, o app também vai baixar recursos da internet, portanto esteja conectado.

10- Depois de terminar, vamos abrir o arquivo **livecd.iso** no PowerISO, aqui vamos simplesmente adicionar o arquivo **install.wim** ou **install.esd**, clicando em **Add** e então selecionar o arquivo.

No final o resultado será esse:

![](https://cdn-images-1.medium.com/max/800/0*aZ69OZgZX3lr5idB.png)

Após isso basta clicar em **Save** e então aguardar o processo.

11- Agora só falta gravar essa ISO no pendrive, aqui você pode usar ferramentas como o **Rufus** ou o **Ventoy**.

## Instalando o Windows com o WinNTSetup

Depois de ter gravado a iso da livecd no pendrive, reinicie o PC e tente dar boot no pendrive, ao ser carregado a livecd terá esse visual:

![](https://cdn-images-1.medium.com/max/800/0*iorgWsMZKEoQ5q1V.png)

Agora que a liveCD iniciou sem problemas, vamos começar a instalar o Windows com o WinNTSetup, e o processo é diferente para BIOS e modo UEFI.

### Sistema BIOS Legado

1-  Abra o programa **AOMEI Partition Assistant**. Vá em **Settings** e selecione **Language** e selecione o idioma Português.

2- Selecione e apague o disco a ser usado para instalar o Windows

3- Agora que o disco está inteiramente apagado, vamos criar duas partições

3.1- A primeira partição será a de **boot**, ela deve ter no mínimo 8Mb, e em formato FAT32.

Basta clicar em **Criar Partição**, a letra dessa unidade pode ser **Z:**.

![](https://cdn-images-1.medium.com/max/800/0*oMciX177hCmmSiEF.png)

Na parte Tamanho e Posição, com o mouse, diminua o tamanho até o mínimo possível, no meu caso o menor tamanho foi 47Mb, por alguma razão não dá para diminuir sem ser arrastando com o mouse, após isso clique em **Ok** e depois em **Aplicar**.

Com isso a partição de boot foi criada, agora vamos marcar essa partição como ativa, selecione a partição Z e no lado esquerdo clique em **Definir partição ativa**, e por fim clique em **Aplicar**.

![](https://cdn-images-1.medium.com/max/800/0*xIFv6nEnJO1uzREM.png)

3.2- Agora vamos criar a partição do sistema, essa partição deve estar em NTFS, Letra C: e você pode usar o resto do espaço do HD, clique em **Ok** e depois clique em **Aplicar**.

![](https://cdn-images-1.medium.com/max/800/0*UXuzrFFwCoe6eV1c.png)

Quando terminar teremos algo como isso:

![](https://cdn-images-1.medium.com/max/800/0*tQzrWz0uJoRAVshd.png)

Como vocês estão vendo, foram criadas duas partições:

- Partição Z, de 46Mb, marcada como ativa e em FAT32.
- Partição C, usando o restante do espaço (19Gb) e em NTFS

4- Agora vamos abrir o WinNTSetup, voltando para a area de trabalho, vá na pasta **UserTools** e entre na pasta do WinNTSetup, e por fim execute o app.

4.1- Em Select location of Windows Installation files, procure e selecione o arquivo **install.wim** ou .**esd**.

4.2- Em Select location of the Boot drive, selecione a partição Z: e ao lado clique no botão com a letra F, isso vai mostrar a janela de formatar a unidade, basta selecionar FAT16, FAT32 ou NTFS.

4.3- Em Select location of the Installation Drive, selecione a partição C:

Em Options escolhemos a versão do Windows que vamos instalar.

Após tudo isso o programa está configurado assim:

![](https://cdn-images-1.medium.com/max/800/0*ey5VhAd9za8tJkF-.png)

5- Agora é só clicar em **Setup** e aguardar o processo terminar. No final o app vai recomendar que reinicie o PC

Se tudo der certo o Windows vai iniciar.

### Sistema UEFI:

1-  Reinicie o PC e tente dar boot no pendrive em modo UEFI.

Após isso a LiveCD vai funcionar e você já estará na Área de Trabalho.

2- Abra o app **AOMEI Partition Assistant**, vá em Settings, Language e mude para Português.

3- Apague todas as partições do disco que você vai instalar o Windows, clique com o direito do mouse sobre o Disco e selecione a opção **Converter em disco GPT**.

![](https://cdn-images-1.medium.com/max/800/0*dcywb5S12rVOgo3a.png)

Após isso o programa vai pedir a confirmação, clique em **Ok**. Depois clique em **Aplicar**, **Prosseguir** e **Yes**.

4- Agora nós vamos criar a partição de boot, porém essa partição EFI é peculiar e não conseguiremos cria-la com o AOMEI Partition Assistente, então vamos usar o **diskpart**.

Na parte de **Assistentes**, clique em **Windows Command Line**.

Ao abrir a janela do cmd, digite “diskpart” e aperte Enter

Agora vamos os comandos abaixo para listar, selecionar o disco e criar partições:

> _list disk_

_Esse comando vai mostrar a lista de HDs disponiveis no sistema_.

> _select disk 0_

_Esse comando vai escolher o disco de acordo com o numero dele, observe na lista qual é o numero do disco que você vai instalar o Windows_.

> _create partition efi size=512_

_Esse comando vai criar uma partição EFI de 512Mb._

> _format quick fs=fat32 label=”EFI”_

_Esse comando formata a partição EFI para FAT32 e será nomeada como “EFI”_

> _assign letter=”Z”_

_Esse comando vai definir qual é a letra da partição._

> _create partition msr size=128_

_Esse comando cria uma partição reservada para o sistema, de 128Mb._

e digite **exit**, para sair do diskpart, veja como ficou no CMD:

![](https://cdn-images-1.medium.com/max/800/0*LKI835ipErX7Dbn4.png)

5- Volte para o AOMEI Partition Assistent, e clique em **Recarregar**, no final conseguiremos ver que as duas partições foram criadas e que sobrou muito espaço livre no HD.

![](https://cdn-images-1.medium.com/max/800/0*aCmEre6C-Zy4mued.png)

Agora só falta criar a partição C: do Sistema, selecione o espaço “não alocado” e crie uma partição NTFS, Letra C e use o restante do espaço do HD.

6- Volte para a Área de Trabalho, entre na pasta **UserTools** e então entre na pasta do **WinNTSetup** e execute o App.

6.1- Em Select location of Windows Installation files, procure e selecione o arquivo **install.wim** ou .**esd**.

6.2- Em Select location of the Boot drive, selecione a partição Z:

6.3- Em Select location of the Installation Drive, selecione a partição C:

Em Options escolhemos a versão do Windows que vamos instalar.

Após tudo isso o programa está configurado assim:

![](https://cdn-images-1.medium.com/max/800/0*5Jtif7LEbnHWuMQf.png)

Agora é só clicar em **Setup** e na próxima janela clicar em **Ok**.

Isso vai fazer o Windows ser instalado, depois disso o programa vai pedir para reiniciar o PC, e então o Windows vai começar a funcionar normalmente.

### Considerações finais:

Bom pessoal, o tutorial termina aqui, se você não estava conseguindo instalar o Windows pelo método padrão de instalação você pode tentar isso para conseguir contornar os problemas de instalação que surgiram antes.

Espero que o tutorial tenha sido útil e em breve o vídeo desse artigo vai entrar no meu canal do YouTube, esse post será atualizado com o link dele posteriormente.
