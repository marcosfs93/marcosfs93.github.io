---
title: Parametro intel_idle.max_cstate
date: 2023-07-02
author: M4rQu1Nh0S
tags: [parametro, opção, intel_idle, max_cstate, CState]
subtitle: Um parametro que limite o uso do CState da CPU
category: [Dicas e tutoriais, linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*V_T_gaLGOAfXslGP.png
share-img: https://cdn-images-1.medium.com/max/800/0*V_T_gaLGOAfXslGP.png
layout: post
---

Se você tem problemas de congelamento no PC e precisa desativar o C-State da CPU, terá que usar o parâmetro “intel_idle.max_cstate” na inicialização do sistema.

Esse parâmetro vai carregar um módulo do kernel chamado **intel_idle** e dependendo do numero que vem depois de **max_cstate** você pode escolher qual o **C-State máximo** que a sua CPU vai usar.

Por exemplo:

Usando o parâmetro **“intel_idle.max_cstate=0”** o C-State máximo da CPU será o **C0**.

Enquanto com **“intel_idle.max_cstate=2”** o C-State máximo será C1E que é mais econômico que C0.

## Como encontrar as opções de C-State
O numero de opções variam de acordo com o processador e para saber quais opções você pode usar basta abrir o terminal e usar esse comando:

> _grep . /sys/devices/system/cpu/cpu0/cpuidle/_**_state*_**_/name_

![](https://cdn-images-1.medium.com/max/800/0*V_T_gaLGOAfXslGP.png)

Se eu quiser definir o C-State máximo como C1E, o parâmetro será **intel_idle.max_cstate=2**.

Porque no comando acima o C-State **C1E** está no diretório **state2**

>/sys/devices/system/cpu/cpu0/cpuidle/**state2**/name:**C1E**

## Como adicionar o parâmetro no kernel
Esse parametro é aplicado antes da inicialização do kernel e ele é aplicado no GRUB que é o inicializador padrão no Linux.

Basta abrir o arquivo grub, ele fica no diretório /etc/default e pode ser aberto por comando:

    $ sudo nano /etc/default/grub

![](https://cdn-images-1.medium.com/max/800/0*f3MONPGJN7A9pofy.png)

Basta adicionar o parâmetro na linha **GRUB_CMDLINE_LINUX_DEFAULT** como na imagem acima.

Basta salvar o arquivo e depois rodar o comando:

    $  sudo update-grub

Por fim basta reiniciar o PC.

### Referencias:

- [https://gist.github.com/wmealing/2dd2b543c4d3cff6cab7](https://gist.github.com/wmealing/2dd2b543c4d3cff6cab7)
- [https://github.com/cyring/CoreFreq](https://github.com/cyring/CoreFreq)

