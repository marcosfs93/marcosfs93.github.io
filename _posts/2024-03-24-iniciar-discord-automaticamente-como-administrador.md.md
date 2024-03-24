---
title: Iniciar discord automaticamente como administrador
date: 2024-03-24
author: M4rQu1Nh0S
tags: [discord, autostart, administrador]
subtitle: Inicie o discord automaticamente como admin, ao iniciar o sistema.
categories: [dicas e tutoriais]
comments: true
#cover-img: /assets/img/path.jpg [foto de capa da pagina]
thumbnail-img: https://marcosfs93.github.io/assets/img/posts/discord.png
share-img: https://marcosfs93.github.io/assets/img/posts/discord.png
layout: post
---

<p align='center'><img alt='logomarca' src="https://marcosfs93.github.io/assets/img/posts/discord.png"/></p>

O discord por padrão não é iniciado como administrador quando ligamos o PC e entramos no Windows, sendo assim é comum que funções como o push to talk não funcionam se a janela do discord não estiver em primeiro plano.

O push to talk é uma função que permite ativar o microfone enquanto pressionamos uma tecla configurada, caso você queira ter controle de quando será ouvido pelas pessoas na sala do discord.

Embora você consiga alterar as permissões do aplicativo, permitindo que ele inicie como administrador, o aplicativo deixa de iniciar automaticamente quando iniciamos o sistema operacional.

Ou seja, se você marcar o discord para abrir sempre como administrador, a função de autorun deixa de funcionar. Se voce não marcar o discord para abrir sempre como administrador, o push to talk não vai funcionar quando o discord estiver minimizado.

No artigo de hoje vamos aprender a como fazer o Discord sempre iniciar como administrador e garantir que ele inicie automaticamente junto com o Windows

## Como configurar
Vamos usar o **Agendador de Tarefas** do Windows para configurar o aplicativo.

1- Acesse o menu iniciar e digite: "Agendador de tarefas", ou nas opções "Ferramentas administrativas do Windows" > "Agendador de tarefas"

2- Ao abrir o agendador de tarefas, na parte da coluna "Ações", clique na opção: **Criar tarefa básica...**

3- Em "Nome:" você pode colocar "discord" mesmo, e então clique em **Avançar >**

4- Marque a opção **Ao fazer logon**, e então clique em **Avançar >**

5- Marque a opção **Iniciar o programa**, e então clique em **Avançar >**

6- No campo **Programa/Script**, insira o caminho para o diretório do discord.

No meu caso, o caminho é esse:
`C:\Users\M4rQu1Nh0S\AppData\Local\Discord\Update.exe`

Isso é só um exemplo, observe como é no seu caso. Basta trocar o nome M4rQu1Nh0S pelo nome do seu usuário.

7- Em **Adicione argumentos (opcional)**, coloque esse argumento:
`--processStart Discord.exe`

Veja como fica no meu caso.
![Exemplo 1](/assets/img/posts/discord_autorun1.png)

8- Na próxima parte, marque a caixa **Abrir a caixa de propriedades da tarefa depois de clicar em concluir** e clique em "Concluir".

9- Depois disso vai abrir uma janela nova, nessa parte clique na opção **Executar com previlégios mais altos** e clique em "Ok"

Veja outra imagem de exemplo
![Exemplo 2](/assets/img/posts/discord_autorun2.png)

Agora é só reiniciar o PC para fazer o teste, quando o Windows iniciar e você logar no usuário o discord vai ser iniciado automaticamente e como administrador. Assim as funções do discord como o overlay e o push to talk vão funcionar a qualquer momento.

Espero que no futuro os desenvolvedores melhorem o discord para que ele abra como administrador, sem afetar a função de iniciar automaticamente junto com o sistema.