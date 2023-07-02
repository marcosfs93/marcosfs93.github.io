---
title: Fire Emblem Three Houses - Configuração low-end para o Yuzu
date: 2023-07-02
author: M4rQu1Nh0S
tags: [Fire Emblem, Three Houses, configuração, low, end, baixo]
subtitle: Guia de configuração do jogo para PC fraco
category: [Dicas e tutoriais, Games]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/1*aR9NfSS8HE9BQdfRausbtg.jpeg
share-img: https://cdn-images-1.medium.com/max/800/1*aR9NfSS8HE9BQdfRausbtg.jpeg
layout: post
---

Fala pessoal, hoje estou aqui para compartilhar a configuração que tem o melhor desempenho no Yuzu para Linux com o jogo **Fire Emblem 3 Houses**.

_Post atualizado em 14/07/2022_

O PC que eu tenho é um:

-   Intel i7 2600
-   16Gb de RAM — DDR3
-   NVIDIA GTX 1050ti 4Gb

Embora o PC seja bonzinho ele está um pouco abaixo das configurações mínimas exigidas para rodar o Yuzu, emulador de Nintendo Switch.

Com as configurações padrões do emulador, o Fire Emblem 3 Houses era “injogável” nesse PC, pelo menos era, pois eu encontrei dicas de configuração que me ajudaram a fazer o jogo rodar a no máximo 60 FPS e quase fluídamente durante todo o jogo.

Hoje vou compartilhar a configuração que eu uso nesse PC pra fazer o jogo rodar e a dica se aplica apenas para o Yuzu para Linux mas você pode tentar pelo Windows.

**Conteúdo**

- 1[. Configurações de CPU](#1--configurações-de-cpu)
- 2[. Configuração de GPU](#2--configuração-de-gpu)
- 2.1[. Gráficos](#21--gráficos)
- 2.2[. Avançado](#22--avançado)
- 3[. Dicas extras](#3--dicas-extras)
- 3.1[. MOD 60 FPS](#31--mod-60-fps)
- 4[. Solução para problemas de travamentos aleatórios](#4--solução-para-problemas-de-travamentos-aleatórios)
- 4.1[. Aumentar o limite de mapeamento de memória virtual](#41--aumentar-o-limite-de-mapeamento-de-memória-virtual)
- 4.2[. Desative ou remova o mod 60 fps](#42--desative-ou-remova-o-mod-60-fps)
- 5[. Versão recomendada do Yuzu](#5--versão-recomendada-do-yuzu)
- [- Considerações finais](#considerações-finais)

## 1- Configurações de CPU
Começando pela CPU, as configurações que eu uso são essas:

1- Em **Geral**, na parte **Precisão,** selecione a opção: **Não seguro**.

2- Depois disso selecione a opção **Não usar FMA**.

![](https://cdn-images-1.medium.com/max/800/1*aR9NfSS8HE9BQdfRausbtg.jpeg)

O Intel i7 2600 não tem essa instrução e por padrão o Yuzu deixa o uso de FMA ativo, mesmo que o processador não tenha suporte para tal, daí o jogo fica bem travado e só de desabilitar esse recurso no emulador que o jogo já fica bem melhor.

## 2- Configuração de GPU

### 2.1- Gráficos:
Nas **configurações de API** eu deixo selecionado a **API: Vulkan** e **Dispositivo: NVIDIA GeForce GTX 1050 Ti**.

Imagem:

![](https://cdn-images-1.medium.com/max/800/1*2r9OvvrWZJRqaZhKPJjBtw.jpeg)

### 2.2- Avançado:
Nas configurações avançadas, eu deixei o **Nivel de precisão: High**.

Nas 3 opções seguintes eu deixei:

**Desativado **— Usar sincronização vertical (apenas OpenGL)

**Ativado **— Usar compilação assíncrona de shaders (hack)

**Ativado **— Usar tempo de resposta rápido (hack)

**Filtragem anisotrópica:** Padrão ou **2X**

Imagem:

![](https://cdn-images-1.medium.com/max/800/1*T_2Z5Wx_Km5ENnRQ6UXCQA.jpeg)

Além do FMA desabilitado ter ajudado muito em fazer o jogo rodar melhor, usando a opção “compilação assíncrona de shaders” em conjunto tornou a experiência de jogo muito melhor, pois ocorria muitos stutterings sem essas duas configurações.

## 3- Dicas extras:

### 3.1- MOD 60 FPS:
1- Baixe o mod **60 FPS**, sem ele você pode ficar cravado nos 30FPS nesse jogo.

Você pode encontrar esse patch nessa página do github:

[https://github.com/yuzu-emu/yuzu/wiki/Switch-Mods](https://github.com/yuzu-emu/yuzu/wiki/Switch-Mods)

2- Após baixar o mod, basta extrair ele nessa pasta:

`~/.local/share/yuzu/load/010055D009F78000/`

A pasta “**010055D009F78000**” é de acordo com o **ID do jogo**, esse ID fica disponível na lista de jogos e na parte propriedades.

3- Abra o Yuzu, selecione o jogo na lista e com o botão direito do mouse selecione a opção **Propriedades**

Se você extraiu a pasta **60 FPS** que estava dentro do .zip para a pasta do jogo, que foi exemplificado no passo 2, ele vai aparecer na lista de mods.

Imagem:

![](https://cdn-images-1.medium.com/max/800/1*Z9ru_kuA_8EFk6Ms8zQjFg.jpeg)

## 4- Solução para problemas de travamentos aleatórios:
Pode acontecer de você estar jogando e do nada o jogo congelar e cravar nos **0 fps** enquanto o som continua saindo normalmente.

### 4.1- Aumentar o limite de mapeamento de memória virtual
No caso do Linux isso acontece porque o Yuzu precisa de um numero maior de [“Memory Map”](https://www.kernel.org/doc/html/latest/admin-guide/sysctl/vm.html?highlight=max_map_count#max-map-count) do que o padrão definido pelo Kernel Linux (o valor padrão é **65530**)

Para resolver basta abrir o Terminal usar esse comando para aumentar o limite antes de começar a jogar:

    $ sudo sysctl -w vm.max_map_count=262144

Depois disso basta tentar jogar novamente e ver se o problema foi resolvido, se realmente resolveu você pode tornar essa alteração permanente no sistema.

Você só precisar criar um arquivo que será carregado durante a inicialização do sistema, na prática você só precisa rodar esse comando:

> [_echo ‘vm.max_map_count=262144’ | sudo tee /etc/sysctl.d/99-yuzu-maps.conf_](https://github.com/yuzu-emu/yuzu/issues/7397#issuecomment-974834996)

### 4.2- Desative ou remova o mod 60 fps
O mod 60 fps, como seu nome diz, é um mod que permite que você saia do limite de 30 FPS no jogo para ter no máximo 60 fps.

Porém com esse mod presente as chances de ter travamentos durante o jogo aumentam, por isso eu recomendo que você **desative ou remova** esse mod no jogo, no meu caso o jogo nunca mais teve esses problemas de congelamento após remover esse mod.

## 5- Versão recomendada do Yuzu:
É sempre bom manter o emulador sempre atualizado para obter melhorias de desempenho e bug fixes, mas nem toda atualização é melhor do que a anterior pois pode acontecer do jogo não funcionar em novas versões.

Eu particularmente uso a versão **Release 1057** e **1067** do Yuzu através do GitHub:

[https://github.com/yuzu-emu/yuzu-mainline/releases/tag/mainline-0-1057](https://github.com/yuzu-emu/yuzu-mainline/releases/tag/mainline-0-1057)

[https://github.com/yuzu-emu/yuzu-mainline/releases/tag/mainline-0-1067](https://github.com/yuzu-emu/yuzu-mainline/releases/tag/mainline-0-1067)

Recomendo essas versões pois são as que eu testei, aparentemente essas versões são ótimas pra rodar o Fire Emblem 3 Houses, mas você pode tentar a versão mais recente caso queira testar.

Inclusive eu recomendo que você tenha essa duas versões, pois se o jogo travar com uma versão, continue pela outra.

### Considerações finais:
Basicamente é isso, com essas configurações o jogo vai rodar satisfatoriamente nesse PC, eu não testei outras possibilidades de configuração e acredito que dá pra ganhar um desempenho melhor ainda.

Atualmente eu tenho 130 horas de jogo e já zerei o game 3 vezes, com isso garanto que as configurações indicadas nesse post funcionam.

Testado no Ubuntu 20.04 LTS KDE.

Espero que o artigo tenha sido útil, até a próxima.
