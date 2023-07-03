---
title: Backup automático do timeshift não funciona
date: 2023-07-02
author: M4rQu1Nh0S
tags: [backup, automatico, timeshift, não funciona, como, resolver]
subtitle: Saiba como resolver esse problema
category: [Dicas e tutoriais, Linux]
comments: true
#cover-img: /assets/img/path.jpg
thumbnail-img: https://cdn-images-1.medium.com/max/800/1*faTjGReS9EC7bnHTBNlmsA.png
share-img: https://cdn-images-1.medium.com/max/800/1*faTjGReS9EC7bnHTBNlmsA.png
layout: post
---

O timeshift no Ubuntu e no Linux Mint funciona perfeitamente, e desde que eu conheci esse aplicativo eu não pensei em usar outro. Ao migrar para o Arch Linux eu queria continuar usando esse app para fazer os snapshots da partição BTRFS do sistema.

Após conseguir instalar o app e depois de aprender a configurar adequadamente o subvolume @, eu consegui fazer os snapshots no timeshift igual eu conseguia no Ubuntu e Mint.

Porém eu percebi dias depois que os snapshots automáticos não estavam acontecendo, algo que é configurado nessa parte:

<p align='center'><img alt='Screenshot da configuração dos agendamentos de backup automático' src="https://cdn-images-1.medium.com/max/800/1*faTjGReS9EC7bnHTBNlmsA.png"/></p>

Eu tinha configurado o timeshift para manter 3 backups da semana e 6 backups diários, mas nenhum backup automático aconteceu.

Para resolver isso era necessário habilitar um serviço do systemd chamado **cronie**.

Por alguma razão o pacote do timeshift não habilitava esse serviço por padrão e então os backups automaticos não aconteciam. Se você usa Arch Linux, timeshift, e sofre com esse problema, faça o seguinte:

1- Abra o terminal e consulte o serviço com o comando:

    $ systemctl list-unit-files | grep cronie

Aqui o resultado estava:

> **cronie**.service disabled disabled

Isso informa que o serviço está desativado, precisamos então habilitar esse serviço e deixar que ele inicie automaticamente junto com o sistema.

2- Vamos iniciar esse serviço, use o comando:

    $ systemctl start cronie

3- Veja se o serviço foi iniciado, use o comando:

    $ systemctl status cronie

Aqui o resultado que apareceu foi esse:

```sh
● cronie.service — Periodic Command Scheduler
 Loaded: loaded (/usr/lib/systemd/system/cronie.service; enabled; preset: disabled)
 Active: active (running) since Mon 2023–06–19 21:24:22 -03; 15min ago
 Main PID: 2828 (crond)
 Tasks: 1 (limit: 19124)
 Memory: 960.0K
 CPU: 3ms
 CGroup: /system.slice/cronie.service
 └─2828 /usr/bin/crond -n
```

Active significa ativo, então o serviço está rodando neste momento.

4- Faça que esse serviço inicie junto com o sistema, use o comando:

    $ systemctl enable cronie

Agora o serviço vai iniciar junto com o sistema na proxima vez que você reiniciar o sistema.

O timeshift usa o cron, um agendador de tarefas do sistema. Sem ele os backups automaticos não funcionam, com ele ativo o timeshift vai funcionar tão bem no Arch como funciona no Ubuntu e no Mint.

### Referencias:
[https://gist.github.com/ovelny/12ccdb8ebcaaecaebdab228e902dfef5](https://gist.github.com/ovelny/12ccdb8ebcaaecaebdab228e902dfef5)

