---
title: Boot mais rápido mesmo com a /home separada
date: 2023-07-02
author: M4rQu1Nh0S
tags: [boot, mais, rapido, /home, separada, HD, SSD]
subtitle: Saiba como tornar o boot mais rápido com a /home no HD
category: [Dicas e tutoriais, Linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*DlC_WTHcZ3UUiIhV.png
share-img: https://cdn-images-1.medium.com/max/800/0*DlC_WTHcZ3UUiIhV.png
layout: post
---

![](https://cdn-images-1.medium.com/max/800/0*DlC_WTHcZ3UUiIhV.png)<br/>
Quem tem SSDs sabe que uma das maiores vantagens sobre o HD é sua velocidade de leitura e escrita, que consequentemente agilizam em muito o tempo de inicialização do sistema operacional, embora sua desvantagem seja a sua **capacidade total**.

Uma das alternativas quanto a esse problema, é usar HDs junto com SSDs onde o SSD vai armazenar o sistema, para desfrutar das vantagens de velocidade, e os HDs comuns, para desfrutar da sua capacidade máxima de armazenamento.

É possível fazer esse tipo de configuração tanto no Windows quanto no Linux, mas no Linux em particular a coisa simplesmente funciona assim: SSD vai contar a partição raiz do sistema **( / )** enquanto a pasta home ( **/home/user** ) fica no HD.

Dessa forma os arquivos pessoais ficam na pasta home, incluindo arquivos de configuração dos apps enquanto o sistema em sí fica no SSD.

Porém eu observei um problema que no qual o **boot do sistema ficava mais lento**, como se o próprio sistema estivesse no HD ao invés do SSD, no caso eu uso **KDE Neon 20.04**.

Eu não cheguei a testar outros sistemas e nem outros ambientes como o GNOME, mas não era normal o boot ser afetado com a separação da pasta **/home** fora do SSD.

Enfim, eu encontrei uma alternativa que resolve esse problema e hoje venho aqui para compartilhar com vocês o que eu fiz para melhorar o tempo de boot no sistema.

**Conteúdo:**

- [- Causa do problema](#causa-do-problema)
- [- Solução](#solução)
- [- Instruções](#instruções)
- 1[. Crie uma pasta no SSD](#1--crie-uma-pasta-no-ssd)
- 2[. Adicionado permissões de usuário](#2--adicionado-permissões-de-usuário)
- 3[. Use uma LiveCD](#3--use-uma-livecd)
- 4[. Copie o diretório .config da /home para a pasta /user_config](#4--copie-o-diretório-config-da-home-para-a-pasta-user_config)
- 5[. Renomeie e crie um link simbólico da pasta .config](#5--renomeie-e-crie-um-link-simbólico-da-pasta-config)
- 6[. Saia do LiveCD e reinicie o PC](#6--saia-do-livecd-e-reinicie-o-pc)
- [-Referencias](#referencias)

## Causa do problema
Quando logamos no usuário do sistema, o sistema vai carregar os arquivos de configuração do desktop, esses arquivos ficam no diretório **.config**, e esse diretório fica dentro da pasta home, como a pasta /home estava no HD comum… o tempo de leitura era afetado e assim afetando também o tempo de inicialização.

## Solução
Resolvi o problema fazendo com que a pasta .config ficasse no SSD, mesmo que a /home estivesse no **HD**.

A principio eu achei que teria que deixar /home no SSD mesmo e criar links somente das pastas de Downloads, Documentos, etc, mas no final eu consegui criar links somente do diretório **.config**, que acabaria sendo mais prático.

_Daria pra fazer isso também com os diretórios_ **_.local_** _e_ **_.cache_**_, mas como eles não são carregados na inicialização do sistema eu decidi manter no HD, mas se quiser pode manter eles no SSD também._

## Instruções
Sabendo que será necessário mover o diretório **.config** para o SSD, devemos criar um link em seu antigo local: a pasta /home que está no HD. vamos começar:

### 1- Crie uma pasta no SSD
Vamos criar uma pasta dentro da raiz do sistema, pra isso é só abrir o terminar e digitar o seguinte comando:

    $ sudo mkdir /user_config

Veja como fica no gerenciador de arquivos:

![](https://cdn-images-1.medium.com/max/800/0*1dRjk5rR5X4e8c-u.png)

### 2- Adicionado permissões de usuário
Agora que a pasta foi criada, precisamos mudar o dono dessa pasta, que será o usuário comum.

Ainda no terminal digite o comando:

    $ sudo chown marcos:marcos /user_config

Esse comando vai me tornar o dono dessa pasta, e consequentemente eu vou poder ler e gravar dados dentro dela, o que antes só seria possível usando o root.

No seu caso é só trocar **marcos:marcos** pelo seu nome de usuário.

### 3- Use uma LiveCD
Vamos precisar mover o diretório .config para um novo local e para evitar problemas de fazer isso com o sistema principal ligado, é recomendado prosseguir através da live CD de alguma distro.

Baixe e reinicie o PC dando boot em alguma live CD antes de continuar com o tutorial.

### 4- Copie o diretório .config da /home para a pasta /user_config
Agora é só copiar a pasta .config da **/home** que está no HD para a pasta **/user_config** do SSD, recomendo usar **rsync** para fazer a cópia

Como estamos usando uma LiveCD, você vai precisar montar a partição do SSD contendo o sistema e a partição contendo a partição com a /home.

Geralmente elas são montadas no diretório /media, identifique o diretório do SSD e o HD e use o comando abaixo para copiar a pasta **.config**

**Use o comando:**

> $ sudo rsync -av **/media/livecd/HDD/home/user/.config** **/media/livecd/SSD/user_config**

Ao concluir, no gerenciador de arquivos a pasta **user_config** ficará assim:

![](https://cdn-images-1.medium.com/max/800/0*-HFrxC16tA4rEP0D.png)

### 5- Renomeie e crie um link simbólico da pasta .config
Agora que a pasta .config já esta no SSD, vamos renomear a pasta .config que está em /home, pois com isso podemos “reverter” caso ocorra problema.

Use esse comando no terminal:

    $ sudo mv  /media/livecd/HDD/home/user/.config /media/livecd/HDD/home/user/.config_bkp

Depois disso vamos criar um link simbólico da pasta .config em /home que **vai redirecionar** para a pasta .config localizada em /user_config.

Use o comando:

    $ sudo ln -fs  /user_config/.config /media/livecd/HDD/home/user/.config

Após isso conseguiremos ver que no gerenciador de arquivos a pasta .config dentro da pasta /home é um link:

![](https://cdn-images-1.medium.com/max/800/0*FsXPxogaDrlBXKSL.png)

Vejamos as propriedades do link:

![](https://cdn-images-1.medium.com/max/800/0*3PR2l0nGp5A0sFjn.png)

### 6- Saia do LiveCD e reinicie o PC:
Com isso terminamos, reinicie o PC para iniciar o sistema e veja o resultado, a inicialização da sessão do KDE vai estar mais rápida.

Se não houver problemas, você poderá apagar a pasta **.config_bkp** quando quiser, que é referente ao backup que fizemos antes.

Alias você pode fazer o mesmo com as pastas **.cache e .local** seguindo as dicas desse tutorial, você também pode usar a pasta **/user_config** para por exemplo colocar games que vão se beneficiar ao rodar em SSDs, caso não estejam instalados diretamente no SSD na sua instalação.

Sempre use aplicativos como o **baobab** para ficar ciente do tamanho dos diretórios antes de decidir passar para o SSD.

É isso, espero ter ajudado.

#### Referencias:
[https://plus.diolinux.com.br/t/pasta-home-separada-boot-lento/48016](https://plus.diolinux.com.br/t/pasta-home-separada-boot-lento/48016)

