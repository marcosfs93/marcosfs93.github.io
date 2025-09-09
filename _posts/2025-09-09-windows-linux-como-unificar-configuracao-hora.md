---
title: Windows e Linux: como unificar a configuração de hora
date: 2025-09-09
author: M4rQu1Nh0S
tags: [Windows, Linux, Data, Hora, Relógio]
subtitle: Veja como corrigir e manter a hora sempre certa em ambos
categories: [windows, linux]
comments: true
#cover-img: /assets/img/path.jpg [foto de capa da pagina]
thumbnail-img: /assets/img/posts/relogio_linux_windows.png
share-img: /assets/img/posts/relogio_linux_windows.png
layout: post
---

<p align='center'><img alt='ilustração de um relogio abaixo da logo do windows e do linux' src="/assets/img/posts/relogio_linux_windows.png"/></p>
Se você usa Windows e Linux em dual boot, já deve ter notado o relógio errado ao trocar de sistema. Isso acontece porque cada um interpreta o horário de forma diferente.

Para resolver o problema precisamos configurar um dos dois sistemas para usar a mesma configuração de horario do outro. Aqui você pode escolher se prefere configurar o Windows ou o Linux, saiba como fazer a configuração em cada sistema.

## Aplicando a correção:

### Windows:
No Windows precisamos alterar uma configuração no registro, ele vai deixar de usar a Hora local e vai usar o UTC igual o Linux:

1- Vá no Menu Iniciar
2- Escreva "CMD", e na janela ao lado clique em **Executar como Administrador**
3- Digite o comando abaixo e depois aperte Enter
`reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation" /v RealTimeIsUniversal /t REG_DWORD /d 1 /f`
4- Reinicie o sistema

Com isso o Windows vai herdar o horario que você definir no Linux

### Linux:
No Linux vamos alterar a configuração que o faça usar a Hora local ao invés do UTC, como o que ocorre no Windows por padrão.

1- Abra o Terminal do sistema (gnome-terminal, konsole, xterm, etc...)
2- Execute o comando abaixo:
`sudo timedatectl set-local-rtc 1 --adjust-system-clock`
3- Reinicie o sistema

## Conclusão:
Após configurar um dos sistemas o outro vai estar com a hora igual, com isso você poderá alternar entre sistemas sem se preocupar com o fuso-horário.