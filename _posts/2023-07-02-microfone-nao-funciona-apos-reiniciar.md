---
title: Microfone não funciona ao reiniciar o sistema
date: 2023-07-02
author: M4rQu1Nh0S
tags: [microfone, não, funciona, reiniciar, sistema]
subtitle: Saiba o que eu fiz para resolver o problema
category: [Dicas e tutoriais, Linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/0*JcOMwiz6Hab4SRF-.png
share-img: https://cdn-images-1.medium.com/max/800/0*JcOMwiz6Hab4SRF-.png
layout: post
---

<p align='center'><img alt='alsamixer' src="https://cdn-images-1.medium.com/max/800/0*JcOMwiz6Hab4SRF-.png"/></p>
Minha placa mãe tem som onboard com o chip VIA VT1705, porém o driver para Linux não funciona completamente. Por causa disso, enfrento um problema onde o microfone para de gravar após reiniciar o computador. Para contornar a situação, eu preciso trocar a entrada do microfone da porta frontal para a traseira nas configurações de som do sistema.

No entanto, toda vez que reinicio o PC, o microfone para de funcionar novamente e tenho que trocar a entrada do microfone repetidamente para fazê-lo funcionar novamente. Se você também enfrenta esse problema, onde o microfone para de gravar após reiniciar o computador e volta a funcionar somente após a troca entre a porta frontal e traseira, neste tutorial, vou demonstrar como criar um script que faça a troca automaticamente.

**Conteúdo**

1. [Ative as opções do mixer](#ative-as-opções-do-mixer)
2. [Requisitos para criar o script](#requisitos-para-criar-o-script)
3. [Criando o script](#criando-o-script)
4. [Fazendo o script iniciar junto com o sistema](#fazendo-o-script-iniciar-junto-com-o-sistema)
5. [Caso o sistema use o PipeWire](#caso-o-sistema-use-o-pipewire)
6. [Considerações finais](#considerações-finais)

## Ative as opções do mixer
1- Abra o terminal e digite o comando “**alsamixer**”

2- Pressione a tecla “**F6**” e selecione a placa de som, que neste caso é “**HDA Intel PCH**”

3- Pressione a tecla “**F3**” para acessar a seção “**Playback**” e use as teclas direcionais para navegar entre as opções

4- Procure pelas opções “**Dynamic**”, “**Independent**” e “**Loopback**” e habilite-as usando as teclas direcionais para cima e para baixo, deixando-as como “**Enabled**”.

## Requisitos para criar o script
Para trocar automaticamente as portas do microfone assim que o sistema iniciar, vamos usar o **pacmd** do PulseAudio por meio de um script. Para usá-lo, é necessário saber os endereços da porta frontal e traseira do microfone.

Para descobrir esses endereços, execute o seguinte comando:

    $ pacmd list-sources | grep -e 'index:' -e device.string -e 'name:'

Isso vai trazer uma lista parecida com essa:

> _*index: 1_
>
> **_name:_** _<alsa_input.pci-0000_00_1b.0.analog-stereo analog-input-_**_front_**_-mic>_
>
> _index: 2_
>
> **_name:_** _<alsa_input.pci-0000_00_1b.0.analog-stereo analog-input-_**_rear_**_-mic>_

O endereço referente as entradas do microfone estão na linha **name**, agora já podemos criar o script.

## Criando o script
Para criar o script de troca automática de portas do microfone, siga os passos abaixo:

1- Abra o editor de texto do sistema e insira o seguinte conteúdo no arquivo de texto:

> _#!/bin/bash_
>
> _sleep 3 &&_ **_pactl set-source-port alsa_input.pci-0000_00_1b.0.analog-stereo analog-input-front-mic_**
>
> _sleep 3 &&_ **_pactl set-source-port alsa_input.pci-0000_00_1b.0.analog-stereo analog-input-rear-mic_**
>
> _exit;_

Certifique-se de salvar o arquivo com a extensão .sh e escolha um nome para o arquivo, como “**refresh_mic.sh**”.

O script funciona da seguinte forma: quando executado, o microfone frontal é selecionado após 3 segundos e, em seguida, o script alterna para a porta traseira após mais 3 segundos. Se o seu microfone estiver conectado na porta traseira, o script primeiro mudará para a porta frontal e, em seguida, para a traseira. Isso evita que você precise fazer essa troca manualmente.

3- Após salvar o script, mova-o para o diretório /usr/bin com o seguinte comando:

    $ sudo mv refresh_mic.sh /usr/bin

4- Tornar o script executável com o seguinte comando:

    $ sudo chmod +x /usr/bin/refresh_mic.sh

## Fazendo o script iniciar junto com o sistema
O script que criamos vai trocar automaticamente as entradas do microfone para você. Para que isso aconteça assim que você logar no sistema, precisamos configurar a inicialização automática do script.

Para isso, basta criar um arquivo dentro do diretório “**/home/usuário/.config/autostart**”. Nomeie o arquivo como “**refresh_mic.desktop**”.

Dentro deste arquivo, cole o seguinte conteúdo:

> _[Desktop Entry]_
>
> _Exec=_**_/usr/bin/refresh_mic.sh_**_
> Icon=
> Name=refresh_mic.sh
> Path=
> Terminal=False
> Type=Application_

Com essas configurações, mesmo que você reinicie a máquina, o microfone estará sempre pronto para uso.

## Caso o sistema use o PipeWire
Se o sistema estiver usando o PipeWire, uma nova infraestrutura de mídia para sistemas Linux que substitui o PulseAudio e o JACK Audio Connection Kit (JACK), pode ser necessário instalar o pacote **pulseaudio-utils** para que o script funcione corretamente, já que algumas distribuições que usam o PipeWire não possuem as ferramentas **pacmd** e **pactl** do PulseAudio.

Geralmente o nome do pacote é o mesmo para a maioria das distribuições, basta rodar o comando de instalação de acordo com a distribuição

**Ubuntu/Debian:** `$ sudo apt install pulseaudio-utils`

**Fedora:** `$ sudo dnf install pulseaudio-utils`

### Considerações finais
Com essas configurações, mesmo que você reinicie a máquina, o microfone estará sempre pronto para uso.
